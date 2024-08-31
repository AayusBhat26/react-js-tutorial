
# React
---
installing react js application 


```
npx create-react-app "folder name or location"
```

> [! info] Make sure that the folder name should be in small letters, since it is the convention set the react js developers i.e. facebook developers.

humare pass generally 2 chizey hoti hai 

1. npm => node package manager => deals with the packages that are present currently (use to perform install, deletion, updation and alternation in packages)
	1. here the package is installed and saved 
	2. we can install the package globally with the help of npm 
2. npx => a part of npm which 
	1. here the package is installed for the short period of time and once the process or functionality of package is complete, it automatically deletes the package. 

`create-react-app` is an utility tool which provides the basic project folder which is predefined by the react developers (facebook developers)

so, we are install the create-react-app for a bit so that it can create the folder structure and once it is done, npx will automatically deletes the same.

"folder name or location" => we have to mention the folder name or location(should be in lower case) 

./ => represents the current folder 
../ => previous folder 




# Components 

> functional components 
> class Components 
> Higher order components 
> Pure Components 

Components
- components are nothing but the part of the application which acts as the building block/s of components.
- component example: 
	- 
- in react js, we have two type of components
	- functional components (mostly yehi use hote hai 99.9%)
	- class components (ab zdya use nhi hote)

## Functional Components 

javascript functions that accept properties (`props`) (optionally) as an argument and return react element (JSX) that describr what should appear on the screen.

initially, these were stateless, i.e. we cannot manage the state through this component as well as inside these components
1. stateless or stateful
but with the introduction of hooks, we can do it with the help of useState
now functional components can now also handle state and side effects, making them capable of performing all tasks that class components can. 


2. no `this` keyword 
unlike class components, functional components do not use this which can make them easier to read and understand 

3. concise syntax 
functional components are usually shorter and more readable, as they are just javascript functions. 

4. performance 
functional component especially with memooization can be more performant due to optimized by react.
```javascript
import React from 'react';

function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}

export default Greeting;

```

```javascript 
import React from 'react';
import Greeting from './Greeting';

function App() {
  return (
    <div>
      <Greeting name="Aayush" />
    </div>
  );
}

export default App;

```

note that app function is the entry point for the react application.

with hooks 

```javascript 
import React, { useState } from 'react';

function Counter() {
  // Declare a state variable 'count' and a function 'setCount' to update it
  const [count, setCount] = useState(0);

  // Function to handle button click
  const handleIncrement = () => {
    setCount(count + 1);
  };

  return (
    <div>
      <p>Current count: {count}</p>
      <button onClick={handleIncrement}>Increment</button>
    </div>
  );
}

export default Counter;

```


with side effects 

```javascript 
import React, { useState, useEffect } from 'react';

function UserProfile({ userId }) {
  const [userData, setUserData] = useState(null);

  // useEffect to fetch user data when component mounts or userId changes
  useEffect(() => {
    async function fetchUserData() {
      const response = await fetch(`https://api.example.com/users/${userId}`);
      const data = await response.json();
      setUserData(data);
    }
    
    fetchUserData();
  }, [userId]); // Dependency array, re-runs effect if userId changes

  if (!userData) {
    return <div>Loading...</div>;
  }

  return (
    <div>
      <h2>{userData.name}</h2>
      <p>Email: {userData.email}</p>
    </div>
  );
}

export default UserProfile;

```


# JSX

JavaScript XML looks similar to HTML but is actually javascript, used to define the UI structure 

# Props 

Properties passed from parent to child component used for communication between components


# Hooks

introduced to react in version 16.8 
whenever there is change in the value inside of any hook, it re-renders the entire application. 

>[! info] Hooks are functions that lets us `hook into` react state and lifecycle features from function components

#### Rules 
1. you must `import` hooks from react 
2. hooks can only be called `inside` react function components 
3. hooks can be called at the top level of a component 
4. hooks cannot be conditional


#### First Hook: useState 

```javascript 
const [count, setCount] = useState(0);
// state variable, upadting/updated function, 0 -> initial value 
```

useState hook or function returns an array with two elements 
destructing the array 

name could be anything

1. count => a state variable which stores the current value.
2. setCount => a method or function which helps in updating the current state of count variable. 

example: 
```javascript
import React, { useState } from "react";
import styled from "styled-components";
import { BiPlusMedical } from "react-icons/bi";
import { FaMinus } from "react-icons/fa";

const UseState = () => {
  const [count, setCount] = useState(0);

  return (
    <>
      <Wrapper>
        <div className="container">
          <button onClick={() => setCount(count + 1)}>
            <BiPlusMedical className="icon" />
          </button>
          <h1>{count}</h1>
          <button
            onClick={() => (count === 0 ? setCount(0) : setCount(count - 1))}>
            <FaMinus className="icon minus_icon" />
          </button>
        </div>
      </Wrapper>
    </>
  );
};
// count === 0 ? setCount(0) : setCount(count-1)

// ternary operator => condition ? (if condition true) : (if condition false)
// here we setting the value of count as 0. If the value of count is 0, it will remain 0 only, aur agar nhi hai toh minus kr denge.

const Wrapper = styled.section`
  .container {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 4.8rem;
  }
  .icon {
    font-size: 2rem;
  }

  h1 {
    font-size: 5.4rem;
    color: #2e86c1;
  }
`;

export default UseState;
```


#### Building Basic form using useState

```javascript 
import React, { useState } from "react";
import styled from "styled-components";

const UseStateObject = () => {
  const [formData, setFormData] = useState({
    username: "",
    email: "",
    password: "",
    confirm_password: "",
  });

  const handleInput = (event) => {
    const name = event.target.name;

    const value = event.target.value;

    setFormData((prev) => {
      return { ...prev, [name]: value };
      // spread operator 
      // maintaing the previous value of object
      // agr hum koi ek field change krenge toh vahi particular field change hogi instead of all the fields. 
    
    });
  };

  return (
    <Wrapper>
      <div className="container">
        <div className="card">
          <h2 className="card-title text-center">Register</h2>
          <div className="card-body py-md-4">
            <form>
              <div className="form-group">
                <input
                  type="text"
                  className="form-control"
                  id="name"
                  name="username"
                  placeholder="Name"
                  autoComplete="off"
                  value={formData.username}
                  onChange={handleInput}
                />
              </div>
              <div className="form-group">
                <input
                  type="email"
                  className="form-control"
                  id="email"
                  name="email"
                  autoComplete="off"
                  placeholder="Email"
                  value={formData.email}
                  onChange={handleInput}
                />
              </div>

              <div className="form-group">
                <input
                  type="password"
                  className="form-control"
                  id="password"
                  name="password"
                  placeholder="Password"
                  autoComplete="off"
                  value={formData.password}
                  onChange={handleInput}
                />
              </div>
              <div className="form-group">
                <input
                  type="password"
                  className="form-control"
                  id="confirm-password"
                  name="confirm_password"
                  placeholder="confirm-password"
                  autoComplete="off"
                  value={formData.confirm_password}
                  onChange={handleInput}
                />
              </div>
              <div className="d-flex flex-row align-items-center justify-content-between">
                <button className="btn btn-primary">Create Account</button>
              </div>
            </form>
            <div>
              <p>{`My name is ${formData.username} and email is ${formData.email}`}</p>
            </div>
          </div>
        </div>
      </div>
    </Wrapper>
  );
};

const Wrapper = styled.section`
  .container {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  h2 {
    font-size: 2.4rem;
    margin: 3.2rem 0;
  }
  a {
    color: #333;
  }
  a:hover {
    color: #da5767;
    text-decoration: none;
  }
  .card {
    border: 0.1rem solid #f8f9fa;
    padding: 0 3.2rem;
  }

  form {
    display: flex;
    flex-direction: column;
    gap: 1.2rem;
  }

  .form-control:focus {
    color: #000000;
    background-color: #ffffff;
    border: inset 0.5rem solid #da5767;
    outline: 0;
    box-shadow: none;
  }

  input {
    width: 25rem;
    padding: 1rem 2rem;
    font-family: "Work Sans", sans-serif;
    outline: 0;
    border: none;
    font-size: 1.2rem;
  }

  .btn {
    padding: 0.6rem 1.2rem;
    background-color: #df8c96;
    border-color: #df8c96;
    margin-bottom: 3.2rem;
  }

  .btn-primary:hover {
    background: #da5767;
    border: inset 0.2rem solid #da5767;
    transition: 0.3s;
  }
`;

export default UseStateObject;
```

#### Second Hook: useEffect hook 

it helps us to perform side effects in function components. 

side effects => koi bhi operation perform krna ho depending on something.

for example: data fetching, manually changing the DOM in react. 

> it accepts two parameters
> 1. callback function -> where we write side effect code
> 2. dependency array (it could be set empty)

dependency array  is responsible for calling the callback function i.e. on the change of the value inside the array,  the callback function will be executed.

in the code given below, count state variable is stored in dependency array. 
as the value of count changes, it will update title of the web page. 

and if we want to run useeffect callback function for the first time only (when page renders for the first time), we will keep the array as empty  

1. no dependency passed => runs on every render i.e. every time the value of mentioned variable changes, it will pass execute.
2. an empty array => runs on first render 
3. props or state values => runs on first render and any time dependency value changes.

```javascript 
useEffect(()=>{
	// first time will run 
}, []);

useEffect(()=>{
	// then this will run 
}, []);

useEffect(()=>{
	// and then this will run 
}, []);
```


```javascript
import React, { useState, useEffect } from "react";
import styled from "styled-components";
import { BiPlusMedical } from "react-icons/bi";
import { FaMinus } from "react-icons/fa";

const UseEffect = () => {
  const [count, setCount] = useState(0);

  const countUpdate = (val) => {
    if (val === "inc") return setCount(count + 1);
    if (val === "dec") return setCount(count - 1);
  };

  useEffect(() => {
    document.title = count;
  }, [count]);

  return (
    <>
      <Wrapper>
        <div className="container">
          <button onClick={() => countUpdate("inc")}>
            <BiPlusMedical className="icon" />
          </button>
          <h1>{count}</h1>
          <button onClick={() => countUpdate("dec")}>
            <FaMinus className="icon minus_icon" />
          </button>
        </div>
      </Wrapper>
    </>
  );
};

const Wrapper = styled.section`
  .container {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 4.8rem;
  }
  .icon {
    font-size: 2rem;
  }

  h1 {
    font-size: 5.4rem;
    color: #2e86c1;
  }
`;

export default UseEffect;
```


cleanup function 

	cleans up the data that was created because of useEffect   

```javascript
import React, { useState, useEffect } from "react";
import styled from "styled-components";

const ClearUp = () => {
  const [widthCount, setWidthCount] = useState(window.screen.width);

  const currentScreenWidth = () => {
    setWidthCount(() => window.innerWidth);
  };

  useEffect(() => {
    window.addEventListener("resize", currentScreenWidth);
    return () => {
      window.removeEventListener("resize", currentScreenWidth);
    };
  });
  return (
    <Wrapper>
      <div className="container">
        <h2>
          The size of the window is <span> {widthCount} </span>
        </h2>
      </div>
    </Wrapper>
  );
};
ClearUp;
const Wrapper = styled.section`
  .container {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  h2 {
    line-height: 5.2rem;
    font-size: 4.2rem;
  }
  span {
    color: #2e86c1;
  }
`;

export default ClearUp;
```



#### Third Hook: useContext Hook 

to manage state globally. 

> [! Props Drilling]

when the  grand parent component passes the data (which is required to child or grand child ) to every single parent then child then grand child, it is known as props drilling 

useContext hook deals with this only.
instead of passing the data to everyone, it creates a global space where the data can be stored and this data is accessible to everyone (conditionally).

![[Pasted image 20240831124925.png]]


useContext uses context api 

inside the context api we have providers and consumers 

providers is responsible for providing the data and consumers is responsible for consuming the data.


steps for context creation 

1. create a new folder with the name `context` or `usecontext` 
2. inside that folder, create a new file named as userContext.jsx (or anything )


```javascript 
// userContext.js 

// context 
// provider 
// useContext 

// please note that context and useContext are two differen things. 
// useContext should be used inside the context only.

import { createContext, useContext } from "react";

const AppContext = createContext();

const AppProvider = ({ children }) => {
  const userData = {
    name: "vinod",
    age: 28,
  };

  return <AppContext.Provider value={userData}>{children}</AppContext.Provider>;
  // app component would be children to this component,
};

// custom hook
const useGlobalContext = () => {
  return useContext(AppContext);
};

export { AppContext, AppProvider, useGlobalContext };
```


```javascript
child.jsx
import React from "react";
import { useGlobalContext } from "./components/usecontext/userContext";

const Child = () => {
  // const { name, age } = user;
  const userData = useGlobalContext();
  // console.log("🚀 ~ file: Child.jsx ~ line 8 ~ Child ~ userData", userData);

  return (
    <div>
      Child = My name is {userData.name} and my age is {userData.age}.{" "}
    </div>
  );
};

export default Child;
```



#### Use Reducer hook

use reducer is same as use state hook but it is efficient and powerful.
manages the states 
> syntax: useReducer(reducer, initial_val);

use reducer hook returns an array with two elements
reducer is the function and initial_val is the variable

reducer function takes two parameter, state and action   

> const [state, dispatch] = useReducer(reducer, initial_val);

reducer is the function.

whenever we have a button or anything which is repsonsible for the change of state, first we have to mention the type inside the dispatch, this dispatch will call the reducer function which will finally call the user defined function.

general the reducer function are defined in reducer.jsx (convention)




```javascript 
import { useReducer } from "react";
import styled from "styled-components";
import { BiPlusMedical } from "react-icons/bi";
import { FaMinus } from "react-icons/fa";
import reducer from "./reducer";

const initialValue = 0;

const ReducerHook = () => {
  const [count, setCount] = useState(0);
  return (
    <>
      <Wrapper>
        <div className="container">
          <button onClick={() => dispatch({ type: "INC" })}>
            <BiPlusMedical className="icon" />
          </button>
          <h1>{count}</h1>
          <button onClick={() => dispatch({ type: "DEC" })}>
            <FaMinus className="icon minus_icon" />
          </button>
        </div>
      </Wrapper>
    </>
  );
};

const Wrapper = styled.section`
  .container {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 4.8rem;
  }
  .icon {
    font-size: 2rem;
  }

  h1 {
    font-size: 5.4rem;
    color: #2e86c1;
  }
`;

export default ReducerHook;
```


```javascript 
const reducer = (state, action)=>{
	if(action.type === "INC"){
		return (state = state + 1);
	}
	if(action.type === "DEC"){
		return (state = state - 1);
	}

	return state; 
}
export default reducer;
```



#### Fifth hook  use ref

1. creates a mutable variable which will not re-render the components 
2. used to access the DOM elements directly. 
3. use state and use effect re-renders the entire page.  
4. use ref hook returns an object with a property as cur.rent.
- **Mutable Reference**: `useRef` creates a mutable variable that will not cause the component to re-render when updated. It's useful for storing a value that changes without needing to trigger a re-render.
    
- **Access to DOM Elements**: `useRef` is often used to directly access a DOM element. For example, if you want to focus an input field programmatically, you can use `useRef` to get the reference to the input element and manipulate it.
    
- **No Re-render**: Unlike `useState` or `useEffect`, updating a `useRef` value does not trigger a re-render of the component. This makes `useRef` efficient when you need to keep track of information but do not want the component to re-render unnecessarily.

```javascript

import React, { useRef } from 'react';

function TextInputWithFocusButton() {
  const inputRef = useRef(null);

  const handleClick = () => {
    // Access the DOM node directly to focus
    inputRef.current.focus();
  };

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={handleClick}>Focus the input</button>
    </div>
  );
}

export default TextInputWithFocusButton;

```

.In this example:

- We use `useRef` to create a reference to the `<input>` element.
- The `handleClick` function uses `inputRef.current` to directly access the input element and call the `focus()` method on it.

#### Common Use Cases of `useRef`

1. **Accessing Child Components or DOM Elements**: Accessing the properties or methods of a child component or a DOM element.
2. **Storing Previous Values**: Storing the previous value of a prop or state without triggering a re-render.
3. **Tracking Intervals or Timers**: Keeping track of `setInterval` or `setTimeout` IDs so they can be cleared later without triggering a re-render.


```javascript 
// it create a mutable variable which will not re-render the components
// Used to access the DOM element directly

import React, { useState, useEffect, useRef } from "react";
import styled from "styled-components";

const RefHook1 = () => {
  const [userInput, setUserInput] = useState("");
  // const [count, setCount] = useState();
  const count = useRef(0);
  // console.log("🚀 ~ file: RefHook1.jsx ~ line 11 ~ RefHook1 ~ count", count);

  useEffect(() => {
    // setCount(count + 1);
    count.current = count.current + 1;
  });

  return (
    <Wrapper>
      <input
        type="text"
        value={userInput}
        onChange={(e) => setUserInput(e.target.value)}
      />

      <p>the number of times comp render:{count.current} </p>
    </Wrapper>
  );
};

const Wrapper = styled.section`
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  font-size: 2.4rem;

  input {
    min-width: 20rem;
    /* padding: 1rem 0.5rem; */
    color: #000;
    font-size: 2rem;
  }
`;

export default RefHook1;

```



#### sixth hook: use layout effect 

1. we try to avoid using this instead we use use effect
2. use effect runs asynchronously where it runs synchronously.
3. the value is updated even before the screen is updated. 
4. only advantage: sabse phele uselayouteffect hi chalega even before useEffect 


```javascript 
useEffect(()=>{
	// this will run after useLayoutEffect
}, []);
useLayoutEffect(()=>{
	// this will run first 
}, [])
useEffect(()=>{
	// this sill run after useLayoutEffect and useEffect
}, []);
```




#### seventh Hook: use memo hook 

same as use effect hook 

> syntax: const [var_name] = useMemo(callback, [dependency]);

note: it returns a memorized value.
with the help of callback function, we can return the value.
it increase the performance 

consider memoization as caching a value so that it does not need to be recalculated 

the useMemo hook only runs when one of its dependencies update. 
it can be used to keep expensive, resource intensive functions from needlessly running. 

```javascript
import React, { useState, useMemo } from "react";
import styled from "styled-components";

const MemoHook = () => {
  const [myNum, setMyNum] = useState(0);
  const [show, setShow] = useState(false);

  const getValue = () => {
    return setMyNum(myNum + 1);
  };

  const countNumber = (num) => {
    // console.log("🚀 ~ file: Memo.jsx ~ line 12 ~ countNumber ~ num", num);
    for (let i = 0; i <= 1000000000; i++) {}
    return num;
  };

  const CheckData = useMemo(() => {
    return countNumber(myNum);
  }, [myNum]);

  return (
    <Wrapper>
      <button onClick={getValue} style={{ backgroundColor: "red" }}>
        Counter
      </button>
      <p> My new number : {CheckData} </p>
      <button onClick={() => setShow(!show)}>
        {show ? "You clicked me" : "Click me plz"}
      </button>
    </Wrapper>
  );
};

const Wrapper = styled.section`
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  font-size: 2.4rem;
`;

export default MemoHook;
```


#### eight hook: usecallback hook 

> it is also used to increase the performance of the react application;
> it returns a memorized function.



### 9. **Custom Hooks**

- **Description**: Custom hooks in React allow you to extract and reuse stateful logic across multiple components. They are JavaScript functions that can call other hooks.
- **Use Cases**: Any time you have logic that is used in more than one component (e.g., fetching data, handling forms, or managing timers).
- **Example**: A custom hook to handle form input:

```javascript
function useForm(initialValues) {
  const [values, setValues] = useState(initialValues);

  const handleChange = (event) => {
    setValues({
      ...values,
      [event.target.name]: event.target.value,
    });
  };

  return [values, handleChange];
}

```

### **Memoization (`React.memo`, `useMemo`, `useCallback`)**
.
- **Description**: Memoization is an optimization technique to prevent unnecessary recalculations or re-renders.
    - **`React.memo`**: A higher-order component that memoizes the output of a function component.
    - **`useMemo`**: A hook that memoizes the result of a function.
    - **`useCallback`**: A hook that memoizes a callback function.
- **Use Cases**:
    - **`React.memo`**: Used for functional components to avoid re-rendering when props haven’t changed.
    - **`useMemo`**: Used for heavy computations that don't need to be recalculated unless dependencies change.
    - **`useCallback`**: Used to memoize functions passed down to child components to prevent unnecessary re-renders.
- **Example**:
```
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
const memoizedCallback = useCallback(() => handleClick(a, b), [a, b]);

```


 

### **Forwarding Refs (`React.forwardRef`)**

- **Description**: Allows a component to forward a ref to a child component or a DOM element. It’s useful when a parent component needs to directly interact with a child’s DOM node.
- **Use Cases**: Useful for managing focus, animations, or integrating with third-party DOM libraries.
- **Example**:
    
```javascript
const FancyButton = React.forwardRef((props, ref) => (
  <button ref={ref} className="FancyButton">
   {props.children}
  </button>
));

```
    

### **Error Boundaries**

- **Description**: Error boundaries are React components that catch JavaScript errors in their child component tree, log those errors, and display a fallback UI.
- **Use Cases**: Use when you want to provide a user-friendly error message and prevent the entire app from crashing.

```javascript
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  render() {
    if (this.state.hasError) {
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children; 
.  }
}

```
### **Portals**

- **Description**: Portals provide a way to render children into a DOM node that exists outside the hierarchy of the parent component.
- **Use Cases**: Useful for creating modals, tooltips, dropdowns, or any component that needs to visually break out of its container.
- **Example**:
    
    javascript
    
    Copy code
    
    `const modalRoot = document.getElementById('modal-root');  function Modal({ children }) {   return ReactDOM.createPortal(     children,     modalRoot   ); }`
    

###  **React Context API (Advanced Usage)**

- **Description**: React Context API is used for managing global state or passing data deeply throughout a component tree without having to pass props down manually at every level.
- **Advanced Usage**:
    - Memoizing context values to avoid unnecessary renders.
    - Splitting context to prevent unnecessary re-renders.
- **Use Cases**: Great for global state management, theming, localization, and handling user authentication.
- **Example**:
    
    javascript
    
    Copy code
    
    `const MyContext = React.createContext();  function MyProvider({ children }) {   const [state, setState] = useState({});   const value = useMemo(() => ({ state, setState }), [state]);    return <MyContext.Provider value={value}>{children}</MyContext.Provider>; }`
    

###  **Concurrent Mode (Experimental)**

- **Description**: Concurrent Mode is an experimental set of features that help React apps stay responsive and gracefully adjust to the user's device capabilities and network speed.
- **Features**:
    - **Automatic batching**: Handles multiple state updates in one re-render.
    - **Transitions**: Allows marking UI updates as non-urgent, making apps feel more responsive.
- **Use Cases**: Ideal for creating apps that need to be highly responsive, like real-time data dashboards or complex interactive UI.
- **Example**: `useTransition` is one such hook in Concurrent Mode that allows marking state updates as non-urgent.

### **React Lazy and Suspense**

- **Description**: `React.lazy()` and `Suspense` are used for code-splitting. `React.lazy()` allows you to dynamically import components, and `Suspense` lets you display a fallback UI while the component is loading.
- **Use Cases**: Improves performance by loading components only when needed.
- **Example**:
```javascript
const .LazyComponent = React.lazy(() => import('./MyComponent'));  function App() {   return (     <Suspense fallback={<div>Loading...</div>}>       <LazyComponent />     </Suspense>   ); }
```
    

### **Strict Mode**

- **Description**: `StrictMode` is a development tool that helps identify potential problems in an application. It activates additional checks and warnings for its descendants.
- **Use Cases**: Use to enforce best practices and detect possible errors like side effects in render, usage of deprecated APIs, and other warnings.
- **Example**:
```javascript

<React.StrictMode>   <App /> </React.StrictMode>
```

###  **Immutable State Management**

- **De.scription**: Ensures that state is never mutated directly; instead, a new copy of the state is created whenever changes are m.ade. Libraries like Immer provide utilities to work with immutable state in a more readable way.
- **Use Cases**: Guarantees predictable state updates, simplifies debugging, and helps React optimize rendering.
- **Example**:

```javascript
import produce from "immer";  const nextState = produce(currentState, draftState => {   draftState.property = "new value"; });`
```