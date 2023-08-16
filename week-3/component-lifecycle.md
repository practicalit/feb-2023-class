_Component lifecycle_

**1. componentDidMount:**

In class components, **`componentDidMount`** is called once the component has been rendered to the DOM.

Equivalent in functional components with Hooks:

```jsx
useEffect(() => {
  // Your code here
}, []); // Passing an empty array as second argument
```

The second argument to **`useEffect`** is an array of dependencies that will cause the effect to rerun if they change. If you pass an empty array (**`[]`**), the effect will only run once after the initial render, just like **`componentDidMount`**.

**2. componentDidUpdate:**

In class components, **`componentDidUpdate`** is called after the component updates, meaning when state or props change.

Equivalent in functional components with Hooks:

```jsx
useEffect(() => {
  // Your code here
}); // No second argument
```

By omitting the second argument, the effect will run after every render, much like **`componentDidUpdate`**.

If you only want the effect to run when certain values have changed, you can pass those values in the dependency array:

```jsx
useEffect(() => {
  // Your code here
}, [value1, value2]); // Only re-run the effect if `value1` or `value2` changes
```

**3. componentWillUnmount:**

In class components, **`componentWillUnmount`** is called just before the component is unmounted and destroyed.

Equivalent in functional components with Hooks:

```jsx
useEffect(() => {
  // Your code here

  return () => {
    // Your cleanup code here
  };
}, []); // Passing an empty array as second argument
```

By returning a function from the effect, this function will be called when it's time to cleanup. This is akin to the **`componentWillUnmount`** lifecycle method in class components.

As a conclusion, the **`useEffect`** hook in functional components can be used to mimic the different lifecycle methods that are available in class components, giving you similar control over your component's behavior during different stages of its lifecycle.
