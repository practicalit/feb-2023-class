# Redux

**Redux:** is a predictable state container for JavaScript apps. It helps you write applications that behave consistently, run in different environments (client, server, and native), and are easy to test.

https://redux.js.org/

**Core Principles of Redux:**

1. **Single source of truth**: The state of your whole application is stored in an object tree within a single store.
2. **State is read-only**: The only way to change the state is to emit an action, an object describing what happened.
3. **Changes are made with pure functions**: To specify how the state tree is transformed by actions, you write pure reducers.

**Redux Toolkit**: It's the official, opinionated, batteries-included toolset for efficient Redux development. It includes utilities to simplify several common Redux use cases, like storing data, responding to asynchronous calls, and more.

https://redux-toolkit.js.org/

Let's break down the basic concepts and then look at a simple example.

**1. Action**: Plain JavaScript objects that have a **`type`** field. You can also put more info into actions.

Example:

```jsx
{
  type: "INCREMENT";
}
```

**2. Reducer**: Pure functions that take the previous state and an action, and return the next state.

Example:

```jsx
function counter(state = 0, action) {
  switch (action.type) {
    case "INCREMENT":
      return state + 1;
    case "DECREMENT":
      return state - 1;
    default:
      return state;
  }
}
```

**3. Store**: Holds application state; allows access to state via **`getState()`**, allows state to be updated via **`dispatch(action)`**, and registers listeners via **`subscribe(listener)`**.

Now, let's create a basic counter using Redux and Redux Toolkit.

**Simple Todo App Example:**

1. **Setting up Redux Toolkit**:
   Install Redux Toolkit using **`npm`** or **`yarn`**:

```bash
npm install @reduxjs/toolkit react-redux

```

1. **Create a slice of the Redux store for our to-do items**:

```jsx
import { createSlice } from "@reduxjs/toolkit";

export const todosSlice = createSlice({
  name: "todos",
  initialState: [],
  reducers: {
    addTodo: (state, action) => {
      state.push({ id: Date.now(), text: action.payload, completed: false });
    },
    toggleTodo: (state, action) => {
      const todo = state.find((todo) => todo.id === action.payload);
      if (todo) {
        todo.completed = !todo.completed;
      }
    },
  },
});

export const { addTodo, toggleTodo } = todosSlice.actions;
export default todosSlice.reducer;
```

1. **Set up the store**:

```jsx
import { configureStore } from "@reduxjs/toolkit";
import todosReducer from "./todosSlice";

export const store = configureStore({
  reducer: {
    todos: todosReducer,
  },
});
```

1. **Using in a React component**:

```jsx
import React, { useState } from "react";
import { useDispatch, useSelector } from "react-redux";
import { addTodo, toggleTodo } from "./todosSlice";

function App() {
  const [input, setInput] = useState("");
  const todos = useSelector((state) => state.todos);
  const dispatch = useDispatch();

  return (
    <div>
      <input value={input} onChange={(e) => setInput(e.target.value)} />
      <button
        onClick={() => {
          dispatch(addTodo(input));
          setInput("");
        }}
      >
        Add Todo
      </button>

      <ul>
        {todos.map((todo) => (
          <li
            key={todo.id}
            onClick={() => dispatch(toggleTodo(todo.id))}
            style={{ textDecoration: todo.completed ? "line-through" : "none" }}
          >
            {todo.text}
          </li>
        ))}
      </ul>
    </div>
  );
}

export default App;
```

1. **Wrap your App in the Provider**:

```jsx
import React from "react";
import ReactDOM from "react-dom";
import { Provider } from "react-redux";
import App from "./App";
import { store } from "./store";

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById("root")
);
```
