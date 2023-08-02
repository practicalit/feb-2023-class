# The useEffect hook

The **`useEffect`** hook is a built-in hook in React that allows you to perform side effects in your function components. Side effects could be things like data fetching, subscriptions, or manually changing the DOM that would typically be done inside `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount` in class components.

The **`useEffect`** hook takes two arguments: a function (which we call the effect) and a dependency array.

**Basic Syntax:**

```jsx
useEffect(() => {
  // side effect goes here
}, [dependencies]);
```

**First Argument - Function**

The first argument to **`useEffect`** is the function where you'll perform your side effect. This could be fetching data from an API, subscribing to some service, setting up a timer, etc.

**Second Argument - Dependency Array**

The second argument to **`useEffect`** is an array of dependencies for your effect. When any of the dependencies change, the effect will run again. If you pass an empty array (**`[]`**), the effect will only run once after the initial render, similar to **`componentDidMount`** in class components.

Here's an example of **`useEffect`**:

```jsx
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // Re-run the effect when `count` changes
```

In the above example, the **`useEffect`** hook will change the document title whenever the **`count`** state changes.

**Cleaning Up Effects**

Some side effects might require cleaning up. For instance, if you're setting up a subscription in your effect, you'll want to tear it down when the component is unmounted. To do this, you return a function from your effect. This function will be run by React when it's time to clean up:

```jsx
useEffect(() => {
  const subscription = props.source.subscribe();
  return () => {
    // Clean up the subscription
    subscription.unsubscribe();
  };
}, [props.source]);
```

In this example, a subscription is established, and then the cleanup function unsubscribes when the component is unmounted or before re-running the effect due to changes in dependencies.

**Skipping Side Effects**

By default, effects run after every completed render. However, this might be more than you need. If your effect doesn’t need to run after every render, you can tell React to skip an effect if certain values haven’t changed between re-renders by providing an array as a second argument.

```jsx
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // Only re-run the effect if `count` changes
```

In this example, the effect will only re-run if the **`count`** value changes.

**If you omit the array entirely**

If you omit the second argument entirely, the effect will run after every render.

```jsx
jsxCopy code
useEffect(() => {
  document.title = `You clicked ${count} times`;
});  // Re-run the effect after every render

```

In this case, the effect will run after every re-render.

**Note:**

1. All **`useEffect`** tasks are not blocking the browser from updating the screen, which means they are performed asynchronously and do not block the browser.
2. If the function inside **`useEffect`** returns a function, React will run it when it is time to clean up.
3. Always use the **`useEffect`** hook inside the body of a function component. Do not use it inside loops, conditions, or nested functions.
4. If you use multiple effects, they will run in the order they are defined.
5. Be careful with the dependencies you pass to the array. If the dependencies change too often, you might trigger your effect more often than necessary. On the other hand, if you forget to include a dependency, your effect might not update when it should.

That's the basic idea of the **`useEffect`** hook! It's a powerful tool, but it requires understanding and careful use.

**1. useEffect with no dependencies:**

This is similar to **`componentDidMount`** and **`componentDidUpdate`** combined in class components, i.e., the effect runs after every render.

```jsx
const [count, setCount] = useState(0);

useEffect(() => {
  document.title = `You clicked ${count} times`;
});

return (
  <div>
    <p>You clicked {count} times</p>
    <button onClick={() => setCount(count + 1)}>Click me</button>
  </div>
);
```

In this example, the document title is updated after every render.

**2. useEffect with empty dependency array:**

This is similar to **`componentDidMount`** in class components, i.e., the effect runs once after the initial render.

```jsx
const [count, setCount] = useState(0);

useEffect(() => {
  console.log("Component mounted");
}, []);

return (
  <div>
    <p>You clicked {count} times</p>
    <button onClick={() => setCount(count + 1)}>Click me</button>
  </div>
);
```

In this example, "Component mounted" is logged to the console once when the component is first rendered.

**3. useEffect with specific dependencies:**

The effect runs after the initial render and whenever a dependency changes.

```jsx
const [count, setCount] = useState(0);

useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]);

return (
  <div>
    <p>You clicked {count} times</p>
    <button onClick={() => setCount(count + 1)}>Click me</button>
  </div>
);
```

In this example, the document title is updated whenever the **`count`** state changes.

**4. useEffect with cleanup:**

Sometimes, you need to clean up side effects, such as canceling network requests, clearing timers, or removing event listeners.

```jsx
useEffect(() => {
  const timer = setTimeout(() => {
    console.log("This will run after 1 second");
  }, 1000);

  return () => {
    clearTimeout(timer);
  };
}, []);
```

In this example, a timer is set up that logs a message after 1 second. If the component unmounts before the timer goes off, the cleanup function is called, preventing the log message and preventing a potential memory leak.

**5. useEffect with multiple dependencies:**

You can provide multiple dependencies to **`useEffect`**.

```jsx
jsxCopy code
const [count, setCount] = useState(0);
const [timestamp, setTimestamp] = useState(Date.now());

useEffect(() => {
  document.title = `Count: ${count}, Timestamp: ${timestamp}`;
}, [count, timestamp]);

return (
  <div>
    <p>You clicked {count} times</p>
    <button onClick={() => {setCount(count + 1); setTimestamp(Date.now())}}>
      Click me
    </button>
  </div>
);

```

In this example, the document title updates whenever either the **`count`** or **`timestamp`** states change.

These examples should help illustrate how to use **`useEffect`** in different scenarios.

The **`useEffect`** hook in React is very versatile and is used in many scenarios beyond the ones discussed previously. Here are a few more use cases:

**1. Fetching Data:**

**`useEffect`** is commonly used for fetching data from an API when a component mounts and possibly when certain props/state change:

```jsx
const [data, setData] = useState(null);

useEffect(() => {
  fetch("/api/data")
    .then((response) => response.json())
    .then((data) => setData(data));
}, []); // Only runs once after initial render
```

**2. Event Listeners:**

You can also use **`useEffect`** to add event listeners to the **`window`** or other DOM elements:

```jsx
useEffect(() => {
  const handleResize = () => {
    console.log(window.innerWidth);
  };

  window.addEventListener("resize", handleResize);

  // Remember to clean up with a return function
  return () => {
    window.removeEventListener("resize", handleResize);
  };
}, []); // Only runs once after initial render
```

**3. Interaction with Local Storage:**

**`useEffect`** can be used to sync state with local storage:

```jsx
jsxCopy code
const [name, setName] = useState(localStorage.getItem('name') || '');

useEffect(() => {
  localStorage.setItem('name', name);
}, [name]);  // Runs after name changes

```

**4. Interval or Timeout:**

**`useEffect`** can also be used to run interval or timeout functions:

```jsx
useEffect(() => {
  const id = setInterval(() => {
    // something to do every second...
  }, 1000);

  return () => {
    clearInterval(id);
  };
}, []); // Only runs once after initial render
```

**5. Working with external libraries:**

Sometimes, you may need to work with an external JS library that needs direct access to the DOM. **`useEffect`** is a great place to integrate these kinds of effects.

```jsx
useEffect(() => {
  // instantiate and use a library that needs direct DOM access
}, []);
```

The **`useEffect`** hook is one of the most versatile tools in React as it allows you to perform any kind of side effect in a function component. The scenarios listed above and before are just examples, you'll find many more uses for **`useEffect`** as you build different things with React.
