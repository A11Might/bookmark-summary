Title: Unit Tests As Documentation

URL Source: https://www.thecoder.cafe/p/unit-tests-as-documentation

Published Time: 2024-10-17T04:01:04+00:00

Markdown Content:
_Hello! Let’s continue our series on unit tests by discussing their relation with documentation._

[![Image 1](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb6981fff-754b-461e-98a4-63e2d43f8922_1600x900.png)](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb6981fff-754b-461e-98a4-63e2d43f8922_1600x900.png)

When we think about documentation, we think about comments, README files, or tools like Notion or Confluence. Yet, we often forget about one form of documentation that exists within the code itself: **unit tests**. Indeed, unit tests do more than just validating our code works as expected; they also serve as **living documentation** explaining how our code behaves.

Let’s discuss the three main reasons why unit tests are such a powerful tool for documenting our codebase:

*   **Unit tests explain code behavior**: A unit test usually validates the behavior of a function or method. When a unit test is written correctly, it provides a clear and concise explanation of how a piece of code is supposed to work.
    
*   **Unit tests are always in sync with the code**: One of the biggest challenges with traditional documentation is that they can easily become outdated as the code evolves[1](https://www.thecoder.cafe/p/unit-tests-as-documentation#footnote-1-148529141). However, unit tests are tightly coupled with the code they test. If the behavior of a code changes, its corresponding unit tests should evolve, too. That makes unit tests always up-to-date.
    
*   **Unit tests cover edge cases**: Documentation is also about covering edge cases, such as unexpected inputs. Good unit tests should also cover these cases, which provides valuable documentation insights that may not be captured elsewhere.
    

To maximize the effectiveness of unit tests as documentation, it’s important to follow some best practices:

*   **Descriptive test name**: Make sure the test name clearly conveys what is being tested and the expected outcome.
    
*   **Atomic**: Each test should focus on a single aspect of the function behavior. This makes the test easier to read and ensures it serves as clear documentation.
    
*   **Keep tests simple**: If possible, avoid overly complex tests that require too many steps and can be hard to follow. Make sure an external reader should be able to understand the tested behavior.
    
*   **Keep tests independent**: Make sure unit tests do not depend on each other. Keeping isolated tests also helps readers to understand our tests.
    

Unit tests are more than _just_ a way to validate our code. When written properly, they act as **documentation that reflects the behavior of our code**. Therefore, let’s make sure our tests are as readable and understandable as possible. Note also that I’m not suggesting that unit tests should replace any form of documentation but rather that they should complement and enrich it.

[![Image 2](https://substackcdn.com/image/fetch/w_1456,c_limit,f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0af0acf5-eb65-43a8-b1ae-da49f4e3511c_1600x900.png)](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F0af0acf5-eb65-43a8-b1ae-da49f4e3511c_1600x900.png)

_Tomorrow, you will receive your weekly recap on unit tests._
