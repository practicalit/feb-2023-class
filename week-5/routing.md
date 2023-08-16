# Routing (react-router-dom v6)

### **1. Installation**

To start, you'll need to install **`react-router-dom`**:

```bash

npm install react-router-dom

```

### **2. Basic Routing**

To get started, you can set up your main App component with some routes:

```jsx
import React from "react";
import { BrowserRouter as Router, Routes, Route, Link } from "react-router-dom";

function Home() {
  return <h2>Home</h2>;
}

function About() {
  return <h2>About</h2>;
}

function App() {
  return (
    <Router>
      <nav>
        <ul>
          <li>
            <Link to='/'>Home</Link>
          </li>
          <li>
            <Link to='/about'>About</Link>
          </li>
        </ul>
      </nav>

      <Routes>
        <Route path='/' element={<Home />} />
        <Route path='/about' element={<About />} />
      </Routes>
    </Router>
  );
}

export default App;
```

In the code above:

- We have the **`Router`** component wrapping our application.
- The **`Routes`** component contains all our **`Route`** components.
- Each **`Route`** uses an **`element`** prop to specify which component should render for that route.
- **`Link`** is used for navigation.

### **3. Nested Routing**

Let's say you want to have nested routes. Here's how you can set that up:

```jsx
javascriptCopy code
import { Outlet } from 'react-router-dom';

function Dashboard() {
  return (
    <div>
      <h2>Dashboard</h2>
      <Outlet />
    </div>
  );
}

function Profile() {
  return <h3>Profile</h3>;
}

function App() {
  return (
    <Router>
      {/* ... */}
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/dashboard" element={<Dashboard />}>
          <Route path="profile" element={<Profile />} />
        </Route>
      </Routes>
    </Router>
  );
}

```

Here, if you navigate to **`/dashboard/profile`**, you'll see both the **`Dashboard`** and **`Profile`** components. This is because **`Outlet`** renders any nested routes.

### **4. Navigate Programmatically**

To navigate programmatically in v6, use the **`useNavigate`** hook:

```jsx
javascriptCopy code
import { useNavigate } from 'react-router-dom';

function MyComponent() {
  const navigate = useNavigate();

  const goToHome = () => {
    navigate("/");
  };

  return <button onClick={goToHome}>Go Home</button>;
}

```

### **5. Access Route Parameters**

To access parameters from the URL, use the **`useParams`** hook:

```jsx
javascriptCopy code
import { useParams } from 'react-router-dom';

function User() {
  const { userId } = useParams();
  return <h2>User ID: {userId}</h2>;
}

// When defining your routes:
// <Route path="/user/:userId" element={<User />} />

```

In the code above, if you navigate to **`/user/123`**, the **`User`** component will display "User ID: 123".
