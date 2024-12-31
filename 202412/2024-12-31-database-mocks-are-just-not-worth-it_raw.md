Title: Database mocks are just not worth it

URL Source: https://www.shayon.dev/post/2024/365/database-mocks-are-just-not-worth-it/

Published Time: 2024-12-30

Markdown Content:
It’s tempting to rely on mocks for database calls. Mocking is faster and often feels more straightforward. However, testing against a real database uncovers hidden pitfalls that can appear as the application matures. Issues like unique constraint violations, default value handling, or even performance bottlenecks may only surface when the code is exercised against actual data.

The importance of real database testing
---------------------------------------

Consider a simple example where you create a user in your application. One approach uses mocks, while the other uses a real database:

```
# Mocked approach
it 'creates a user (mocked)' do
  user_repo = double('UserRepository')
  expect(user_repo).to receive(:create).with(
    email: 'test@example.com',
    status: 'active'
  ).and_return(User.new)

  service = UserService.new(user_repo)
  service.create_user('test@example.com')
end

# Real database approach
it 'creates a user (real database)' do
  service = UserService.new
  result = service.create_user('test@example.com')

  expect(User.find(result.id)).to be_present
  expect(User.find(result.id).status).to eq('active')
end
```

The real database approach reveals potential problems with data integrity or constraints. It may also highlight how your application handles default values and indexes. By catching these issues early, you save on debugging time and reduce the risk of discovering them too late in production.

Future-proofing your tests
--------------------------

Over time, new features or schema changes can impact how the application interacts with the database. When the database is mocked, these changes might go unnoticed. A test that uses a real database can catch errors sparked by new validations, data type modifications, or changes in timestamp precision. The following test might fail quickly if a new status validation is introduced or if status timestamps are handled differently:

```
RSpec.describe OrderService do
  it 'handles order creation with status tracking' do
    order = described_class.create_order(
      user_id: user.id,
      amount: 100
    )

    expect(order.status_changes).to include(
      from: nil,
      to: 'pending'
    )
    expect(order.status_changed_at).to be_present
  end
end
```

Because it interacts with the real database, this test guards against mismatches between your code and the actual schema.

Maintaining realistic database state
------------------------------------

When you test whether account balances or transaction totals are calculated correctly, a real database can expose concurrency, isolation, and aggregate issues. For instance:

```
RSpec.describe AccountBalanceService do
  it 'calculates correct balance after transactions' do
    account = create(:account)
    create(:transaction, account: account, amount: 100)
    create(:transaction, account: account, amount: -30)

    balance = described_class.calculate_balance(account)

    expect(balance).to eq(70)
    expect(account.transactions.count).to eq(2)
  end
end
```

This approach ensures that transaction handling and aggregate calculations remain accurate as they evolve, catching data consistency problems that mocks might obscure.

Understanding service boundaries in testing
-------------------------------------------

Many applications have multiple layers, such as controllers, services, repositories, and external service integrations. Each layer can focus on its own responsibilities:

```
RSpec.describe OrderProcessingService do
  it 'creates order with proper database state' do
    service = described_class.new
    result = service.create_order(user_id: 1, amount: 100)

    expect(Order.find(result.id)).to be_present
    expect(Order.find(result.id).status).to eq('pending')
  end
end

RSpec.describe OrdersController do
  let(:order_service) { instance_double(OrderProcessingService) }

  it 'delegates to order service' do
    expect(order_service).to receive(:create_order)
      .with(user_id: '1', amount: 100)
      .and_return(OpenStruct.new(id: 1))

    post '/orders', params: { user_id: '1', amount: 100 }
    expect(response).to be_successful
  end
end
```

By allowing the service layer to use a real database while controllers mock the services, you isolate testing concerns. This keeps your tests focused and ensures database interactions are verified in the layer that truly handles them.

Testing strategy and layered responsibilities
---------------------------------------------

For the data access layer, real database testing is essential. Verifying foreign keys, referential integrity, and database transactions helps ensure that the foundation remains strong. At the service layer, real database testing reveals how business logic interacts with data. In contrast, controllers focus on parameter handling and responses and can mock service calls without sacrificing coverage.

Use cases, or interactor layers, can also mock any lower-level services they are orchestrating. This makes it easier to pinpoint errors in the logic that binds multiple services together, without introducing extra reliance on external systems or the database.

Balancing real database tests and mocks
---------------------------------------

Real database tests are especially important for repository methods, complex data relationships, and performance-sensitive scenarios. Meanwhile, mocking remains valuable for verifying higher-level orchestration and external service interactions. Controllers can focus on incoming and outgoing data without worrying about the complexity of database operations or third-party calls.
