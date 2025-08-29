
### !IMP: Whenever you need to see which property to take, simply print console.log(e)
```js
eg:
<input 
  onChange={(e)=>{
  handleChange(e)
  }}
  type="text"
/>

const handleChange=(e)=>{
    console.log(e);
}
```

#### Create dom element in react script (when we add react using cdn links):
```js
var h1 = React.createElement('h1', null, 'Hello from H1')
var parentelement = document.querySelector(.parentelement)
var root = ReactDOM.createRoot(parentelement);
root.render(h1) 
```

Here "null" is the attributes,\
we initialize parentelement as root,\
h1 will be a child for the '.parentelement' class using 'render'


#### Change username on click
```js
//WE CAN'T DO
import React from 'react'

const App = () => {
  let user="Kanishka"
  const handleUser = ()=>{
    user= user==="Kanishka" ? user="Panwar":user="Kanishka";
  }
  return (
    <>
    <h1 onClick={handleUser}>Hello {user}</h1>
    </>
  )
}

export default App

//CORRECT
import React, {useState} from 'react'

const App = () => {
  //We can write name of second element as "X" also
  const [user,changeUser]=useState("Kanishka");

  const handleUser = ()=>{
    user= user==="Kanishka" ? changeUser("Panwar"):changeUser("Kanishka");
  }
  return (
    <>
    <h1 onClick={handleUser}>Hello {user}</h1>
    </>
  )
}

export default App
```

#### Reset a counter
```js
import React, {useState} from 'react'

const App = () => {

  const [count,cCount]=useState(0);

  const handleCount = ()=>{
    if(count==="already zero") cCount(1);
    else cCount(count+1);
  }

  const handleReset=()=>{
    if(count===0 || count==="already zero"){
      cCount("already zero");
    }
    else cCount(0);
  }

  return (
    <>
    <h1 onClick={handleCount}>{count}</h1>
    <button   
      style={{
        backgroundColor:"black", 
        height:"60px", 
        width:"150px", 
        color:"white"}} 
      onClick={handleReset}
    >
      Reset
    </button>
    </>
  )
}

export default App
```
`Note: we add double {} in script becasue 1st one is for JSX and second is or JS object`
even tho it's not ideal to switch data type of counter between numeric and string, bt this is created just for experiment purpose\



https://github.com/user-attachments/assets/ac27a126-dc2c-4e43-8af2-0d7c961c4649

#### Prevent default form behaviour (directly interacting with DOM)

```js
import React from 'react'

const App = () => {
  function handleSubmit(e){
    e.preventDefault();
  }
  return (
    <>
    <form>
      <input type="text"/>
      <button onClick={handleSubmit}type="submit"/>
    </form>
    </>
  )
}

export default App
```

We can also do <button onClick={(e)=>{handleSubmit(e)}}type="submit"/>, bt we prefer it one using extra args

Now without intercating with DOM:
```js
const App = () => {
  const [text,upText]=useState('');
  return (
    <>
    <form>
      <input
        value={text},
        onChange={(e)=>{
            upText(e.target.value)
        }}
        type="text"/>
    </form>
    </>
  )
}
```

Props:\
prop is an object, ths either we can do App=(prop) or App=({name,age,number})

```js
//App.jsx

import React from 'react'
import User from './User'

const App = () => {
  const user={
    name: "Kanishka",
    age: "21",
    number:"1234"
  }
  return (
    <User
      name={user.name}
      age={user.age}
      no={user.number}/>
  )
}

export default App
```

```js
//User.jsx

import React from 'react'

const User = (props) => {
  return (
    <>
        <h2>Name of user is: {props.name}</h2>
        <h2>{props.age}</h2>
        <h2>{props.no}</h2>
    </>
    
  )
}

export default User
```

Now what if I want to pass an array of users then, instead of
```js
const user={
    name: "Kanishka",
    age: "21",
    number:"1234"
  }
```
we'll do
```js
const user=[{
    name: "Kanishka",
    age: "21",
    number:"1234"
  },
  {
    name: "Kanishka",
    age: "21",
    number:"1234"
  },....(and so on)
]
```


Iteration on a MAP:

```js
const App = () => {
  const user=[{
    name: "Kanishka",
  },
  {
  name: "Rajesh",
}]
  return (
    <>
    {user.map((x)=>{
      return <User
      name={x.name}
    />
    })}
    </>
  )
}
```


\Note that here we wrote (x) beacuse USER is an array of object and we iterate over these objects thus we name these objects as "x" and then x.name i.e. object.name


### Adding a card when we take info from input (thirsty pot cards eg):
```js
//App.jsx
import React, {useState} from 'react'
import User from './User'
import Add from './Add'
import "./index.css"

const App = () => {
  const [user,setUser]=useState([{
    name: "Kanishka",
    age: "21",
    number:"1234"
  }])

const addData=(e)=>{
  setUser([...user,e]);
}
  return (
    <>
    {user.map((user)=>{
      return <User
      name={user.name}
      age={user.age}
      no={user.number}
    /> })}
    <Add onAdd={addData}/>
    </>
  )
}

export default App

//Add.jsx

import React, {useRef,useState} from 'react'

const Add = (prop) => {

    const nameRef = useRef();
    const ageRef = useRef();
    const numberRef = useRef();

    const handleSubmit=(e)=>{
        e.preventDefault();
        const newUser = {
            name: nameRef.current.value,
            age: ageRef.current.value,
            number: numberRef.current.value,
          };

        prop.onAdd(newUser);

        // Reset them
        nameRef.current.value = "";
        ageRef.current.value = "";
        numberRef.current.value = "";
    }

  return (
    <form onSubmit={handleSubmit}>
    <input type="text" ref={nameRef}/>
    <input type="text" ref={ageRef}/>
    <input type="text" ref={numberRef}/>
    
    <button type="submit">
        Submit
    </button>
    </form>
  )
}

export default Add

//User.jsx

import React from 'react'


const User = (props) => {
  return (
    <div className="card">
        <h2>Name of user is: {props.name}</h2>
        <h2>{props.age}</h2>
        <h2>{props.no}</h2>
    </div>
    
  )
}

export default User
```

