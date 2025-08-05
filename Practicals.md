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

### Dependency Array
In React hooks like useMemo, useEffect, and useCallback, the dependency array tells React:\

“Only re-run this logic if something inside the array changes.”

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

**PropDrilling**
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

### React Reducer
A reducer is a function that controls how your state changes in response to certain actions.\
  - It takes in:
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
