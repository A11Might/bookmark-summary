Title: How rqlite is tested – Vallified

URL Source: https://philipotoole.com/how-is-rqlite-tested/

Markdown Content:
**[![Image 9](https://philipotoole.com/wp-content/uploads/2016/04/j.png)](https://www.rqlite.io/)**[rqlite](https://www.rqlite.io/) is a lightweight, open-source, distributed relational database built on [SQLite](http://sqlite.com/) and [Raft](https://raft.github.io/). With its [origins dating back to 2014](https://philipotoole.com/replicating-sqlite-using-raft-consensus/), its [design](https://rqlite.io/docs/design/) has always prioritized reliability, and quality. The robustness of rqlite is also a testament to its disciplined testing strategy: after more than 10 years of development and deployments, users have reported fewer than 10 instances of [panics](https://gobyexample.com/panic) in production.

Testing a distributed system like rqlite is no small feat. It requires careful consideration of various layers: from individual components to the entire system in operation. Let’s explore how rqlite is tested, following its philosophy of maintaining quality without unnecessary complexity.

* * *

### The Testing Pyramid: An Effective Approach

[![Image 10](https://philipotoole.com/wp-content/uploads/2025/01/sloc-test-300x257.png)](https://philipotoole.com/2021-rqlite-cmu-tech-talk)Testing rqlite adheres to the well-known [**testing pyramid**](https://martinfowler.com/articles/practical-test-pyramid.html), which prioritizes unit tests as the foundation, supported by integration tests, and capped with minimal end-to-end (E2E) tests. This strategy reflects decades of software development experience, ensuring test suites remain efficient, targeted, and easy to debug — and in my experience this approach **works**.

#### Unit Testing: The Core of Quality

At the base of the pyramid lies [**unit testing**](https://github.com/search?q=repo%3Arqlite%2Frqlite+path%3A*_test.go&type=code), covering isolated components. Unit testing dominates rqlite’s test suite because it offers the best balance of speed and precision. Given that rqlite’s database layer is built around SQLite, a “shared nothing” architecture, most database-related functionality can be reliably tested with unit tests.

Testing is a huge part of the design process. If a component cannot be unit-tested easily, it often signals issues with its design. A little dependency injection during testing is a good thing, but too much indicates an over-reliance on other components. And an emphasis on clean interfaces ensures that components remain focused on a single task.

As of version 8.34.0, **the entire rqlite code base is approximately 75,000 lines long** (including tests, but excluding imported packages). Of that rqlite’s unit test suite comprises **27,000 lines of source code**, making it the largest testing investment. Despite its breadth, the entire suite runs in just a few minutes, [enabling frequent testing](https://app.circleci.com/pipelines/github/rqlite/rqlite) during development.

* * *

#### System-Level Testing: Validating Consensus

Above unit testing lies [**system-level testing**](https://github.com/rqlite/rqlite/tree/v8.36.4/system_test), which focuses on the interplay between the Raft consensus module and SQLite. Distributed databases often rely on consensus for correctness, making this layer crucial. Tests in this category validate:

*   Replication of SQLite statements across nodes.
*   Behavior of read operations at different consistency levels.
*   Resilience during cluster disruptions, such as node failures and subsequent recoveries, as well as Leader elections.

System tests include both single-node and multi-node configurations, ensuring the database operates correctly under varying cluster conditions. As of version 8.34.0, approximate **7000 lines of system-level tests** **exist**, offering comprehensive coverage of these interactions.

* * *

#### End-to-End Testing: A Minimal Layer

End-to-end testing in rqlite serves as a [**smoke check**](https://en.wikipedia.org/wiki/Smoke_testing_(software)), verifying that the system starts, clusters, and performs basic operations. Written in [Python](https://www.python.org/), [these tests launch real rqlite clusters](https://github.com/rqlite/rqlite/tree/v8.36.4/system_test/e2e) to ensure “happy path” functionality, guarding against embarrassing issues like a cluster failing to start due to a bug in command-line flag parsing.

End-to-end tests are deliberately limited to scenarios that cannot be tested at lower levels. Over-reliance on end-to-end testing is avoided because debugging failures in such tests can become prohibitively costly. For instance, a misconfigured dependency deep in the stack might surface in an end-to-end test, but tracing the root cause would require navigating through numerous layers.

For version 8.340, only **5000 lines of end-to-end tests** **exist**, demonstrating a targeted approach.

* * *

### Performance Testing: Pushing the Limits

![Image 11](https://philipotoole.com/wp-content/uploads/2021/02/5.6.1-annotated-300x159.png)Beyond functional correctness, rqlite undergoes performance testing to evaluate its limits under load. These tests measure metrics such as:

*   Maximum INSERT rates.
*   Handling of concurrent queries.
*   Memory and disk usage during heavy operations.

A notable example involves testing with large SQLite databases, sometimes exceeding **2GB**. Such scenarios highlight bottlenecks like rqlite’s memory management or disk write latencies, which are intrinsic to its architecture. Generating such large datasets efficiently remains an ongoing challenge, with potential solutions involving prebuilt SQLite databases stored in cloud buckets.

Performance testing also ensures stability, identifying issues like [memory leaks](https://philipotoole.com/plugging-a-memory-leak-in-rqlite/) or unexpected Leader elections under stress.

* * *

### Lessons Learned

Testing rqlite has taught me valuable lessons, many of which resonate beyond database development:

1.  **Start Small:** Unit testing is the most effective way to build confidence in your system. If a bug exists, you’ll likely find it faster here than in an integration or E2E test.
2.  **Be Deliberate:** Adding tests at higher levels must be justified. Excessive integration or end-to-end tests can bog down development and debugging.
3.  **Adapt and Iterate:** For example, performance tests revealed that **[fsync](https://man7.org/linux/man-pages/man2/fsync.2.html) calls** were the primary bottleneck, leading to further optimizations in disk usage – such as compressing Raft log entries before writing them to disk.
4.  **Efficiency Matters:** With a suite that runs in a matter of minutes, I can iterate rapidly, a crucial advantage in maintaining an active open-source project.

* * *

### Quality Matters

By adhering to the testing pyramid and focusing on targeted, efficient tests, rqlite maintains high quality while minimizing overhead. Whether through unit tests for component reliability, system tests for distributed consensus, or end-to-end tests for sanity checks, every layer serves a purpose.

As rqlite continues to evolve, so will its testing practices. With distributed systems becoming increasingly complex, maintaining simplicity in testing will remain a cornerstone of its design philosophy. After all, the goal is not just to build a database but to build one that works reliably, and is easy to operate, in the real world.
