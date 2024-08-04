<style>
.block {
    background-color: #f5f5f5;
    padding: 6px 10px;
    border-radius: 5px;
    box-shadow: 0 0 5px 0px grey;margin:15px 0px;
    padding-bottom: 1px;
    font-size:13px;
    transition: all 1s ease;
    overflow: hidden;
}
code {
    font-size: 12px;
}
.block2 {
    background-color: #fffae7;
    padding: 6px 10px;
    border-radius: 5px;
    box-shadow: 0 0 5px 0px grey;margin:15px 0px;
    padding-bottom: 1px;
    font-size:13px;
    color: #7c1212;
    font-weight: 600
}

.detail .long {
    display: none;
  }

  .detail:hover .short {
    display: none;
  }
  .detail:hover .long {
    display: inline;
  }

  .detail .short {
    background-color: #FFF6E9;
  }
</style>

React is a popular open-source JavaScript library used for building user interfaces, particularly single-page applications. Developed and maintained by Facebook (now Meta) and a community of individual developers and companies, React has become one of the most widely used libraries for front-end development.

React was created by Jordan Walke, a software engineer at Facebook, in 2011. It was first deployed on Facebook's news feed in 2011 and later on Instagram in 2012. React was open-sourced and publicly released at JSConf US in May 2013.

React "reacts to changes in the components"


Installation
- needs NodeJS
- recommended Chrome extension: react developer tools
- VSCode extension: es7 react/redux/graphQL/React-Native snippets
- VSCode setting: Emmet: Include Languages: javascript - javascriptreact
- VSCode extension: prettier

`npx create-react-app nameofproject`

*npx is a package runner tool that comes with npm (Node Package Manager) starting from version 5.2.0 (released in July 2017). It is designed to execute binaries from npm packages, making it easier to use CLI tools and scripts without needing to install them globally or add them as dependencies to a project.*



The main entry point is the `public/index.html` file for the browser to start with. After that React takes over.

The React work will be basically done in the `src` folder.



Start project: `npm start`



JSX (JavaScript XML) is a syntax extension for JavaScript commonly used with React to describe what the UI should look like. It allows developers to write HTML-like code within JavaScript, which is then transformed into React elements.


Concepts:
- Each component gets it's own file.
- Modern React use functional components instead of class components




Basic functional component
```javascript
import logo from './logo.svg';
import './App.css';
import Header from './Header'

function App() { // it could be an arrow function also
  const name = "NAME";

  const double = (name) => {
    return name + name; 
  }

  return (
    // 'class' is reserved
    <div className="App">
        {name + "!"} 
        {double(name)}

        <img src={logo} alt="logo" />

        <Header />
    </div>
  );
}

export default App;
```



ES7 snippet search: Command + Shift + R

example: _rafce

Entry point of React components is the index.js
```js
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
);
```
NB: it's a nice practice to not to forget about the #root element to ass some css, like expand to full page.

<div class="block">

### How to add styles?
<div class="detail">
<div class="short">

Inline, separate .css files, styled-components library
</div>
<div class="long">

Inline, sometimes it's useful
```js
import './App.css';

function App() {
  return (<div style={{
    backgroundColor: "gray"
  }}>Hello</div>);
}

export default App;
```
Or like creating a sebarate variable for it:
```js
import './App.css';

function App() {
  const myStyle = {
    backgroundColor: "gray"
  }

  return (<div style={myStyle}>Hello</div>);
}

export default App;
```

Generally you can have a .css file named the same way as the component.

```javascript
import './App.css';

function App() {
  return (<div className="App">Hello</div>);
}

export default App;
```

Keep in mind that if you import two different CSS files into separate components, CSS class names can interfere with each other if they have the same name. This is because CSS in traditional stylesheets is global by default. When two CSS classes have the same name, the styles defined in the CSS files can potentially conflict, leading to unexpected styling results.

Solution 1:  
CSS Modules locally scope CSS by automatically generating unique class names. This prevents class name conflicts. To use CSS Modules, rename your CSS files to ComponentA.module.css and ComponentB.module.css.

```js
import React from 'react';
import styles from './ComponentA.module.css';

function ComponentA() {
  return <div className={styles.container}>Component A</div>;
}

export default ComponentA;
```

Solution 2:
Just come up with your own naming convention

Solution 3:
styled-components library

```js
import React from 'react';
import styled from 'styled-components';

const Container = styled.div`
  background-color: red;
`;

function ComponentA() {
  return <Container>Component A</Container>;
}

export default ComponentA;
```
</div>
</div>




</div>





<div class="block">
<div class="detail">
<div class="short">
NB: As of React 17 and later, the `import React from 'react';` line is not strictly necessary
</div>
<div class="long">

NB: As of React 17 and later, the `import React from 'react';` line is not strictly necessary in many cases due to the new JSX Transform introduced by React. However, understanding when it's necessary and when it's not is important for maintaining compatibility and understanding your codebase.

Prior to React 17, JSX code needed the React import because JSX is syntactic sugar for React.createElement calls. For example:  
`const element = <h1>Hello, world!</h1>;`  
would be transformed into:  
`const element = React.createElement('h1', null, 'Hello, world!');`  
Because of this transformation, the React object needed to be in scope, so the import was required.

To ensure compatibility:
- Ensure your project is using React 17 or later.
- Make sure your Babel configuration is set up to use the new JSX Transform. This is often handled automatically by tools like Create React App, but if you are configuring Babel manually, it should look like this:
```js
// babel.config.js or .babelrc
module.exports = {
  presets: [
    ['@babel/preset-env', { targets: "defaults" }],
    ['@babel/preset-react', { runtime: 'automatic' }],
  ],
};
```
</div>
</div>
</div>




```js
const Content = () => {
    const handleClick = (txt = "YEAY") => {
        console.log(`You clicked it: ${txt}`)
    }

    const handleEvent = (event) => {
        console.log(event)
    }

    return (
        <button onClick={handleClick}>Click me1</button>
        <button onClick={() => handleClick('YEAP')}>Click me2</button>
        <button onClick={(event) => handleEvent(e)}>Click me3</button>
    )
}

export default Content
```




### useState
```js
import { useState } from 'react';

const Content = () => {
    const [name, setName] = useState('default');
    const [count, setCount] = useState(0);

    function handleClick() {
        setName("Dave")
    }

    function increment() {    // first round count == 0
        setCount(count + 1)   // 0+1
        setCount(count + 1)   // 0+1
        console.log(count)    // 0
    }

    return (
        <button onClick={handleClick}>Change</button>
        <button onClick={increment}>Increment</button>
        {name}
        {count}
    )
}

export default Content
```

In React, when you use the useState hook to manage state, the setter function returned by useState can accept either a new state value or a function that takes the previous state and returns the new state. This function-based approach is particularly useful when the new state depends on the previous state.

When you call the setter function with a function, React ensures that you are working with the most up-to-date state. This is important in scenarios where state updates might be batched or when multiple updates might happen in quick succession.

```js
const handleChange = (event) => {
  const { name, value } = event.target;
  setFormData({
    ...formData, // this could be stale
    [name]: value
  });
};
```

If multiple handleChange events happen quickly, formData might be stale when the state update happens, leading to unexpected results.

```js
const handleChange = (event) => {
  const { name, value } = event.target;
  setFormData((prevData) => ({
    ...prevData,
    [name]: value
  }));
};
```

Performance Optimization: React may batch state updates for performance reasons. Using the function form avoids potential pitfalls associated with these optimizations.

Predictable State Updates: Ensures that state updates are predictable and consistent, reducing bugs related to stale state.


### Lists, keys
package: react-icons `npm i react-icons`

```js
import { useState } from 'react';
import { FaTrashAlt } from 'react-icons/fa';

const Content = () => {
    const [items, setItems] = useState([
        { id: 1, checked: false, txt: "txt1" },
        { id: 2, checked: false, txt: "txt2" },
        { id: 3, checked: false, txt: "txt3" }
    ]);

    function handleCheck(id) {
        const listItems = items.map(item => {
            return item.id == id ? { ...item, checked: !item.checked } : item
        })

        setItems(listItems);
        localStorage.setItem('shoppinglist', JSON.stringify(listItems))
    }

    function handleDelete(id) {
        const listItems = items.filter(item => item.id != id)

        setItems(listItems);
        localStorage.setItem('shoppinglist', JSON.stringify(listItems))
    }

    return (
        <div>
            {items.length ? (
                <ul>
                    {items.map((item, index) => {
                        return (<li key={item.id}>
                                    <input
                                        type="checkbox"
                                        onChange={() => handleCheck(item.id)}
                                        checked={item.checked}
                                        id={`field${item.id}`}
                                        />
                                    <label htmlFor={`field${item.id}`}>{item.txt}</label>
                                    <FaTrashAlt
                                        role="button"
                                        tabIndex="0"
                                        onClick={() => handleDelete(item.id)}
                                        />
                                </li>)
                    })}
                </ul>
            ) : "No items"}
        </div>
    )
}

export default Content;
```



<div class="block">
<div class="detail">
<div class="short">

**localStorage** is a web storage API provided by modern web browsers that allows developers to store key-value pairs in a web application. This data is stored in the user's browser and persists even after the browser is closed and reopened.
</div>
<div class="long">

**localStorage** is a web storage API provided by modern web browsers that allows developers to store key-value pairs in a web application. This data is stored in the user's browser and persists even after the browser is closed and reopened.

- Persistence: Data stored in localStorage persists across browser sessions. This means that if a user closes their browser or navigates away from the page, the data will still be available the next time they visit the site.
- Storage Limit: The storage limit for localStorage is usually around 5MB per origin (domain). This is significantly larger than the storage available with cookies.
- Scope: Data stored in localStorage is scoped to the protocol (HTTP or HTTPS), domain, and port. This means data stored in http://example.com is not accessible from https://example.com or http://sub.example.com.
- Synchronous API: The localStorage API is synchronous, meaning it can block the main thread, which might impact performance if used excessively.

```js
localStorage.setItem('key', 'value');
const value = localStorage.getItem('key');

localStorage.removeItem('key');

localStorage.clear(); // Clearing All Data

const numberOfItems = localStorage.length; // get the number of items stored 

// Iterating Over All Items
for (let i = 0; i < localStorage.length; i++) {
  const key = localStorage.key(i);
  const value = localStorage.getItem(key);
  console.log(`${key}: ${value}`);
}
```

Use Cases
- Storing User Preferences: For example, theme settings (dark mode/light mode), language preferences, etc.
- Caching Data: Storing data that doesn’t change frequently to avoid unnecessary network requests.
- Shopping Cart: Keeping track of items in a user's shopping cart.
- Form Data: Saving form data so that it can be recovered if the user accidentally refreshes the page or closes the browser.

Security Considerations
- Sensitive Data: Avoid storing sensitive information like passwords, credit card numbers, or personal data in localStorage, as it is accessible from JavaScript and can be exploited if there's an XSS vulnerability.
- Storage Size: Be mindful of the storage limits and avoid storing large amounts of data.
</div>
</div>
</div>






### Props, prop drilling

```js
import { useState } from 'react';
import Header from './Header'

function App() {
  const [items, setItems] = useState([{}, {}, {}])

    function handleCheck(id) {
        const listItems = items.map(item => {
            return item.id == id ? { ...item, checked: !item.checked } : item
        })

        setItems(listItems);
        localStorage.setItem('shoppinglist', JSON.stringify(listItems))
    }

    function handleDelete(id) {
        const listItems = items.filter(item => item.id != id)

        setItems(listItems);
        localStorage.setItem('shoppinglist', JSON.stringify(listItems))
    }

  return (
    <div>
        <Header title="Title"/>
        <Content
            items={items}
            handleCheck={handleCheck}
            handleDelete={handleDelete}
            />
    </div>
  );
}

export default App;
```

How to access props (2 way), set up default props (2 way)
```js
// function Header(props) {
function Header({ title = "default"}) { // destructure, give default value here is preferred

  return (
    <div>
        {/* {props.title} */}
        {title}
    </div>
  );
}

// set up default props
Header.defaultProps = {
    title: "default"
}

export default Header;
```

```js
import { FaTrashAlt } from 'react-icons/fa';

const Content = ({items, handleCheck, handleDelete}) => {

    return (
        <div>
            {items.length ? (
                <ul>
                    {/* could make a component from here */}
                    {items.map((item, index) => {
                        // or/and could make a separate component of this below
                        return (<li key={item.id}>
                                    <input
                                        type="checkbox"
                                        onChange={() => handleCheck(item.id)}
                                        checked={item.checked}
                                        id={`field${item.id}`}
                                        />
                                    <label htmlFor={`field${item.id}`}>{item.txt}</label>
                                    <FaTrashAlt
                                        role="button"
                                        tabIndex="0"
                                        aria-label={`Delete ${item.txt}`}
                                        onClick={() => handleDelete(item.id)}
                                        />
                                </li>)
                    })}
                </ul>
            ) : "No items"}
        </div>
    )
}

export default Content;
```

### Controlled component inputs

In React, a "Controlled Component" refers to an input element (such as a `<input>`, `<textarea>`, or `<select>`) that is controlled by React state. This means that the value of the input element is set by the state of the component, and any changes to the input are handled by event listeners that update the state.

```js
import { useState } from 'react';
import Header from './Header';
import AddItem from './AddItem';

function App() {
  // should handle if localStorage is not set before..
  // the logical OR operator || is used to provide a default value when the first operand evaluates to a falsy value.
  const [items, setItems] = useState(JSON.parse(localStorage.getItem('shoppinglist')) || [])
  const [newItem, setNewItem] = useState('')

  function handleCheck(id) {...}
  function handleDelete(id) {...}

  function handleSubmit(event) {
      if (!newItem) return;

    // as on submit the page reloads, we should stop this behaviour
    event.preventDefault();
    
    addItem(newItem);
    setNewItem('');
  }

  function addItem(txt) {
    const id = items.length ? items[items.length - 1].id + 1 : 1;
    const myNewItem = {
        id,
        checked: false,
        txt
    };

    const listItems = [...items, myNewItem];
    setItems(listItems);
    localStorage.setItem('shoppinglist', JSON.stringify(listItems));
  }

//   useEffect(() => {
//     localStorage.setItem('shoppinglist', JSON.stringify(listItems));
//   }, [items]) // sets first time to [], and don't have to handle in other functions

  return (
    <div>
        <Header title="Title"/>
        <Content
            items={items}
            handleCheck={handleCheck}
            handleDelete={handleDelete}
            />
        <AddItem
            newItem={newItem}
            setNewItem={setNewItem}
            handleSubmit={handleSubmit}
            />
    </div>
  );
}

export default App;
```

When we added a new item, the button remained in focus, and we should move back the focus to the input.
```js
import { useRef } from 'react'
import { FaPlus } from 'react-icons/fa'

const AddItem = ({ newItem, setNewItem, handleSubmit }) => {
    const inputRef = useRef();

    return (
        <form onSubmit={handleSubmit} > // here the event is implicitly passed
            <label htmlFor='addItem'>Add Item</label>
            <input
                autoFocus
                ref={inputRef}

                id='addItem'
                type='text'
                placeholder='Add Item'
                required
                {/* here's the main logic */}
                value={newItem}
                onChange={event => setNewItem(e.target.value)}
            />
            <button
                type='submit'
                aria-label='Add Item'
                {/* here's the change to handle the focus */}
                onClick={() => inputRef.current.focus()}
            >
                <FaPlus />
            </button>
        </form>
    )
}

export default AddItem
```

<div class="block">
<div class="detail">
<div class="short">

Using the `<form>` tags in React is generally useful.
</div>
<div class="long">

Wrapping inputs in `<form>` tags in React is generally useful, especially for organizing and handling form submissions.

- Forms provide a built-in way to handle submission events with the onSubmit attribute. This makes it easy to collect and process all the input data in one place.
- Forms allow users to submit by pressing Enter, which improves accessibility and user experience. This behavior is especially important for accessibility and for users who rely on keyboard navigation.
- Wrapping related inputs in a form provides semantic meaning and groups them logically. This helps maintain a clear structure and makes the code easier to understand.
- Forms support HTML5 validation attributes like required, pattern, min, max, etc., which provide a way to enforce input constraints before submission.
</div>
</div>
</div>



### useEffect

In React, the useEffect hook allows you to perform side effects in function components. Understanding when and why the function provided to useEffect runs involves understanding the dependencies array and the component lifecycle.

The useEffect hook takes two arguments:
- A function that contains the side-effect logic.
- An optional array of dependencies.

Initial Render: The effect function always runs after the initial render. The rest is a bit more troublesome.

And in general, the function passed to useEffect runs AFTER the render phase. 
___
Everytime the component renders, the function given in the useEffect runs too.
```js
useEffect(() => {
    // everytime
})
```

But we can add dependencies also in order to have a condition when to run it.
```js
useEffect(() => {
    // only load time
}, [])
```
Basically it runs if the given dependencies change. Which means, no dependency, no change.
```js
const [items, setItems] = useState([])

useEffect(() => {
    // when items change
}, [items])
```
___
Let's discuss the order of the execution.
```js
console.log("before")

useEffect(() => {
    console.log("inside")
})

console.log("after")

// results: before, after, inside
```

___
NB: when you have multiple useEffect hooks within the same component, they will run in the order in which they are defined in the component. Each useEffect will execute after the render phase but before the browser updates the screen.
___
The useEffect hook itself cannot be made async because the function passed to useEffect must return either nothing (undefined) or a cleanup function, and async functions return promises, which cannot be directly used for cleanup in React.

However, you can define an async function inside the useEffect and call it. Here’s how you can handle asynchronous logic within a useEffect hook:

```javascript
// Define an async function
const fetchData = async () => {
    try {
    const response = await fetch('https://api.example.com/data');
    const result = await response.json();
    setData(result);
    } catch (error) {
    console.error('Error fetching data:', error);
    }
};

useEffect(() => {
    // Call the async function
    fetchData();
}, []);
```
___
The return part of the useEffect hook is used for cleanup. This cleanup function is crucial for managing side effects and avoiding memory leaks or unintended behaviors in your React components.

```js
import React, { useState, useEffect } from 'react';

const TimerComponent = () => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    // Set up a timer
    const interval = setInterval(() => {
      setCount((prevCount) => prevCount + 1);
    }, 1000);

    // Cleanup function to clear the timer
    return () => {
      clearInterval(interval);
    };
  }, []); // Empty dependency array means this effect runs once after initial render

  return (
    <div>
      <p>Count: {count}</p>
    </div>
  );
};

export default TimerComponent;
```

```js
import React, { useEffect } from 'react';

const EventListenerComponent = () => {
  useEffect(() => {
    const handleResize = () => {
      console.log('Window resized');
    };

    // Add the event listener
    window.addEventListener('resize', handleResize);

    // Cleanup function to remove the event listener
    return () => {
      window.removeEventListener('resize', handleResize);
    };
  }, []); // Empty dependency array means this effect runs once after initial render

  return (
    <div>
      <p>Resize the window to see the effect</p>
    </div>
  );
};

export default EventListenerComponent;
```
___
When you use useEffect with dependencies, the effect runs initially after the component mounts and then again whenever one of the dependencies changes. If you have a cleanup function, it will run before the effect re-runs due to a dependency change, as well as when the component unmounts.

Example with a Dependency

Let's create a component that sets up an interval to update a count every second, and the interval's behavior depends on a prop. When the prop changes, the effect should clean up the previous interval and set up a new one.

```js
import React, { useState, useEffect } from 'react';

const IntervalComponent = ({ delay }) => {
  const [count, setCount] = useState(0);

  useEffect(() => {
    // Set up the interval
    const interval = setInterval(() => {
      setCount((prevCount) => prevCount + 1);
    }, delay);

    // Cleanup function to clear the interval
    return () => {
      clearInterval(interval);
    };
  }, [delay]); // Effect depends on 'delay'

  return (
    <div>
      <p>Count: {count}</p>
      <p>Delay: {delay}ms</p>
    </div>
  );
};

export default IntervalComponent;
```
___
Let's not create an endless loop
```js
const [items, setItems] = useState([])

useEffect(() => {
    setItems([])
}, [items])
```
___
NB: In class components use componentDidUpdate to perform actions based on changes in props or state.



### JSON server
Lunch a development API

`npm i json-server` or could do it on the go `npx json-server`

a "data" folder on the root level of the project can be created to be used

with a file called db.json

Then to run a server: `npx json-server -p 3500 -w data/db.json`



We can also use POST and DELETE requests like:

`curl -X POST http://localhost:3000/posts -H "Content-Type: application/json" -d '{"title": "New Post"}'`

```js
fetch('http://localhost:3000/posts', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ title: 'New Post' })
})
.then(response => response.json())
.then(data => console.log(data));
```


`curl -X DELETE http://localhost:3000/posts/1`

```js
fetch('http://localhost:3000/posts/1', {
  method: 'DELETE'
})
.then(response => response.json())
.then(data => console.log(data));
```


### Fetch API

Let's get the data.
```js
import { useState } from 'react';
import Header from './Header';
import AddItem from './AddItem';

function App() {
  const API_URL = 'http://localhost:3500/items';
  const [items, setItems] = useState([]); // change to simple list, no localStorage needed
  const [newItem, setNewItem] = useState('');
  const [fetchError, setFetchError] = useState(null);
  const [isLoading, setIsLoading] = useState(true);

  // load data from api
  useEffect(() => {
    async function fetchItems() {
        try {
            const response = await fetch(API_URL);   // Response object is returned
            // The Response object from fetch contains the raw response data, including status, headers, and body
            if (!response.ok) {
                throw Error("Did not received expected data")
            }

            const listItems = await response.json(); // reads the response body and parses it as JSON
            setItems(listItems);
        } catch (error) {
            // Network Errors
            // Response Errors: If the response.ok property is false, it indicates that the request was not successful
            // JSON Parsing Errors: If the response body cannot be parsed as JSON
            console.log(error.stack)
            setFetchError(error.message)
        } finally {
            setIsLoading(false);
        }
    }

    fetchItems(); // no need to await the run, as no return is expected
  }, [])

  function handleCheck(id) {...}
  function handleDelete(id) {...}
  function handleSubmit(event) {...}
  function addItem(txt) {...}

  return (
    <div>
        <Header title="Title"/>
        <AddItem
            newItem={newItem}
            setNewItem={setNewItem}
            handleSubmit={handleSubmit}
            />
        {isLoading && <p>Loading items...</p>}
        {fetchError && <p>{`Error: ${fetchError}`}</p>}
        {!isLoading && !fetchError && <Content
            items={items}
            handleCheck={handleCheck}
            handleDelete={handleDelete}
            />}
    </div>
  );
}

export default App;
```

Let's separate a bit the request logic.

apiRequest.js
```js
const apiRequest = async (url = '', optionsObj = null, errMsg = null) => {
    try {
        const response = await fetch(url, optionsObj); // we will make a POST, DELETE.. request based on the optionsObj 
        if (!response.ok) {
            throw Error("Please reload the app");
        }
    } catch (error) {
        errMsg = err.message;
    } finally {
        return errMsg;
    }
}

export default apiRequest;
```

After that the App will look like

```js
import { useState } from 'react';
import Header from './Header';
import AddItem from './AddItem';

function App() {
  const API_URL = 'http://localhost:3500/items';
  const [items, setItems] = useState([]);
  const [newItem, setNewItem] = useState('');
  const [fetchError, setFetchError] = useState(null);
  const [isLoading, setIsLoading] = useState(true);

  useEffect(() => {
    async function fetchItems() {
        try {
            const response = await fetch(API_URL);
            if (!response.ok) {
                throw Error("Did not received expected data")
            }

            const listItems = await response.json();
            setItems(listItems);
        } catch (error) {
            console.log(error.stack)
            setFetchError(error.message)
        } finally {
            setIsLoading(false);
        }
    }

    fetchItems();
  }, [])

  async function handleCheck(id) {
    // ...
    const myItem = listItems.filter(item => item.id === id);

    const updateOptions = {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ checked: myItem[0].checked })
    }
    const reqUrl = `${API_URL}_${id}`;
    const result = await apiRequest(reqUrl, updateOptions);
    if (result) setFetchError(result);
  }

  async function handleDelete(id) {
    // ...
    const deleteOptions = { method: "DELETE" };
    const reqUrl = `${API_URL}_${id}`;
    const result = await apiRequest(reqUrl, deleteOptions);
    if (result) setFetchError(result);
  }

  function handleSubmit(event) {...}

  async function addItem(txt) { // had to make it async!
    const myNewItem = {...}
    // ...
    const postOptions = {
        method: 'POST',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify(myNewItem)
    };
    const result = await apiRequest(API_URL, postOptions);
    if (result) {
        setFetchError(result)
    }
  }

  return (
    <div>
        <Header title="Title"/>
        <AddItem
            newItem={newItem}
            setNewItem={setNewItem}
            handleSubmit={handleSubmit}
            />
        {isLoading && <p>Loading items...</p>}
        {fetchError && <p>{`Error: ${fetchError}`}</p>}
        {!isLoading && !fetchError && <Content
            items={items}
            handleCheck={handleCheck}
            handleDelete={handleDelete}
            />}
    </div>
  );
}

export default App;
```


### Router

`npm i react-router-dom -S`

In a React application, the Router component, typically provided by react-router-dom, is used to handle routing and navigation. The Router should be placed at a high level in your component hierarchy to ensure that all routes and navigation logic are available throughout your application.

The most common and recommended approach is to place the Router component at the top level of your application, usually in your main application component (often App.js) or in the entry point of your application (e.g., index.js). This allows all components within your application to access routing features and navigate between routes.



index.js
```js
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
import { BrowserRouter as Router, Route } from 'react-router-dom';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <Router>
      <Route path="/" component={App} />
    </Router>
  </React.StrictMode>
);

```


```js
import Header from './Header';
import Nav from './Nav';
import Footer from './Footer';
import Home from './Home';
import NewPost from './NewPost';
import PostPage from './PostPage';
import About from './About';
import Missing from './Missing';
import { Route, Switch, useHistory } from 'react-router-dom';
import { useState, useEffect } from 'react';


function App() {
  const [posts, setPosts] = useState([{}, {}, {}]);
  const history = useHistory();

  function handleDelete() {
    // ...
    history.push('/'); // this is how we can take us somewhere using some code
  }

  return (
    <div>
      <Header />
      <Nav />

      <Switch>
        <Route exact path="/">
          <Home posts={posts}/>
          {/* somewhere in there we can have a <Link to=`/post/${post.id}`>{post.title}</Link> */}
        </Route>

        <Route exact path="/post">
          <NewPost />
        </Route>

        <Route path="/post/:id">
          <PostPage posts={posts} handleDelete={handleDelete}/>
        </Route>

        <Route path="/about" component={About}/> {/* if component is simply added, use this one */}
        <Route path="*" component={Missing}/>
      </Switch>

      <Footer />
    </div>
  );
}

export default App;
```

NB: When you navigate away from ComponentA to another component (e.g., ComponentB), ComponentA is unmounted, and its local state is discarded.

```js
import { Link } from 'react-router-dom';

function Nav() {
  return (
    <nav>
      <ul>
        <li>
          <Link to="/"> Home </Link>
          <Link to="/post"> Post </Link>
          <Link to="/about"> About </Link>
        </li>
      </ul>
    </nav>
  );
}

export default Nav;
```

```js
import { useParams, Link } from 'react-router-dom';

function PostPage({ posts, handleDelete }) {
  const { id } = useParams(); // as we've used <Route path="/post/:id">
  const post = posts.find(post => (post.id).toString() === id);

  return (
    <main>

    </main>
  );
}

export default PostPage;
```

### axios

`npm i axios`


/api/posts.js
```js
import axios from 'axios';

export default axios.create({
  baseURL: 'http://localhost:3500'
})
```

When using Axios to make HTTP requests, it’s generally good practice to validate the response, even though Axios typically handles errors by rejecting the promise for non-2xx status codes. 

The response object contains:

- response.data: The actual data returned from the server (usually the payload of the response).
- response.status: The HTTP status code of the response.
- response.statusText: The HTTP status text of the response.
- response.headers: The headers of the response.
- response.config: The configuration used for the request.

```js
import api from './api/posts';

const fetchPosts = async () => {
  try {
    const response = await api.get('/posts');
    // advantage is that the response will be already parsed, no need to call .json()
    // automatically catch errors if response is not in the 200 responses, no need for if (!response.ok) {}

    // still not a bad thing to be careful
    if (response && response.data) { // could also validate the data structure
      setPosts(response.data) // so the only change is .data
    }

    // or could be differenciating between statuses
    if (response.status === 200) {}
  } catch (error) {
    if (err.response) {
      console.log(error.response.data);
      console.log(error.response.status);
      console.log(error.response.headers);
    } else {
      console.log(`Error: ${err.message}`); // didn't receive any response at all
    }
  }
}
```

```js
// ...
const response = await api.post('/posts', newPost);

await api.delete(`/posts/${id}`);

const respons = await api.put(`/posts/${id}`, updatedPost); // might get back a bit different object
setPosts(posts.map(post => post.id === id ? { ...response.data } : post)); 
// ...
```



### custom hooks
A hook function is a special type of function in React that allows you to use React state and lifecycle features in functional components. Hooks enable you to manage state, side effects, context, and more.

Rules:
- don't call hooks inside loops, conditions, or nested functions, regular functions. instead use Hooks at the top level of your React function
- only call them from React function components, or possibly call Hooks from custom Hooks

naming convention: start them with 'use'

// useWindowSize.js
```js
import { useState, useEffect } from 'react';

const useWindowSize = () => {
  const [windowSize, setWindowSize] = useState({
    width: undefined,
    height: undefined
  });

  useEffect(() => {

    const handleResize = () => {
      setWindowSize({
        width: window.innerWidth,
        height: window.innerHeight
      })
    }

    handleResize();
    window.addEventListener("resize", handleResize);

    return () => {
      window.removeEventListener("resize", handleResize);
    }
  }, [])

  return windowSize;
}

export default useWindowSize;
```

The useWindowSize hook internally manages the windowSize state. Updates to this state (e.g., when the window is resized) will trigger re-renders of the component which uses it, and during each render, width and height will reflect the latest values from useWindowSize.

NB: how to check the cleanup function actually runs. make a log in it. And as there's no dependency given, the only way to check it is in development mode, when you make a change in the code of the useWindowSize hook. tricky isn't it?

___
// useAxiosFetch.js
```js
import { useState, useEffect } from 'react';
import axios from 'axios';

const useAxiosFetch = (dataUrl) => {
  const [data, setData] = useState([]);
  const [fetchError, setFetchError] = useState(null);
  const [isLoading, setIsLoading] = useState(false);

  useEffect(() => {
    let isMounted = true;
    const source = axios.CancelToken.source();

    const fetchData = async (url) => {
      setIsLoading(true);
      try {
        const response = await axios.get(url, {
          cancelToken: source.token
        })
        if (isMounted) {
          setData(response.data);
          setFetchError(null);
        }
      } catch (error) {
        if (isMounted) {
          setFetchError(err.message);
          setData([]);
        }
      } finally {
        if (isMounted) {
          setTimeout(() => setIsLoading(false), 2000);
        }
      }
    }

    fetchData(dataUrl);

    return () => {
      isMounted = false;
      source.cancel();
    }
  }, [dataUrl])

  return { data, fetchError, isLoading };
}

export default useAxiosFetch;
```

```js
const {data, fetchError, isLoading } = useAxiosFetch('fullUrl');
// could modify it to handle any kind of request not just get

useEffect(() => {
  setPosts(data);
}, [data])
```




___
The axios.CancelToken is a mechanism provided by Axios to allow for the cancellation of requests. This is useful when you need to cancel an ongoing HTTP request, for example, when a component unmounts or when a new request is made that renders the previous request irrelevant.

axios.CancelToken.source() creates a new CancelToken source object. This source object contains a token that can be used to cancel requests and a cancel method that can be called to trigger the cancellation.

The source object has two properties:
- token: A token object to be passed to the Axios request configuration.
- cancel: A function that can be called to cancel the request.

When making a request, you can pass the token from the source object to the Axios request configuration. This token will be used to track the request and allow it to be canceled.

```js
axios.get('/some-endpoint', {
  cancelToken: source.token
})
.then(response => {
  console.log('Response:', response);
})
.catch(error => {
  if (axios.isCancel(error)) {
    console.log('Request canceled:', error.message);
  } else {
    // Handle error
  }
});
```
You can call the cancel method on the source object to cancel the request. This triggers the catch block with an error indicating that the request was canceled.
```js
source.cancel('Operation canceled by the user.');
```

NB: if you pass the same CancelToken to multiple requests, calling cancel on that token will cancel all of the requests associated with that token.


### useContext
The useContext hook is a part of React's Context API. It allows you to access the current value of a context directly within functional components. The Context API is used to share state or data across multiple components without having to pass props down manually through every level of the component tree.

Contexts are ideal for managing and sharing state or configuration values that need to be accessible by many components across the application. This can include:

User Authentication:
- Current user information, login status, and user preferences.
- Theme or Styling: Application-wide themes, color schemes, or style settings.
- Locale or Language: Current language, locale settings, and translations for internationalization.

Contexts can also be used to provide shared functionality or methods that are used by multiple components:
- API Calls: Functions to fetch data from a server or handle API requests.
- Event Handlers: Functions for handling user interactions or application events.

If you have state that is too complex or deeply nested to be easily managed with individual state hooks, you can use context to manage it:
- Application State: State related to navigation, routing, or overall application state that needs to be accessed globally.
- Data Caching: Shared data that might be fetched from an API and used across various components.

What Not to Put in Context
- Local Component State: For state that only affects a single component or is only used within a small part of the component tree, use local state with useState or useReducer instead.
- Frequent State Updates: If the context value changes very frequently (e.g., every keystroke), it can cause performance issues due to excessive re-renders. Consider local state or other optimization techniques in such cases.
- Component-Specific Logic: Any logic or state that is specific to a single component should generally remain within that component.
#### 1. Create a Context  

First, you need to create a context using React.createContext(). This function returns a Context object, which has two components: Provider and Consumer.

```js
import { createContext } from 'react';

const defaultContextValue = {
  user: null,
  theme: 'light',
  isLoggedIn: false
};

export const MyContext = createContext(defaultContextValue);
```
MyContext: This is the context object that will be used to provide and consume values.

#### 2. Provide Context Value

Wrap the parts of your component tree that need access to the context with a Provider. The Provider component allows you to pass down the context value to its descendants.

```js
import React, { useState } from 'react';
import { MyContext } from './MyContext';

const MyProvider = ({ children }) => {
  const [contextValue, setContextValue] = useState({
    user: { name: 'John Doe', email: 'john.doe@example.com' },
    theme: 'dark',
    isLoggedIn: true
  });

  return (
    <MyContext.Provider value={contextValue}>
      {children}
    </MyContext.Provider>
  );
};

export default MyProvider;
```
- MyContext.Provider: This component provides the context value to all its descendants.
- value: This is the data or state you want to share.

#### 3. Consume Context Value

Use the useContext hook to access the context value in any functional component that is a descendant of a Provider.

```js
import React, { useContext } from 'react';
import { MyContext } from './MyContext';

const MyComponent = () => {
  const { user, theme, isLoggedIn } = useContext(MyContext);

  return (
    <div>
      <h1>Context Information</h1>
      <p>User Name: {user ? user.name : 'Guest'}</p>
      <p>Email: {user ? user.email : 'N/A'}</p>
      <p>Theme: {theme}</p>
      <p>Status: {isLoggedIn ? 'Logged In' : 'Logged Out'}</p>
    </div>
  );
};

export default MyComponent;
```
- useContext(MyContext): Accesses the current value of MyContext.
- contextValue: The current context value as provided by the nearest MyContext.Provider.

#### 4. Wrap Your Component Tree

Ensure that the components using the context are wrapped in a Provider to get the context value.

```js
import React from 'react';
import MyProvider from './MyProvider';
import MyComponent from './MyComponent';

const App = () => (
  <MyProvider>
    <MyComponent />
  </MyProvider>
);

export default App;
```
MyProvider: Wraps the component tree to provide the context value.



### useContext A bit about efficiency and optimisation

React's context mechanism does not track changes to individual properties within the context object. Instead, it tracks changes to the entire context value. If any part of the context value changes, React will consider the context value as a whole to have changed.

So if we have a context with `a` and `b` variables, and ComponentA is only using `a` and ComponentB is only using `b`. What happens if only `b` changes?
- ComponentB will re-render because b is part of its context value and the context value changes.
- ComponentA will also re-render even though it only uses a from the context. This is because the context value object itself has changed (due to the update to b), and React triggers re-renders for all components that use the context, regardless of whether they use all parts of the context value or not.

Solution for this issue:


### Clarify a bit about rerenders of components
In React, a component may re-render even if its props haven’t changed due to several factors beyond just prop changes. Here are some common scenarios where a component might re-render:

- A component re-renders when its local state changes. This includes using useState in functional components or this.setState in class components.
```js
import React, { useState } from 'react';

const MyComponent = () => {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      {/* Here, clicking the button updates the state and causes MyComponent to re-render. */}
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
};
```

- When the state of a parent component changes, it can trigger a re-render of child components, even if their props haven't changed. This is because React re-renders the entire component tree when the state or props of a component change.
```js
import React, { useState } from 'react';
import ChildComponent from './ChildComponent';

const ParentComponent = () => {
  const [parentState, setParentState] = useState('initial');

  return (
    <div>
      <ChildComponent />
      <button onClick={() => setParentState('updated')}>Update Parent State</button>
    </div>
  );
};
```
- useContext usage when it's value change, like described above
- Components with a key prop will re-render if the key changes. This is often used in lists to uniquely identify elements. If the key for ListItem changes, it will trigger a re-render of that component.
```js
import React, { useState } from 'react';

const ListItem = ({ item }) => {
  return <div>{item}</div>;
};

const List = () => {
  const [items, setItems] = useState(['item1', 'item2']);

  return (
    <div>
      {items.map(item => (
        <ListItem key={item} item={item} />
      ))}
    </div>
  );
};
```

#### Optimize Context Consumers 1
React.memo is designed to optimize functional components by preventing unnecessary re-renders. It does this by performing a shallow comparison of the component's props. If the props have not changed, React.memo will skip the re-rendering of that component.

When a component uses useContext to consume context values, the behavior of React.memo is influenced by how context updates are handled. React.memo does not prevent a component from re-rendering if the context it consumes has changed. This is because context changes are not considered part of the props that React.memo compares.

So the take away here is: React.memo optimizes based on props only. Since context values are not props in the traditional sense but rather a global state shared via React’s context API, React.memo does not intercept or optimize these updates.

```js
import React, { memo } from 'react';
import { useMyContext } from './MyContext';

const ComponentA = () => {
  const { a } = useMyContext();

  return (
    <div>
      <h1>Value of A: {a}</h1>
    </div>
  );
};

export default memo(ComponentA);
```
THIS IS NOT A SOLUTION..
#### Optimize Context Consumers 2
Split the Context into Multiple Contexts

If a and b are logically separate and don’t need to be bundled together, you can split them into two different contexts. This way, each component will only subscribe to the context it actually uses.

```js
// ContextA.js
import React, { createContext, useContext, useState } from 'react';

const ContextA = createContext();

export const useContextA = () => useContext(ContextA);

export const ContextAProvider = ({ children }) => {
  const [a, setA] = useState('valueA');
  
  return (
    <ContextA.Provider value={{ a, setA }}>
      {children}
    </ContextA.Provider>
  );
};

// ContextB.js
import React, { createContext, useContext, useState } from 'react';

const ContextB = createContext();

export const useContextB = () => useContext(ContextB);

export const ContextBProvider = ({ children }) => {
  const [b, setB] = useState('valueB');
  
  return (
    <ContextB.Provider value={{ b, setB }}>
      {children}
    </ContextB.Provider>
  );
};

// App.js
import React from 'react';
import { ContextAProvider } from './ContextA';
import { ContextBProvider } from './ContextB';
import ComponentA from './ComponentA';
import ComponentB from './ComponentB';

const App = () => (
  <ContextAProvider>
    <ContextBProvider>
      <ComponentA />
      <ComponentB />
    </ContextBProvider>
  </ContextAProvider>
);
```
By splitting contexts, ComponentA will only re-render when a changes, and ComponentB will only re-render when b changes.

#### Optimize Context Consumers 3
useMemo is a React hook that memoizes the result of a computation (in this case, the JSX code inside the useMemo function) and returns a cached version of that result. It only recomputes the result when one of its dependencies changes.

useMemo is used to optimize performance by memoizing expensive calculations or render operations. It ensures that the computation or JSX is only recalculated when its dependencies change, preventing unnecessary re-renders.

```js
import React, { useMemo } from 'react';
import { useContextA } from './ContextA';

const ComponentA = () => {
  const { a } = useContextA();

  const content = useMemo(() => (
    <div>
      <h1>Value of A: {a}</h1>
    </div>
  ), [a]);

  return content; // could simply return the useMemo without creating a variable
};

export default ComponentA;
```
Parameters:
- First Argument: A function that returns the value you want to memoize—in this case, the JSX to render.
- Second Argument: An array of dependencies that determine when the value should be recalculated. Here, [a] is the dependency array.

While useMemo can help optimize performance, it does not prevent re-renders due to context updates. It only ensures that the computation or JSX rendering is performed only when necessary (i.e., when a changes).

Limitations and Considerations
- Overhead: Using useMemo does add some overhead, as React needs to keep track of the cached result and its dependencies. For simple cases, the performance benefits might not be significant, and using useMemo might not always be necessary.
- Dependencies: Ensure that all relevant dependencies are included in the dependency array to avoid stale or incorrect results.
___
### Memoize Context Value
Also another optimisation option for the problem that if the Provider's parent element rerenders, then the Provider will also rerender. And as a shallow comparison is used to compare the previous and new context object by default, it will cause a rerender. Which means all components using this context will rerender also.

```js
import React, { createContext, useState, useMemo, useContext } from 'react';

const MyContext = createContext();

export const MyProvider = ({ children }) => {
  const [state, setState] = useState('initial');

  // Memoize context value to prevent unnecessary re-renders
  const contextValue = useMemo(() => ({ state, setState }), [state]);

  return (
    <MyContext.Provider value={contextValue}>
      {children}
    </MyContext.Provider>
  );
};

export const useMyContext = () => useContext(MyContext);
```


### useCallback

#### how's life without useCallback
When you declare a function directly inside a component:
```js
const Component = () => {
  const handleClick = () => {
    console.log('Button clicked');
  };

  return <ButtonComponent onClick={handleClick}>Click me</ButtonComponent>;
};
```
Every time the component re-renders, a new instance of handleClick is created. This means handleClick has a new function reference on each render.

#### with the hook
If you use useCallback to memoize the function:
```js
import React, { useCallback } from 'react';

const Component = () => {
  const handleClick = useCallback(() => {
    console.log('Button clicked');
  }, []); // No dependencies

  return <ButtonComponent onClick={handleClick}>Click me</ButtonComponent>;
};
```
useCallback memoizes handleClick, meaning it will return the same function instance unless the dependencies change. Since there are no dependencies ([]), handleClick remains the same across renders.

#### in depth
useCallback is a React hook that returns a memoized version of a callback function. It’s used to optimize performance by preventing unnecessary re-creations of functions on every render. 

When you pass functions as props to child components or use them in dependencies of other hooks (like useEffect), React creates a new function instance on each render. This can lead to unnecessary re-renders of child components or re-executions of effects if those functions are used as dependencies.

useCallback helps avoid these issues by memoizing the function so that it remains the same between renders unless its dependencies change.

```js
const memoizedCallback = useCallback(() => {
  // Your callback logic here
}, [dependencies]);
```
- Callback Function: The function you want to memoize.
- Dependencies Array: An array of dependencies that the function relies on. The memoized function will only change if one of these dependencies changes.

How It Works
- Initial Render: On the first render, useCallback creates and returns a memoized version of the callback function.
- Subsequent Renders: On subsequent renders, if none of the dependencies have changed, useCallback returns the same function instance. If dependencies change, a new function instance is created and returned.

___
When using useCallback, the function you’re memoizing is only recreated if its dependencies change. This means if the dependencies array is empty ([]), the function will be created once and will persist across renders.

