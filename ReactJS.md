# React

React is a JavaScript library for building user interfaces. 
It is a front-end JavaScript library.

React is used for single-page applications. It breaks down the User Interface structure to a component tree. 
The individual components are re-rendered when changes occur.

* Go to [CodeSandBox](https://codesandbox.io/) for working in a browser-based codespace.
* For local development, follow these steps:
    - Install node
    - Create a vite application
        ```
        npm create vite@latest my-react-app --template react
        ```
    - Select *React* as framework and *JavaScript* as the variant.
    - Enter the directory and install dependencies 
        ```
        cd my-react-app
        npm install
        ```
    - Start the development server.
        ```
        npm run dev
        ```
    - Open the app on the browser by heading over to 
    http://localhost:5173/

To require the dependencies,

```javascript
var React = require("react");
var ReactDOM = require("react-dom");
```

The new way is to do import / export directly (ES6 feature).
```javascript
import React from "react";
import ReactDOM from "react-dom";
```

## JSX and Babel

React works by these `.jsx` files. These files have HTML in a JavaScript file. The HTML is picked up by a compiler and rendered.

**Babel** is a JavaScript compiler. It compiles next-gen JavaScript like ES6 to browser-compatible version. It is present in the *React* module we have imported above.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>JSX</title>
    <link rel="stylesheet" href="styles.css" />
  </head>

  <body>
    <div id="root"></div>
    <script src="../src/index.js" type="text/javascript"></script>
  </body>
</html>
```

```javascript
import React from "react";
import ReactDOM from "react-dom";

ReactDOM.render(<h1>Hello, world!</h1>, document.getElementById("root"));
```
The `render` method takes a *single* HTML element and displays it inside another element.

JSX is a Syntax Extension of JavaScript. In React, we combine elements, styles and behaviour together.

```javascript 

```

