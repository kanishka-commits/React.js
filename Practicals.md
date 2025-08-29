
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

`Why in React we prefer arrow functions? this is taken from the surrounding scope → no binding required.`

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

### Toastify

```js
import React from "react";
import { ToastContainer, toast } from "react-toastify";
import "react-toastify/dist/ReactToastify.css";

function App() {
  const showMessage = () => {
    toast.success("Data saved successfully 🚀", {
      position: "top-right",
      autoClose: 3000,
    });
  };

  return (
    <div>
      <button onClick={showMessage}>Click me</button>
      <ToastContainer />
    </div>
  );
}

export default App;
```


### Creeat a To-Do list

```js
import React, { useState, useRef } from "react";

const App = () => {
  const [list, setList] = useState([]);
  const [id, setId] = useState(0);

  const tasknameRef = useRef();

  const handleDelete = (id) => {
    setList(list.filter((item) => item.id !== id));
  };

  const handleAdd = (e) => {
    e.preventDefault();
    const taskname = tasknameRef.current.value.trim();
    if (taskname === "") return;

    setList([...list, { name: taskname, id: id }]);
    setId(id + 1);
    tasknameRef.current.value = "";
  };

  return (
    <>
      {list.map((x) => (
        <div key={x.id} style={{ marginBottom: "10px" }}>
          <h1 style={{ display: "inline", marginRight: "10px" }}>{x.name}</h1>
          <button onClick={() => handleDelete(x.id)}>Delete</button>
        </div>
      ))}

      <form onSubmit={handleAdd}>
        <input type="text" placeholder="Write name of task" ref={tasknameRef} />
        <button type="submit">+</button>
      </form>
    </>
  );
};

export default App;
```


### Axios


```js
import React, { useState, useEffect } from "react";
import axios from "axios";

const App = () => {
  const [arr, setArr] = useState([]);

  useEffect(() => {
    const fetchDetails = async () => {
      try {
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/users"
        );

        if (response.data) {
          // Map all users into objects with name and id
          const users = response.data.map(user => ({
            name: user.name,
            id: user.id
          }));

          setArr(users); // set all at once
        }
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    };

    fetchDetails();
  }, []); // runs once on mount

  return (
    <>
      {arr.map(x => (
        <h1 key={x.id}>{x.name}</h1>
      ))}
    </>
  );
};

export default App;

```

```js
if (response.data) {
          // Use functional form to append to state safely
          setArr(prevArr => [
            ...prevArr,
            { name: response.data[0].name, id: response.data[0].id }
          ]);
```

here we've used prevArr because, we need to have `Functional update` as useEffect remembers the state of variable which was initially declared at the time useEffect was called, so if esrlier it was empty, useEffect will keep ona ading new values without rmembering previous values,

thus we prefer not to use `setArr([...arr, anotherItem])`


### Q. Search & Filter
* Fetch users from API.
* Add a search bar.
* Show only users whose name matches search query.

  ```js
  import React, { useState, useEffect } from "react";
import axios from "axios";

const App = () => {
  const [users, setUsers] = useState([]);
  const [query, setQuery] = useState("");

  useEffect(() => {
    const fetchUsers = async () => {
      try {
        const res = await axios.get("https://jsonplaceholder.typicode.com/users");
        setUsers(res.data);
      } catch (err) {
        console.error(err);
      }
    };
    fetchUsers();
  }, []);

  const filteredUsers = users.filter(user =>
    user.name.toLowerCase().includes(query.toLowerCase())
  );

  return (
    <>
      <input
        type="text"
        placeholder="Search by name..."
        value={query}
        onChange={e => setQuery(e.target.value)}
      />
      <ul>
        {filteredUsers.map(user => (
          <li key={user.id}>{user.name}</li>
        ))}
      </ul>
    </>
  );
};

export default App;
```

### Q. React Toastify
* Fetch API.
* If success → show "Data fetched successfully ✅".
* If error → show "Something went wrong ❌".

```js
import React, { useEffect } from "react";
import axios from "axios";
import { ToastContainer, toast } from "react-toastify";
import "react-toastify/dist/ReactToastify.css";

const App = () => {
  useEffect(() => {
    const fetchData = async () => {
      try {
        await axios.get("https://jsonplaceholder.typicode.com/users");
        toast.success("Data fetched successfully ✅");
      } catch (err) {
        toast.error("Something went wrong ❌");
      }
    };
    fetchData();
  }, []);

  return (
    <>
      <h1>React Toastify Example</h1>
      <ToastContainer />
    </>
  );
};

export default App;
```

### Q.  Form Handling
* Build a form with name, email, password.
* Validate: email must contain @, password min 6 chars.
* Show error messages dynamically.

```js
import React, { useState } from "react";

const App = () => {
  const [form, setForm] = useState({ name: "", email: "", password: "" });
  const [errors, setErrors] = useState({});

  const handleChange = e => {
    setForm({ ...form, [e.target.name]: e.target.value });
  };

  const validate = () => {
    const errs = {};
    if (!form.email.includes("@")) errs.email = "Email must contain @";
    if (form.password.length < 6) errs.password = "Password min 6 chars";
    return errs;
  };

  const handleSubmit = e => {
    e.preventDefault();
    const errs = validate();
    setErrors(errs);
    if (Object.keys(errs).length === 0) alert("Form submitted!");
  };

  return (
    <form onSubmit={handleSubmit}>
      <input name="name" placeholder="Name" value={form.name} onChange={handleChange} />
      <input name="email" placeholder="Email" value={form.email} onChange={handleChange} />
      {errors.email && <p style={{ color: "red" }}>{errors.email}</p>}
      <input
        name="password"
        placeholder="Password"
        type="password"
        value={form.password}
        onChange={handleChange}
      />
      {errors.password && <p style={{ color: "red" }}>{errors.password}</p>}
      <button type="submit">Submit</button>
    </form>
  );
};

export default App;
```

### Q. Modal Popup
* Show a button → “Open Modal”.
* On click → show a modal with text + close button.
* Clicking outside or close button should close modal.
👉 Tests conditional rendering.

```js
import React, { useState } from "react";

const App = () => {
  const [open, setOpen] = useState(false);

  const closeModal = e => {
    if (e.target.className === "modal") setOpen(false);
  };

  return (
    <>
      <button onClick={() => setOpen(true)}>Open Modal</button>
      {open && (
        <div className="modal" onClick={closeModal}>
          <div className="modal-content">
            <p>This is a modal popup!</p>
            <button onClick={() => setOpen(false)}>Close</button>
          </div>
        </div>
      )}
    </>
  );
};

export default App;
```

### Q. Tabs Component
* Create 3 tabs: Home, About, Contact.
* Clicking each shows different content.

```js
import React, { useState } from "react";

const App = () => {
  const [active, setActive] = useState("Home");

  const content = {
    Home: "Welcome to Home!",
    About: "This is About page",
    Contact: "Reach us at contact@example.com"
  };

  return (
    <>
      <div>
        {Object.keys(content).map(tab => (
          <button key={tab} onClick={() => setActive(tab)}>
            {tab}
          </button>
        ))}
      </div>
      <h2>{content[active]}</h2>
    </>
  );
};

export default App;
```

### Q. Dark Mode Toggle
* Add a button to switch between light and dark mode.
* Persist choice in localStorage.

```js
import React, { useState, useEffect } from "react";

const App = () => {
  const [dark, setDark] = useState(false);

  useEffect(() => {
    const saved = localStorage.getItem("darkMode") === "true";
    setDark(saved);
  }, []);

  useEffect(() => {
    document.body.style.background = dark ? "#333" : "#fff";
    document.body.style.color = dark ? "#fff" : "#000";
    localStorage.setItem("darkMode", dark);
  }, [dark]);

  return <button onClick={() => setDark(prev => !prev)}>Toggle Dark Mode</button>;
};

export default App;
```

### Q. Stopwatch / Timer
* Start, stop, and reset a timer.
* Bonus: show time in mm:ss.

```js
import React, { useState, useEffect } from "react";

const App = () => {
  const [seconds, setSeconds] = useState(0);
  const [running, setRunning] = useState(false);

  useEffect(() => {
    let timer;
    if (running) {
      timer = setInterval(() => setSeconds(s => s + 1), 1000);
    }
    return () => clearInterval(timer);
  }, [running]);

  const formatTime = s => {
    const m = String(Math.floor(s / 60)).padStart(2, "0");
    const sec = String(s % 60).padStart(2, "0");
    return `${m}:${sec}`;
  };

  return (
    <>
      <h1>{formatTime(seconds)}</h1>
      <button onClick={() => setRunning(true)}>Start</button>
      <button onClick={() => setRunning(false)}>Stop</button>
      <button
        onClick={() => {
          setRunning(false);
          setSeconds(0);
        }}
      >
        Reset
      </button>
    </>
  );
};

export default App;

```
