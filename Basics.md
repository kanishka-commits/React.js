React is a front-end and open-source JavaScript library which is useful in developing user interfaces specifically for applications with a single page (one main HTML page, content updates dynamically). It is helpful in building complex and reusable user interface(UI) components of mobile and web applications as it follows the component-based approach.\
React is written in JavaScript.

React + DOM = Webpages\
React + Native = Mobile Apps

We can use React via **CDN links**  without installing anything via npm. This is actually the simplest way to try React or include it in a small project
Each lifecycle of a component is having 4 phases which include initilization, mount, update, unmount

**React is a library, but when combined with tools like React Router, Redux, Next.js, etc., it can feel like a framework.**

**Features:**
  - It supports server-side rendering.
  - It will make use of the virtual DOM rather than real DOM (Data Object Model) as RealDOM manipulations are expensive.
  - It follows unidirectional data binding or data flow.
  - It uses reusable or composable UI components for developing the view.

Why Virtual Dom: Each time the data changes in a react app, a new virtual DOM gets created. Creating a virtual DOM is much faster than rendering the UI inside the browser. \
SEO FRiendly: It also allows server-side rendering, which boosts the SEO of an app.\
Higher-Order Component(HOC) is a function that takes in a component and returns a new component. \

`Always tell React to do your task, NEVER interact with DOM directly, else changes will not be made on DOM`

`SSR: Server → (renders HTML + data) sends full page → Browser displays instantly → JS takes over.`\
`CSR:Server → sends blank HTML + JS → Browser runs JS → Content appears later.`


**Concept: React uses two virtual DOMs to render the user interface. One of them is used to store the current state of the objects and the other to store the previous state of the objects. Whenever the virtual DOM gets updated, react compares the two virtual DOMs and gets to know about which virtual DOM objects were updated. After knowing which objects were updated, react renders only those objects inside the real DOM instead of rendering the complete real DOM. This way, with the use of virtual DOM, react solves the problem of inefficient updating.**

Few techniques to optimize React app performance:
  - Prevent unnecessary re-renders: Use React.memo and useMemo so components don’t update if nothing changed.
  - Load only what’s needed: Use lazy loading (React.lazy) to load parts of the app only when the user needs them.
  - Keep state small: Don’t put too much in state to avoid slowing down re-renders.
  - Optimize images and files: Compress images and load them lazily to make the app faster.
  - Use production build: The production version of React runs much faster than the development one.

    
What are the different phases of the component lifecycle? Initialization, Mounting, Updating, Unmounting\
*(Mounting refers to putting the elements into the browser DOM)*

To use React: 
  - Install node.js: It provides the environment and tools to develop, build, and run React applications
  - on terminal:
    - npm create vite
    - cd, npm i (for downloading node packages), npm run dev/npm start

Npm Start for CRA projects, Npm run dev for Vite projects\

```js
IMPORTANT:
In index.html we get an empty div with ID as 'root' ans script tag at end of body which includes src='main.jsx',\
In main.jsx, we get ReactDOM.createRoot(document.getElementBYID('root').render(....) here inside render, we'll be wriitng our herojsx i..e APP.jsx + can write <Reactr.StrictMode>
```
`Note:When we use StrictMode, Functional components are rendered twice (mount → unmount → mount again) only in development. This is to ensure your components are “pure” and side-effects (like console.log, API calls, or state mutations) don’t happen unintentionally during renders.`

rafce: React Arrow Function Component Export

## Two-way binding

- If the data in state changes, the UI updates.
- If the user changes the UI input, the state updates.
So there’s a loop (state ↔ UI).

eg:
```js
  const [text, setText] = useState(""); // state
  return (
    <div>
      <input 
        value={text} 
        onChange={(e) => setText(e.target.value)} // state updates on input
      />
      <p>You typed: {text}</p> {/* UI updates from state */}
    </div>
  );
```

## Create React App (CRA) 
It's a command-line interface (CLI) tool that automates the setup of a new React project. It was officially supported by the React team and provided a streamlined way to get started with React development without needing to manually configure build tools like Webpack and Babel. 

## Babel
It's a JavaScript compiler — mainly used to convert modern JavaScript code (ES6+) into backward-compatible JavaScript that can run in older browsers or environments that don’t support the latest features.\

Use in react: Browsers don't understand JSX or some modern JS, so Babel: Converts JSX to regular JavaScript

## JSX
JSX (JavaScript XML) is a syntax extension for JavaScript that lets you write HTML-like code directly in your JavaScript files, especially useful when working with React.

## LIbrary vs Framework
A library is a collection of helper functions or tools you can call whenever and however you like.\
You’re in control of the application flow.\
More flexible (you choose how to use it)\

A framework is a complete structure that dictates how your application should be built.\
The framework controls the flow, not you\
Less flexible (it imposes structure)\

| Problem                 | Simple Explanation                             |
| ----------------------- | ---------------------------------------------- |
| Just the UI             | You must add extra tools for full app features |
| Too flexible            | No set rules – can be confusing for beginners  |
| JSX ≠ HTML              | Looks like HTML but has its own syntax rules   |
| SEO issues              | Bad for search engines unless using SSR tools  |
| Performance tuning      | Needs effort to avoid slow re-renders          |
| Complex advanced topics | Hooks, context, etc., take time to master      |
| Evolving ecosystem      | Tools around React keep changing often         |

you need to add extra libraries like:React Router (for routing), Redux or Zustand (for state management), Axios (for HTTP requests)

## STyling

  - Inline: <div style={{ color: 'blue', fontSize: '18px' }}>Hello</div>
  - Styled Components (CSS-in-JS):
```js
import styled from 'styled-components';

const Button = styled.button`
  background: orange;
  color: white;
`;

<Button>Click Me</Button>
```

## Class componets
Class components in React are a way to define components using ES6 classes. They were the primary method for creating components before the introduction of React Hooks, which enabled functional components to manage state and lifecycle methods.\

Before the introduction of Hooks in React, functional components were called stateless components and were behind class components on a feature basis. 
```js
 class Card extends React.Component{
  constructor(props){
     super(props);
   }
    render(){
      return(
        <div className="main-container">
          <h2>Title of the card</h2>
        </div>
      )
    }
   }
```
## React Router

React Router is a standard routing library for React.\
It allows you to navigate between different pages (components) in a single-page application (SPA) without reloading the page.\
| Feature           | Description                                                |
| ----------------- | ---------------------------------------------------------- |
| `<BrowserRouter>` | Wraps your app and enables routing.                        |
| `<Routes>`        | Holds all the different `<Route>`s (v6+).                  |
| `<Route>`         | Defines which component to show for which path.            |
| `<Link>`          | Replaces `<a>` to move between pages without reload.       |
| `useNavigate()`   | Hook to navigate programmatically (like `history.push()`). |
| `useParams()`     | Hook to get route parameters (like `:id`).                 |

useNavigate(): redirect the user without them clicking a link.
## HOOKS

React Hooks are the built-in functions that permit developers for using the state and lifecycle methods within React components. These are newly added features made available in React 16.8 version.\
Earlier only class components were used for state management and lifecycle methods.\

Rules:
  - Always put hooks at the top of your function component: don’t call hooks inside loops, conditions, or nested functions.
  - Use hooks only inside function components, not in normal functions or class components.



**1. useState() – State Management in Function Components**
State is a built-in object used to store local, changeable data in a component.

- Adds local state to a function component.
- Returns a state variable and a function to update it.
- Re-renders the component when the state changes.
- Commonly used for toggles, counters, form inputs, etc.

- You use `useState` when something on the screen needs to update based on user interaction. (live updates, validations)
- To store and change values (state)
**Why?**  
Because regular variables don’t remember values between renders — `useState` does.


**note**
```
setlist([...list,'A']);
setlist([...list,'B']);
setlist([...list,'C']);
console.log(list);
```
output `['C']`

Similarly with:
```
const increment = () => {
  setCounter(counter + 1);
  setCounter(counter + 3);
};
```

why? State updates in React are asynchronous and batched, so only the last one will matter,\
React does not immediately change list. Instead, it schedules the update, and your function keeps running with the old value of list.\
The state actually updates later when React re-renders the component.

**If you’re looping and want to build a new array → build it outside state and call setState once.\
If you must update multiple times → use the functional form setState(prev => ...).**



**2. useEffect() – Handle Side Effects**

- Runs code after the component renders.
- This hook is for actions that happen outside the component — Useful for API calls, event listeners, timers, or updating the DOM.
- Can be set to run on every render, only once, or only when specific values change.

- You use `useEffect` when your component needs to "do something" after it appears on the screen or when its data changes.
- To run something when the component updates

**Why?**  
Because React updates the screen first, and then you may want to run extra logic (like fetching from an API).

`Have two arguments: useEffect(callback,[dependencies]);'

**3. useContext() – Access Global Context**

- Allows a component to access values from a React Context.
- Eliminates the need to pass props through multiple levels i..e multiple components.
- You use `useContext` when you want global data like dark mode, language, or logged-in user info.


- To share values across components
**Why?**  
Because it makes your code cleaner by avoiding repeated prop passing.

**4. useRef() – For DOM Access or Storing Values Without Re-render**

- Stores a mutable value that does not trigger re-renders when changed.
- Commonly used to access DOM elements or keep track of previous values.

- To store something without re-rendering
- Use useRef if you only need the value at a specific time (like on form submit).
**Why?**  
Because sometimes you need to store something that doesn’t need to affect the UI.
  
---

**5. useMemo() – Memoize Expensive Calculations**

- Caches(remembers) the result of a calculation and only recomputes when dependencies change.
- Useful for improving performance when doing heavy computations or rendering large lists.

- You use `useMemo` when something takes time to calculate and you don’t want to redo it unnecessarily.
  - useMemo → prevents re-calculating processedData on every render.
  - React.memo → prevents Child from re-rendering unnecessarily.

**Why?**  
To make your app faster by avoiding slow re-computations.

---

**6. useCallback() – Memoize Functions**

- Returns a memoized version of a function.
- Helps prevent unnecessary re-renders when passing functions as props to child components.

- To remember functions
**Why?**  
Because functions in JavaScript are recreated every time a component runs, which can be wasteful.
---

**7. useReducer() – Complex State Logic**

- An alternative to `useState` for managing complex or nested state.
- Works like Redux: uses a reducer function to determine the next state based on the current state and action.

- To manage more complex state
- You use `useReducer` when updating state needs multiple conditions or logic.

**Why?**  
Because it organizes your logic better when things get complicated.

---

**8. useLayoutEffect() – Sync Side Effects Before Paint**

- Similar to `useEffect`, but it runs a bit earlier — before the changes are shown to the user.
- Useful for measuring layout or DOM size before showing content to the user.

- To do something before the screen updates
**Why?**  
Because it lets you make adjustments before the user sees anything.
---

**9. useImperativeHandle() – Customize What Ref Exposes**

- Used with `forwardRef` to allow parent components to access specific methods or values from child components.
- Useful for exposing imperative methods like `focus()` or `scrollIntoView()`.

- To control what your component exposes to others
- Mostly used in advanced patterns or reusable component libraries.

**Why?**  
Because sometimes, the parent component needs to directly access or control something inside a child.

---

**📋 Summary Table**

| Hook                  | What it does                          | When to use it                           |
|-----------------------|----------------------------------------|-------------------------------------------|
| `useState`            | Stores values that change             | Button clicks, form inputs, toggles       |
| `useEffect`           | Runs code after render                | API calls, timers, subscriptions          |
| `useContext`          | Shares values globally                | Themes, user login, language              |
| `useRef`              | Stores a value or DOM element         | Input focus, keep values between renders  |
| `useMemo`             | Remembers expensive results           | Calculations, large lists                 |
| `useCallback`         | Remembers functions                   | Functions passed to children              |
| `useReducer`          | Manages complex state                 | Todo lists, multi-step forms              |
| `useLayoutEffect`     | Runs before screen updates            | Measuring layout, animations              |
| `useImperativeHandle` | Exposes custom methods to parent      | Custom components with special behavior   |

**Note:** Hooks must be used inside function components or custom hooks, and always at the top level — never inside conditions or loops.

**CUSTOM HOOKS**
A Custom Hook is just a regular JavaScript function —
  - but its name starts with use (like useSomething)
  - and it uses built-in hooks like useState, useEffect, etc. inside it.\
  - Use when you need the same logic in many components.\

It was introduced in React v16.8.\
Custom Hooks cannot be used inside class components, only inside function components.\



### note: React doesn’t mutate state immediately
```js
import React, { useState } from "react";

function Counter() {
  const [counter, setCounter] = useState(0);

  console.log("🎬 Component rendered, counter =", counter);

  const increment = () => {
    console.log("before update:", counter);
    setCounter(counter + 1);
    console.log("after update:", counter);
  };

  return (
    <div>
      <h1>Counter: {counter}</h1>
      <button onClick={increment}>Increment</button>
    </div>
  );
}

export default Counter;
```

output: 
```
before update: 0
after update: 0   ❌ (still old value, not updated instantly)
🎬 Component rendered, counter = 1   ✅ (updated after re-render)
```

explanation: React’s state is immutable for the current render.\
When a component is rendering, counter has a fixed value (the one React gave it at the start of that render).\
Calling setCounter(...) does not mutate that value. Instead:
  - React schedules a re-render with the new state.
  - After your function finishes, React re-runs the component function with the new state.
  - Only in that new render do you see the updated value.
So inside the same render cycle, counter is still the old value.

Thus, when we do:
```js
const increment = () => {
    setCounter(counter + 1);
    setCounter(counter + 1);
  };
```

We still get ans as counter+1, because they are asynchronous. Thus we've

## CallBack in Updater Function
`setCounter((prev)=>prev+1)`

We use it when **New value depends on previous value and we need synchronization**

## key
A key is a unique identifier that helps React track elements when rendering lists.\

It tells React: “Hey! This item is the same or different from before.”\

When a list updates (items are added, removed, or reordered), React uses keys to: Know which items changed, Reuse elements instead of recreating them, Improve performance and avoid bugs\

NOte: Avoid using indexes (i) as keys unless the list will never change in order or size. Indexes can cause UI bugs when items are added/removed.\

## Controlled and Uncontrolled components
Controlled and uncontrolled components are just different approaches to handling input from elements in react. \
  - (useRef) → Uncontrolled form. React doesn’t track changes until submit.
  - (useState) → Controlled form. React updates state as user types, which is cleaner for validation, live previews, etc.
    

| Feature                | Controlled                                 | Uncontrolled            |
| ---------------------- | ------------------------------------------ | ----------------------- |
| Value comes from       | React state (`useState`)                   | DOM (`useRef`)          |
| React controls value?  | ✅ Yes                                      | ❌ No                    |
| When value is accessed | On every change                            | On form submit or event |
| Ideal for              | Dynamic inputs, validations, complex forms | Simple or legacy forms  |

## Props
Props (short for properties) are a way to pass data from one component to another in React — usually from a parent to a child component.\
Props are read-only (a child cannot modify them) i..e props are immutable.

## Types of side effects

- Effects Without Cleanup: These are effects that don’t need any special handling when the component updates or unmounts.
- Effects With Cleanup: Some effects do need to clean up resources when the component unmounts or before the next effect runs again. Eg: setInterval(), using clearInterval()


## Error Boundaries
Thye're special React components that catch errors in other components (during rendering or lifecycle methods) and show a fallback message instead of crashing the whole app.\

Usage: If something breaks inside your component (like a bug in render), your whole React app might go blank or stop working.\

With an error boundary, you can: Catch the error, Show a friendly message like "Something went wrong", Keep the rest of the app running\



