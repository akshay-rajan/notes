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
    - Start the deployment server.
        ```
        npm run dev
        ```
    There is one other way, which is to use `npm create-react-app myApp`, which might take longer.
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

---

### <div style="color:red"> !! The `ReactDOM.render()` method was marked 'deprecated' in React 18 and the new way is to use `ReactDOM.createRoot().render()`:</div>

```javascript
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <h1>Hello, world!</h1>
);
```

---

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

## Props

Props are arguments passed to React components. They are passed via HTML attributes.

We can use props by passing them to a component. They are treated as JavaScript objects.
```jsx
function Card(props) {
  return (
    <img src={props.img} alt="alt">
    <h1>{props.name}</h1>
    <h3>{props.id}</h3>
  );
}
```
We can use them just like using HTML attributes.

```jsx
  ...
  <Card 
    img="https://www.picsum.com/200"
    name="Neo"
    id="1562323"
  />
```

## Map

Map is used to generate multiple components. We apply the `map` method to a list of JavaScript objects, and it takes a function as an argument. The function is applied to each object in the list of objects.

    listOfObjects.map(myFunction);

We can use `map` to create repeating elements.

```jsx
function createCard(contact) {
  return (
    <Card
      key={contact.id}
      name={contact.name}
      img={contact.imgURL}
      tel={contact.phone}
      email={contact.email}
    />
  );
}
function App() {
  return (
    <div>
      <h1 className="heading">My Contacts</h1>
      {contacts.map(createCard)}
    </div>
  );
}
```

React creates a virtual DOM to represent the components. To create this, 
**Each component rendered using a method like `map` should have a unique field named `key`.**

### Filter & Reduce

The **Filter** method *filters* an array and only keeps the elements that meet a particular criteria (predicate).

The **Reduce** method accumulates a value by applying a function to each item in an array.

```jsx
// Map: Double each element
let newNums = nums.map(function (x) {
  return x * 2;
});
// Filter: Only keep numbers that are < 10
let newNums = nums.filter(function (x) {
  return x < 10;
});
// Reduce: Sum an array
let newNums = nums.reduce(function (accumulator, curr) {
  accumulator += curr;
});
```

### Find & FindIndex

These are functions introduced newly, which lets us find the first item that satisfies a condition, and find the index of the first item satisfying the condition, respectively.

```jsx
// Find
let fistNoGT10 = nums.find(function (x) {
  return x > 10;
})
// Find Index
let indexOfFirstEven = nums.findIndex(function (x) {
  return x % 2 == 0;
});
```

### Arrow Functions

Arrow functions are a concise way of representing functions. They utilize the 'fat arrow' notation: `=>`. We can use them along with `map` and `filter` to render repeated components.

```jsx
// Suppose we have a list 'notes' and want to render the 'Note' component for each note
  ...
  <Header />
  {notes.map((note) => (
    <Note 
      key={note.key}
      title={note.title}
      content={note.content}
      />
  ))}
  ...
```

## Conditional Rendering

Conditional rendering is done using the ternary operator

    condition ? if_true : if_false

We cannot include JavaScript statements inside components rendered, using `{}` since they only support expressions. But since ternary operators are expressions, we can use them.

```jsx
let isLoggedIn = false;

function App() {
  return (
    <div className="container">
      {isLoggedIn ? <h1>Hello</h1> : <Login />}
    </div>
  );
}
```

To show something only when a condition is satisfied, we can use `null`, or the 'and' operator: `&&`

```jsx
{isLoggedIn ? <h1>Hello</h1> : null}
// OR
{isLoggedIn && <h1>Hello</h1>} 
// Condition && Expression
```

`&&` works as the Guard Operator, preventing the expression evaluation unless the condition is true.

## State & Hooks

`UI = f(State)`

A **state** is a JavaScript object that stores data and can change over time and affect how a component renders. State is local to the component that defines it, and changes to the state can only be made by that component.

**Hooks** are functions that allow us to manipulate the state of a component. The most commonly used hook is `useState`. Hooks can only be used inside a function's body.

```jsx
const state = React.useState(0);
```

The `useState()` method returns an array with the argument as the initial value (initial state), along with a function. 
We can use *Destructuring* to access the value and function separately.

```jsx
const [count, setCount] = React.useState(0);
```

Now, the `count` variable stores the state, 0, and the `setCount` can be used to update state. 

```jsx
function increment() {
  setCount(count + 1);
}
```

We can use React to make the components responsive, by integrating with HTML events like `onClick`, `onMouseOver`, `onMouseOut` etc.
[(HTML Events Reference)](https://www.w3schools.com/tags/ref_eventattributes.asp)

```jsx
let normalStyle = { "background-color": "white" };
let hoverStyle = { "background-color": "black" };

function hoverEffect() {
  setButtonStyle(hoverStyle);
}
function removeHoverEffect() {
  setButtonStyle(normalStyle);
}
return (
  <button
    onMouseOver={hoverEffect}
    onMouseOut={removeHoverEffect}
    style={buttonStyle}
  >
  ...
```
While handling events, we can obtain the event itself as an attribute, just like vanilla JS.

```jsx
// Using event 'onChange' on an input field
function handleChange(event) {
  setName(event.target.value);
}
```

We can use a single `useState()` to control multiple states using an object.

```jsx
const [fullName, setFullName] = useState({
  fname: "Akshay",
  lname: "Rajan",
});
// fullName is an object with value {fname: "Akshay",lname: "Rajan"}
```

We can update the state conditionally by accessing the previous state of the component like this;

```jsx
setFullName(prevValue => { // prevValue is the previous state
  if (name === "fName") {
    return {
      fName: value,
      lName: prevValue.lName
    };
  } else if (name === "lName") {
    return {
      fName: prevValue.fName,
      lname: value
    };
  }
});
```

* The ES6 *Spread* operator `...` can spread or expand an or object.

  ```js
  let arr1 = ["apple", "banana"];
  let arr2 = ["pineapple",...arr1, "mango"];
  // arr2 becomes ["pineapple", "apple", "banana", "mango"]

  let name = {fname: "John", lname: "Doe"};
  let user = {    // 'user' now contains the 2 attributes
    ...name,      // 'fname' and 'lname' in the 'name' object
    id: 1,
  };
  ```

We can use the `spread` operator in React code to avoid repetition.

```jsx
function handleChange(event) {
  const { name, value } = event.target;

  setContact((prevValue) => {
    return { 
      ...prevValue, // Keeps the previous values
      [name]: value, // The 'name' must be inserted as an array
      // Otherwise it will be interpreted as a string
    };
  });
}
```

> We can pass in the index of an array as the `key`, while using `map`, like
  
```jsx
{items.map((data, index) => <ToDoItem key={index} data={data} />)}
```

We are able to not only pass data, but also functions as `props`. This allows us to maipulate components like deleting an Item from a List.

### Material UI

A library of pre-built React components based on the Google, Material design.

```jsx
npm install @mui/material @emotion/react @emotion/styled
```