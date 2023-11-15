# React Amiibo App

## I. Overview
- Let's see how we can build a React app that consumes a web service
  - we will get more practice with components ...
  - and with React's *"Reactivity"* - meaning *data binding* ...
  - and with the core React hooks:
    - [`useState()`](https://react.dev/reference/react/useState)
      - [State: A Component's Memory](https://react.dev/learn/state-a-components-memory)
    - [`useEffect()`](https://react.dev/reference/react/useEffect)
      - [Synchronizing with Effects](https://react.dev/learn/synchronizing-with-effects)
      - [You Might Not Need an Effect](https://react.dev/learn/you-might-not-need-an-effect)
    - [`useContext()`](https://react.dev/reference/react/useContext)
      - [Passing Data Deeply with Context](https://react.dev/learn/passing-data-deeply-with-context)

---

## II. Amiibo API

- Docs: https://amiiboapi.com/docs/
- Playground: https://amiiboapi.com/
- Sample call: https://www.amiiboapi.com/api/amiibo/?name=mario

---

## III. Get Started

- Create folder named **amiibo-app** and `cd` into it
- Type: `npm create vite@latest`
  - for *Project name*: **type a period** (`.`) to create a project in current **todo-app** folder
  - for *Framework*: choose **React**
  - for *Variant*: choose **JavaScript**
- `npm i`
- `npm run dev`
- Head to localhost to see app running in browser
- Get rid of some of the unneeded web files, but keep:
  - **App.jsx**
  - **App.css**
  - **index.html**
    - change the `<title></title>` to "Amiibo Finder"
  - **index.css**
    - to get rid of the vertical centering, comment out or delete `min-height: 100vh;`
  - **main.jsx**
- Make **App.jsx** look like this:

```jsx
import { useState } from "react";
import './App.css'

const App = () => {
  return <>
    <header>
      <h1>Amiibo Finder</h1>
    </header>
    <hr />
    <main>
      <button>Search</button>
      <label>
        Name: 
        <input />
      </label>
    </main>
    <hr />
    <footer>
      <p>&copy; 2023 Ace Coder</p>
    </footer>
  </>;
};

export default App;
```

- View the app in the web browser to be sure it compiles

![screenshot](_images/amiibo-react-app-0.png)
  
---

## IV. Create an XHR helper function

- In **App.jsx**, *above* the `App` component, declare this constant

```js
// app "globals" and utils
const baseurl = "https://www.amiiboapi.com/api/amiibo/?name=";
```

- And implement the `loadXHR()` helper function

```js
const loadXHR = (url, callback) => {
  // set up the connection
  // when the data loads, invoke the callback function and pass it the `xhr` object
};
```

- And here's `searchAmiibo()` - all done:

```
const searchAmiibo = (name, callback) => {
  loadXHR( `${baseurl}${name}`, callback);
};
```

---

## V. Create a callback function

- To test our `searchAmiibo(name, callback)` helper function, let's write a callback function that will be invoked when the amiibo data has downloaded:

```js
 const parseAmiiboResult = xhr => {
    // get the responseText string
   
    // declare a json variable
   
    // try to convert to a json object
    
    // log out number of results (length of json.amiibo)
    console.log(`Number of results=${json.amiibo.length}`);
    
    // loop through json.amiibo and log out character name
  };
```

---

## VI. Test it

- Now everything should work, check the console to be sure
- Try substituting "luigi", "peach" and "rit" to see what you get back

```js
  // call searchAmiibo() with "mario" and our callback function
  searchAmiibo("mario", parseAmiiboResult); // DONE
```

--- 

## VII. Hook the code up to the UI

- Goal: When we click the button, we want to see the web service results of the typed in search term (character name)
- We will need a `useState()` call for `term`
  - need to bind the `<input>` `.value` to `term`
  - need to update `term` whenever `.value` changes
- We need to get button clicking working (fire up `xhr` and download the amiibo data)
- We will need a `useState()` call for `results` (an array of object literals)
- We need to display the `results`

```jsx
      {results.map((amiibo) => (
        <span key={amiibo.head + amiibo.tail} style={{color:"green"}}>
          <h4>{amiibo.name}</h4>
          <img 
            width="100" 
            alt={amiibo.character}
            src={amiibo.image}
          />
        </span>
      ))}
```
- We need to update `results` when the amiibo data has loaded
  - move `parseAmiiboResult(xhr)` into the `App` component and make a small addition
- When you are done, you should have a functioning app:

![screenshot](_images/amiibo-react-app-1.png)
