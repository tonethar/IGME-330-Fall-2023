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

## II. Get Started

- Create folder named **amiibo-app** and `cd` into it
- Type: `npm create vite@latest`
  - for *Project name*: **type a period** (`.`) to create a project in current **todo-app** folder
  - for *Framework*: choose **React**
  - for *Variant*: choose **JavaScript**
- `npm i`
- `npm run dev`
- Head to localhost to see app running in browser
- Get rid of most of the web files, but keep:
  - **App.jsx**
  - **App.css**
  - **index.html**
    - change the `<title></title>` to "Amiibo Finder"
  - **index.css**
    - to get rid of the vertical centering, comment out or delete `min-height: 100vh;`
  - **main.jsx**
    - remove this line from **main.jsx** - `import './index.css'`
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
  
---

## III.
