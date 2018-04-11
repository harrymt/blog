---
layout: post
title: Stubs, Spies and Mocks in JavaScript
tags: [javascript]
---

<div class="message">
Testing with Mocks in JavaScript.
</div>

I have put together a [GitHub repo](https://github.com/harrymt/js-mocking-demo) as an example of how to use Stubs, Spies and Mocks for JavaScript tests. This demo project shows how you would use a popular mocking library called [SinonJS](http://sinonjs.org/) (Pronounced "sigh-non") to `Mock` a simple in-memory store.

### Technologies

- [SinonJS](http://sinonjs.org/) (Pronounced "sigh-non")
- [MochaJS](http://mochajs.org)

### Install

To install the mocking library Sinon, to give you spies, stubs and mocks:

```
$ npm i -D sinon
```

To have the `describe("...")` and `it("...")`:

```
$ npm i -D mocha
```

### Basic In-memory storage

To follow along with the example repo, clone it, then call the following command to run the mocking tests.

```
$ git clone https://github.com/harrymt/js-mocking-demo.git .
$ npm test
```

## Stubs

Replace calls to databases or network requests.
Stubbing (replaces) a function.

*Pros*:
- Replace calls to db
- Replace network requests with this
- Force an error to test error handling


### Unit Test

```js
// index.js
const {stub, assert} = require("sinon");

const database = require("./src/db");
const store = require("./src/store")(database);

it("basic stub", () => {
    // Stub database method
    const getUsers = stub(database, "getUsers");

    // Overrides database.getUsers() implementation
    getUsers.onFirstCall().returns([harry, john]);

    // `store.database.getUsers()` returns `[harry, john]`
    assert.match(store.database.getUsers().length, 2)

    // Put method back to normal 'remove stub'
    getUsers.restore();
});
```


## Spies

Spy on functions and see when or if they are called.

Pros:
- Check if a method has been called with certain variables
- Check if callbacks have been called, and how many times

### Unit Test

```js
// index.js

const {spy, assert} = require("sinon");
const database = require("./src/db");
const store = require("./src/store")(database);

it("basic spy", () => {
    // Spy on a variable
    // Sinon is now watching this variable
    const callback = spy();

    // Use the variable in our function
    store.addUser(john, callback);

    // Now check that `callback([harry, john])` was called inside of `database.addUser()`
    assert.calledWith(callback, [harry, john]);
});
```

## Mocks

Use mocks to stub out whole objects.

```js
// index.js

const {mock, assert} = require("sinon");
const database = require("./src/db");
const store = require("./src/store")(database);

it("mocks", () => {
    // Mock our whole database object
    var db = mock(store.database);

    // Setup our mock to replace functionality,
    // if all we care about is that these methods
    // were called once, we replace them with checks.
    db.expects("setUsers").once();

    // This needs to return something to continue with the method
    // so we stub out the return value of `getUsers()`
    db.expects("getUsers").once().returns([]);

    store.addUser(harry, () => {});

    // Verify that the mocked expects happened
    // setUsers() was called once
    // getUsers() was called once
    db.verify();
});
```


### Further Reading

- [SinonJS docs](http://sinonjs.org/)
- [JavaScript Mocking demo on GitHub](https://github.com/harrymt/js-mocking-demo)
