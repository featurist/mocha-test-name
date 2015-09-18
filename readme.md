# Write the current mocha test name to a global variable

This sounds rediculous, but there really are times when this is useful, hear me out.

Sometimes, when you're testing a web app using browser-monkey, some part of your app makes an asynchronous call that ends and throws an error _after_ the end of the test, sometimes during the next test or test after that. This is notoriously difficult to debug because you don't know which test actually caused the error. This simple module notes the name of the test as it's running, so you can use it in your error messages and find out which test caused the failure.

```sh
npm install mocha-test-name
```

In your test suite:

```js
require('mocha-test-name');
```

In your app:

```js
var testName = window.mochaTestName;
return somethingAsynchronous().then(undefined, function (error) {
  error.message = testName + ': ' + error.message;
  throw error;
});
```
