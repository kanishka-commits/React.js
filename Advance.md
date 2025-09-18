### localStorage
This line stores the INFO in the browser's localStorage — which is a built-in way to save small pieces of data (like text) that persists across page reloads and redirects.

### sessionStorage 
It is a built-in web storage feature in your browser.\
It lets you store key-value data temporarily, for one browser tab/session only.

| Feature            | `sessionStorage`                 | `localStorage`                                   |
| ------------------ | -------------------------------- | ------------------------------------------------ |
| 🕐 Lifetime        | Only while the **tab is open**   | **Persists** even after closing the tab/browser  |
| 🌐 Tab Scope       | **Tab-specific** (not shared)    | Shared across all tabs of same domain            |
| 📦 Storage Limit   | \~5MB                            | \~5MB                                            |
| 🧽 Clears when...? | You close the tab or reload hard | Only clears when you delete manually or via code |
**NOTE: sessionStorage and localStorage can only store strings — not objects, arrays, or any other data types.**

| Step                  | Why it's needed                         |
| --------------------- | --------------------------------------- |
| `JSON.stringify(obj)` | Converts object to string for storage   |
| `JSON.parse(str)`     | Converts it back to object when reading |

### Dependency Array
In React hooks like useMemo, useEffect, and useCallback, the dependency array tells React:\

“Only re-run this logic if something inside the array changes.”\

if its's **empty**, Run this effect only once — right after the component mounts (i.e., gets rendered for the first time).

### propTypes
propTypes is a way to check and validate the props (data) that a React component receives.\

It helps catch bugs early during development.\

eg:
```js
ScoreSummary.propTypes = {
  score: PropTypes.number.isRequired,
  total: PropTypes.number.isRequired
};
```
So if someone tries to use it like:

```jsx
<ScoreSummary score="seven" total="ten" />
```
React will give a warning in the console during development:\
`Warning: Failed prop type: Invalid prop score of type string supplied to ScoreSummary, expected number.`


### displayName
```js
const MyComponent = () => { ... };
```
When defining components in React, each one has an internal name used for:
  - Debugging tools like **React DevTools**
  - Error messages
  - Console logs

By default, React automatically infers the component name:

// React DevTools shows: "MyComponent"

### React.memo()
It's a performance optimization tool.

`Only re-render this component if its props actually change.`
This helps your app run faster when you're rendering lots of components (like 10–20 question reviews)

```js
const X = React.memo((props) => { ... });
```

**NOTE:**
if you're using higher-order functions like React.memo, the displayName can be lost. \
Thus React DevTools may show the component as: `"Memo" or "Anonymous"`

thus we need to set `X.displayName = 'QuestionReview'`


### Key prop, for React’s internal rendering engine

Use key when you 
  - render a list of components using .map()
  - Any time you loop/render multiple elements from an array like:

```jsx
array.map((item) => <Component key={...} />)
```
👉 You must give each item a unique key.

🔍 Why?
React uses the key to track and match items in the DOM when:
  - Re-rendering after state or prop changes
  - Adding/removing/sorting elements in the list

It prevents bugs like:
  - Wrong items updating
  - Flickering UI
  - Poor performance

Common situations where key is required:
| You do this                               | You need `key`? |
| ----------------------------------------- | --------------- |
| `.map()` over an array                    | ✅ YES           |
| Rendering a `<ul><li>` list from data     | ✅ YES           |
| Rendering multiple components dynamically | ✅ YES           |
| Static elements (not in a loop)           | ❌ No            |

`If you're rendering an array of JSX elements, always give each item a key.`

And the key should be: 
  - Unique
  - Stable (shouldn’t change over time)
  - Preferably an ID or unique string, not just the index


### *Trick to check if option selected by user is crct or not:*
```js


question.all_answers.map((option) => {
          const isCorrect = option === question.correct_answer;
          const isSelected = userAnswer === option;

```
iterates over app "option" and if the current selected option is the correct ans, 
isCorrect is true\
if the user ans is the option, then isSelected is true\

### React Context
React Context is used to share data (like state or functions) across your entire app, without passing props manually at every level.\
It's helpful when especially when You have global data (e.g., user info, quiz progress, theme)

`const X = createContext()`
It gives you a Context object with two components:
  - X.Provider → used to provide data i..e shares data and functions to all components under it.
  - X.Consumer → (optional) used to receive data (we now mostly use useContext() instead)
eg `<X.Provider> {y} </X.Provider>`

**Props Drilling v/s Context API**
Prop drilling is when you pass data through many nested components just to reach the one that needs it.\
Using Context avoids this by letting any component access the data directly — keeping your code cleaner and easier to manage.\

instead of :
```js
<App>
  <Parent user="Kanishka" />
</App>

function Parent(props) {
  return <Child user={props.user} />;
}

function Child(props) {
  return <GrandChild user={props.user} />;
}

function GrandChild(props) {
  return <p>Hello, {props.user}</p>;
}
```
we can opt for :
```js
//Just Wrap
<UserContext.Provider value={{ user: 'Kanishka' }}>
  <App />
</UserContext.Provider>

//Use anywhere
const { user } = useContext(UserContext);
```
### REDUX
Redux is a state management library for JavaScript apps\



#### React Reducer
A reducer is a function that controls how your state changes in response to certain actions.\
It takes in:
  - the current state
  - an action (describes what happened)
    
And returns:
  - a new updated state

```js
function reducer(state, action) {
  switch (action.type) {
    case 'ACTION_TYPE':
      return { ...updatedState };
    default:
      return state;
  }
}

```

`const [state, dispatch] = useReducer(reducer, initialState);`
  - state → the current quiz state
  - dispatch(action) → send instructions like START_QUIZ, NEXT_QUESTION, etc.
  - reducer → updates the state based on the action type and data (payload)

**dispatch**
`dispatch({ type: 'SOME_ACTION', payload: someData });`
dispatch(...) is calling the reducer function and Sends an action to the reducer\

```js
{
  type: 'SOME_ACTION',
  payload: someData
}
```
is the `action`

- action.type → tells the reducer what to do
- action.payload → gives it the data to do it (optional)
- reducer → Function that receives action and updates state

**Context API vs Redux**
Context API is mainly for avoiding prop drilling. You wrap a provider at the top level, and any component can directly consume the value. But the limitation is — when the context value changes, all components using that context re-render, even if they don’t all need the updated part. This can lead to performance issues in larger apps.

Redux, on the other hand, is a complete state management library. Components can subscribe only to the specific part of state they care about, so only the relevant components re-render. Redux also comes with powerful debugging tools like Redux DevTools

  ### beforeunload
It's a special browser event that runs when:
  - You try to close the tab or window
  - You refresh the page
  - You navigate away from the current page

This event allows you to warn the user so they don’t accidentally lose their progress.
###  popstate
for backbutton

**window.history.pushState(null, '', window.location.pathname);**
It inserts a dummy entry in the browser's history stack.
So when the user hits the back button, they go from:

```csharp
[Real Page] → [Fake Page from pushState]
```
Pressing Back now just pops that fake entry — and you can catch it using window.onpopstate.\
It recognizes it as fake entry (recognizes by the React app thus update the UI manually) so You never navigated to it naturally (it was added manually),\

*This is how client-side routing works in React (with libraries like React Router).*
Thus, Added to browser history but NEVER Triggers page reload


<img width="611" height="243" alt="Screenshot 2025-08-06 at 1 25 10 AM" src="https://github.com/user-attachments/assets/479e994b-ebff-4a40-95a7-81e4c05c3539" />


### Protected Route
```js
const ProtRoute = ({ children }) => {
  return isAuthenticated ? children : <Navigate to="/" replace />;
};
```
({ children }) - This component receives whatever is inside it in JSX as children.
i.e `<ProtQuizRoute> <QuizPage /> </ProtQuizRoute>`

**This is React's standard way of passing data between siblings:**
  - If siblings are on the same route:A → Parent → B
  - If siblings are not on the same route (i.e., not rendered at the same time): you can use a React Context or Redux store to hold shared data.

Redux stores and manages your app’s data (state) in one central place, and updates it in a predictable, controlled way.

**Switching Between Pages Using React Router:**
  - Using react router dom(RRD):  <Route path="/" element={<HomePage />} />
  - Via Links: <nav> <Link to="/">Home</Link> | </nav>(also vias RRD)


**Strict Mode:**
  - It’s a debugging tool, not a feature that changes your UI.
  - StrictMode does NOT run in production — it's only for development.
    `<React.StrictMode> <App /> </React.StrictMode>`

**How to prevent re-renders in React:**
  - React.memo() – Avoids re-render if props don’t change (for components).
  - useCallback() – Memoizes functions so they don’t change on every render.
  - useMemo() – Caches expensive calculations.
  - Avoid same state update – Don’t call setState if the value hasn’t changed.
  - Split components – Break large components into smaller ones to isolate re-renders.

**How to re-render the view when the browser is resized?**:To re-render a React component when the browser is resized, you can use the useEffect hook with the resize event listener.


### Axios
Axios is a popular JavaScript library used to make HTTP requests (GET, POST, PUT, DELETE, etc.) from:
  - Browser (client-side, e.g. React, Vue)
  - Node.js (server-side

### react-toastify 
It's a small library for React that helps you show toast notifications (those little popup messages that appear at the top/bottom of the screen).



