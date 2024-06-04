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
    <script src="../src/index.js" type="text/JSX"></script>
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

To insert JavaScript `expression` inside the html, use `{}`
```javascript 
const name = "Neo";
ReactDOM.render(<h1>Hello, {name}!</h1>, document.getElementById("root"));

ReactDOM.render(<p>Hello, {34 + 82}!</p>, document.getElementById("root"));

ReactDOM.render(<p>Hello, {`Mr. ${name}!`}!</p>, document.getElementById("root"));
```

We cannnot insert JavaScript `statements` - loops, conditionals etc. like above.

Attributes in JSX must be in **camelCase**.

```jsx 
ReactDOM.render(<p className="heading">Hey</p>, document.getElementById("root"));
```

Best way to style the elements is to add classes to elements using `className` and describe the styles for the classes in a `CSS` file.

To use inline styles, we need to represent the values as a JavaScript object. The css properties must be converted from kebab-case to camelCase (font-size to fontSize).

```jsx
ReactDOM.render(<p style={{ color: "red" }}>Hey</p>, document.getElementById("root"));
```

### [Style Guide for React](https://airbnb.io/javascript/react/)

## React Components

Start with a function with name in PascalCase

```jsx
function Heading() {
  return <h1>Good Morning</h1>;
}
```
This is a component. We can use it while rendering the page by
```jsx
ReactDOM.render(
  <div>
    <Heading />
    ...
```
The componets should be separated into individual files with the extension `.jsx` and leave the `index.js` just as it is. 

Inside `Heading.jsx`, do
```jsx
import React from "react";

function Heading() {
  return <h1>Good Morning</h1>;
}

export default Heading;
```
To use a component, we have to just import it.

```jsx
import Heading from "./Heading";
```
Usually, we only render one component: `App` in the `index.js` file, and in a component named `App.jsx`, we include all the import statements and the rendering logic. 

```jsx
```
```jsx
```
```jsx
```
```jsx
```
```jsx
```
