# Node.js

Node.js is a JavaScript **runtime environment**.

Usually JavaScript runs on the browser.
Node allows us to run JavaScript on the server.

## Get Started

To [Install](https://nodejs.org/en/download/), on Windows, do:

```bash
choco install nodejs-lts --version="20.14.0"
```

Check the version installed:

```bash
node -v
npm -v
```

To start Node **REPL** (Read-Evaluate-Print-Loop), or **run `Node` on the terminal**, just type:

```bash
node
```

To exit this, press `Ctrl + D`.

To interpret a JavaScript file, do:

```bash
node filename.js
```

> Since Node runs on a server, the `console` is the terminal window

The `window` object is replaced with the `global` object.

Try logging the `global` object to see the methods associated with it:

```js
> console.log(global)
<ref *1> Object [global] {
  global: [Circular *1],
  clearImmediate: [Function: clearImmediate],
  setImmediate: [Function: setImmediate] {
    [Symbol(nodejs.util.promisify.custom)]: [Getter]
  },
  clearInterval: [Function: clearInterval],
  clearTimeout: [Function: clearTimeout],
  setInterval: [Function: setInterval],
  setTimeout: [Function: setTimeout] {
    [Symbol(nodejs.util.promisify.custom)]: [Getter]
  },
  queueMicrotask: [Function: queueMicrotask],
  structuredClone: [Function: structuredClone],
  atob: [Getter/Setter],
  btoa: [Getter/Setter],
  performance: [Getter/Setter],
  fetch: [Function: value],
  crypto: [Getter]
}
```

### Module

To import *Common Core modules* in Node, we use `CommonJs` imports (`require` statements) instead of `ES6` imports (`import a from b`).

```js
const os = require('os');

console.log('OS Type:', os.type()); // Windows_NT
console.log('OS Version:', os.release()); // 10.0.1000
console.log('Home Directory:', os.homedir()); // C:Users/user
```

There are some values we always have access to in Node:

```js
console.log(__dirname); // Directory full path
console.log(__filename); // Full path including the filename
```
```js
const path = require('path');

console.log(path.basename(__filename)); // Just the current filename
console.log(path.extname(__filename)); // File extension
console.log(path.parse(__filename)); // Returns an object with all the info
// {
//   root: 'C:\\',
//   dir: 'C:\\Users\\user\\Desktop\\learn_mern\\node',
//   base: 'server.js',
//   ext: '.js',
//   name: 'server'
// }
```

We can create a module, which is just a `js` file:

```js
// math.js
const add = (a, b) => a + b;
const sub = (a, b) => a - b;
// Export the module
module.exports = { add, sub, mul, div };
```
```js
// Alternatively, we can do this to avoid the 'export' at the end
exports.add = (a, b) => a + b;
```

And use it by importing it to our file
```js
const math = require('./math');

console.log(math.add(2, 3)); // 5
```
```js
// Alternatively, we can destructure while importing
const { sub } = require('./math');

console.log(sub(5, 2)); // 3
```

> APIs like `fetch` are missing in Node.js

## Files
