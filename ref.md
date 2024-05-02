# What does React do?

- 2 main things react does:
  > React displays HTML
  > React changes that HTML when the user does something
- React can be thought of as a wrapper around HTML
- we tell React what content we want to show on the screen by creating functions that return JSX.
- These functions that return JSX are called as React Components.
- JSX can return html elements or component elements.
- <h1></h1> if a tag begins with lowercase char, it tells React that we want a plain HTML element
- <ContactList /> if a tag begins with uppercase char, it tells React that we want to find the Component and load its contents

# How does React Application start up?

3 steps:

1. All our project's JS files are 'bundled' together into a single file, then placed onto a server
   Usually refered to as bundle.js file(also called App Bundle). it contains all our code for the entire app.

2. User makes a request to the server using the URL and gets an HTML file(index.html) + the bundle as response
   Index.html only has couple of lines, with link tags and scripts tags that tell the browser about addition JS files need to be fetched from the server
   Browser makes a second request to fetch the bundle.js, which is sent back in the response
3. User's browser executes our code

- index.js is the first file that gets executed when our project starts up
- Find the div with id of root in the DOM
  _const rootEle = document.getElementById('root')_
- tell react to take control of that element
  _const root = createRoot(rootEle)_
- tell React to get JSX from the App component, turn it into HTML and show it in the root
  _root.render(<App/>)_

# Generating a project

- create project using create-react-app
  _npx create-react-app <project name>_
- run the project
  _npm start_
- our browser does not know how to execute JSX.
- dev server uses Babel to turn JSX into normal JS code and it uses Webpack tool to merge all project files into a single file (bundle.js).
  [index.js,App.js,..] -> Babel -> Webpack -> bundle.js

# React library

- library that defined what a component is and how multiple components work together
- import React from 'react';

# ReactDOM library

- library that knows how to get a component to show up in the browser
- import ReactDOM from 'react-dom/client';

# What is JSX?

- it tells React what to render on the screen
- it is not javascript so cannot be run on the browser but is converted to equivalent JS using Babel

<!-- babeljs.io/repl is a tool to show what our JSX is turned into -->

e.g. <h1>Hi there!</h1>

- JSX needs to be returned from a component for React to use it. It acts as an instruction for React, telling it to make an element.

# Printing JS variable in JSX

- use curly braces {} to reference a JS variable or expression
- to print numbers or strings mostly. when trying to print boolean, null, undefined, value not shown. objects give error and arrays are printed as all elements directly

- Other ways to use curly braces {}
  function App() {
  return <h1>{new Date().toLocaleTimeString()}</h1>
  }

- we can customize elements using "props" similar to attributes on HTML elements.
  e.g. <input type="number" min={2} max={10}>
- props can refer to a variable using {}
  e.g. const inputType = "number", minVal = 5;
  <input type={inputType} min={minVal}>
- if prop has a string value, it should be wrapped in double quotes only, type="number"
- if prop is a number, array, object or variable, it should be wrapped in curly braces,
  e.g. min={2}, list={[1,2,3]}, style={{color:'red'}}, alt={message}
- an object cannot be displayed/printed using {} but can be provided as a prop

# Converting HTML to JSX: Rules

- All prop names follow camelCase
  e.g. <textarea autoFocus={true}>
  <input maxLength={5}> instead of maxlength="5"
  here instead of "autofocus" it is written in camel case
- Number attributes use curly braces
- boolean 'true' can be written with just the property name. 'false' should be written with curly braces
  e.g. <input spellCheck> & <input spellCheck={false}>
  same as <input spellCheck={true}>
- the 'class' attribute is written as 'className'
  e.g. <li className="item"/>
- in-line styles are provided as objects.
  e.g. <div style={{color:'red', padding: '5px'}}>

# Module Systems

- export a function to be used in other files
  e.g. function App() { return <h1>Hi</h1> }
  export default App;
- Import function where it needs to be used
  e.g. import App from './App'
- \*Default exports can be renamed in the importing file
  e.g. import MyApp from './App'
- there are 2 ways of exporting variables. 1. default(seen above) 2. Named Export statement
- Named export statement: used when exporting multiple variables, can have as many named exports as we want.
- there can be only 1 default export in a file.
- can be written in 2 ways
  > const message = 'hi'; export {message}
  > export const message = 'hi';
- we can have default export along with multiple named exports
- to use a named export in a file, i.e. import it, we use curly braces
  e.g. import {message} from './App';
- single import statement can get both default + named exports
  e.g. import App, {message} from './App';
- \*Named exports cannot be renamed

# Import path

1. './' or '../' means importing a file we created. This is a relative path.
   e.g. import App from './App';
2. no './' or '../' means importing a package
   e.g. import React from 'react';
   import ReactDOM from 'react-dom/client';

# Props system

- pass data from parent to child
- allow parent to configure each child differently
- one way flow of data. child can't push props back up.
- we can send props to a child component by adding attributes to a JSX element
  e.g. <Child color="red"/>
- React collects all attributes and puts them in an object called "props"
  e.g. {color: 'red'}
- props objects shows up as first argument to child component function and can be used in the child.
  e.g. function Child(props) {
  return <div>{props.color}</div>
  }
- the attribute names/prop names can be anything, few exceptions
- can also use argument destructuring
  e.g. function Child({color}) {
  return <div>{color}</div>
  }
