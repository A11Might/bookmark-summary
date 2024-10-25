Title: Self-documenting Code

URL Source: https://lackofimagination.org/2024/10/self-documenting-code/

Published Time: 2024-10-20T00:00:00Z

Markdown Content:
Think back to the last time you looked at an unfamiliar block of code. Did you immediately understand what it was doing? If not, you’re not alone – many software developers, including myself, find it challenging to grasp unfamiliar code quickly.

Let’s take a look at a simple JavaScript function that creates a user account:

```
async function createUser(user) {
    if (!validateUserInput(user)) {
        throw new Error('u105');
    }

    const rules = [/[a-z]{1,}/, /[A-Z]{1,}/, /[0-9]{1,}/, /\W{1,}/];
    if (user.password.length >= 8 && rules.every((rule) => rule.test(user.password))) {
        if (await userService.getUserByEmail(user.email)) {
            throw new Error('u212');
        }
    } else {
        throw new Error('u201');
    }

    user.password = await hashPassword(user.password);
    return userService.create(user);
}
```

At first glance, this function doesn’t look too bad apart from its use of cryptic error message codes. The argument `user` is apparently an object that contains information about the user to be created. There are a few lines of code that checks if the password conforms to the password policy, using regular expressions. Then, there is a check to see if the user account already exists. Finally, if all the checks pass, the user’s password is hashed, and a function to create the new user is called; it probably returns something on success.

One can certainly do a lot worse than this example, but there is also quite a bit of room for improvement.

> “There are only two hard things in Computer Science: cache invalidation and naming things.” – Phil Karlton

Software developers frequently deal with abstract ideas and complex systems. Translating these abstractions into concrete, meaningful names that accurately reflect their behavior isn’t always straightforward. However, that isn’t really an excuse when we’re dealing with well-understood processes like user account creation, as in our example.

#### Named Constants and Doing One Thing Only

The first change I would make is to use named constants instead of cryptic error codes. Also, putting complex logic, such as the password check, into its own function makes the code easier to read. After all, a function should ideally do one thing and one thing only. Implementing the password check separately allows it to be called from other functions as well.

```
const err = {
    userValidationFailed: 'u105',
    userExists: 'u212',
    invalidPassword: 'u201',
};

function isPasswordValid(password) {
    const rules = [/[a-z]{1,}/, /[A-Z]{1,}/, /[0-9]{1,}/, /\W{1,}/];
    return password.length >= 8 && rules.every((rule) => rule.test(password));
}
```

After these changes, `createUser` should look something like this. We can now immediately tell what would happen if a check fails.

```
async function createUser(user) {
    if (!validateUserInput(user)) {
        throw new Error(err.userValidationFailed);
    }

    if (isPasswordValid(user.password)) {
        if (await userService.getUserByEmail(user.email)) {
            throw new Error(err.userExists);
        }
    } else {
        throw new Error(err.invalidPassword);
    }

    user.password = await hashPassword(user.password);
    return userService.create(user);
}
```

#### Short-circuit Evaluation

The revised code above is now easily readable, and we can leave it as is. However, in this case there’s an opportunity to make the code flow more linear by using short-circuit evaluation.

Short-circuit evaluation allows us to simplify conditional statements by using logical operators. In this case, the **||** operator checks the condition on the left, and if it’s false, it executes the function on the right.

We have also flattened the password validation and existing user checks. The resulting code is shorter and has no nested logic.

```
function throwError(error) {
    throw new Error(error);
}

async function createUser(user) {
    validateUserInput(user) || throwError(err.userValidationFailed);
    isPasswordValid(user.password) || throwError(err.invalidPassword);
    !(await userService.getUserByEmail(user.email)) || throwError(err.userExists);

    user.password = await hashPassword(user.password);
    return userService.create(user);
}
```

#### Type Annotations

Self-documenting code involves writing code with minimal comments, but there is a category of comments that is useful not only for developers but also for compilers and IDEs, and that is annotations about the types of variables and arguments used.

I’m not a fan of TypeScript, but I appreciate its ability to perform static type checks. Fortunately, there’s a way to add static type checking to JavaScript using only JSDoc comments. Alex Harri did an excellent job explaining how you can do that in [this article](https://alexharri.com/blog/jsdoc-as-an-alternative-typescript-syntax) if you’re interested.

The following JSDoc comments make it clear what type of argument `createUser` accepts and what it returns. The type definitions can be automatically picked up by the TypeScript compiler or an IDE like VS Code, giving you real-time feedback when you pass a value with the wrong type.

```
/** @typedef {{ id?: number, birthDate: Date, email: string, password: string }} User */

/**
 * Creates a user and returns the newly created user's id on success
 * @param {User} user
 * @returns <Promise{any}>
 */
async function createUser(user) {
    validateUserInput(user) || throwError(err.userValidationFailed);
    isPasswordValid(user.password) || throwError(err.invalidPassword);
    !(await userService.getUserByEmail(user.email)) || throwError(err.userExists);

    user.password = await hashPassword(user.password);
    return userService.create(user);
}
```

#### Summary

We have turned a seemingly simple but somewhat hard-to-follow function into a self-documenting function by:

*   Using named constants instead of cryptic error codes,
*   Extracting complex logic and putting it in its own function,
*   Using short-circuit evaluation to make the code flow linear,
*   Introducing type annotations to help with static type checking and real-time coding feedback.

* * *

**Related:**

*   [Avoiding if-else Hell: The Functional Style](https://lackofimagination.org/2024/09/avoiding-if-else-hell-the-functional-style/)
*   [Firewalling Your Code](https://lackofimagination.org/2024/08/firewalling-your-code/)
*   [Back to Basics in Web Apps](https://lackofimagination.org/2024/04/back-to-basics-in-web-apps/)
