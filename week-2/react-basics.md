## What is React?

React is an open-source JavaScript library used for building user interfaces or UI components. It was created by Facebook and is widely used in web development for creating dynamic, interactive, and reusable UI components.

React follows a declarative approach to building UIs, meaning that developers can describe what the UI should look like and React handles the underlying logic of rendering the UI. It allows developers to easily manage complex UI components and makes it easier to reuse code, leading to more efficient and faster development.

React works by breaking down the UI into reusable components, which can be combined together to create complex user interfaces. React uses a virtual DOM (Document Object Model) to efficiently update the UI without having to reload the entire page.

React is widely used in web development and is supported by a large community of developers and companies. It is often used in conjunction with other JavaScript libraries and frameworks, such as Redux and React Native.

## What is a component?

In React, a component is a JavaScript function or class that returns a set of instructions, in the form of JSX (JavaScript Syntax Extension), for how a part of a user interface should appear and behave.

Components are the building blocks of React applications, and they can be reused throughout an application to create complex UIs. Components can take input data, known as "props", and use it to customize their appearance and behavior. They can also maintain internal state, which can change over time in response to user interactions or other events.

React components can be divided into two types: functional and class components. Functional components are simply JavaScript functions that take props as input and return JSX. Class components, on the other hand, are JavaScript classes that extend the React.Component class, and have additional features such as lifecycle methods and internal state management.

React components allow developers to create reusable, composable, and maintainable code, leading to more efficient development and easier maintenance over time. Components can be combined together to create more complex UIs, and they can be easily shared across different parts of an application or even between different applications.

![https://syllabus.codeyourfuture.io/20a620b45cf454e827f95f09fc46d13f.png](https://syllabus.codeyourfuture.io/20a620b45cf454e827f95f09fc46d13f.png)

Here we've highlighted some elements that could be components:

![https://syllabus.codeyourfuture.io/653082c56a767e43e911e109dc7a90bc.png](https://syllabus.codeyourfuture.io/653082c56a767e43e911e109dc7a90bc.png)

### Component tips

There are no hard & fast rules for making components. UIs can be split up into components in many different ways, requiring judgment based on your context.

- Components should follow the Single Responsibility Principle
  - Each component should only have 1 "responsibility"
  - Should only do 1 thing
- Components should have good, explicit names
  - This helps you to remember what the component's job is

### Exercise

EXERCISE

1. Look at the user interface below:

![https://syllabus.codeyourfuture.io/assets/images/twitter-components-exercise-908689f7062d165877f9d925bdb09091.png](https://syllabus.codeyourfuture.io/assets/images/twitter-components-exercise-908689f7062d165877f9d925bdb09091.png)

1. Draw boxes around the components and give them names. Compare with the example components shown in the second image.

## JSX

JSX (JavaScript Syntax Extension) is a syntax extension for JavaScript that allows developers to write HTML-like code within their JavaScript code. It is a syntax extension specific to React, and is used to define the structure and appearance of user interfaces in React applications.

JSX allows developers to write code that is more expressive and easier to read and understand, compared to traditional JavaScript code that manipulates the DOM directly. With JSX, developers can write code that looks like HTML, but includes JavaScript expressions within curly braces {}. For example:

`const element = <h1>Hello, {name}!</h1>;`

In the above code, JSX is used to create an h1 element with the text "Hello, {name}!". The curly braces are used to include a JavaScript expression within the element.

JSX is not required to use React, and React can be used without it. However, it is a popular and widely-used feature of React, and is often used in conjunction with other JavaScript features and libraries to create dynamic and interactive user interfaces. JSX is transformed into regular JavaScript code during the build process using a tool like Babel, and can be used with any JavaScript environment that supports ECMAScript 6 or higher.

React is already helping us a bit by cleaning up some of the verbose vanilla JS APIs. However, in a typical React application, you would still use a *lot* of `React.createElement` function. To improve the developer experience the React team developed **JSX**.

JSX is a syntax *sugar* that looks like HTML but is actually converted to `React.createElement` function when you run it.

Using JSX

```
const element = <div>Hello World</div>;

```

This is much easier to read than both the straight `React.createElement` API and the vanilla JS API. Most people using React use JSX to write their components.

## React Components

We looked at the beginning of the lesson at the concept of components. Now, look at how components are made in React.

```
import React from "react";
import ReactDOM from "react-dom";

function HelloWorld() {
return <div>Hello World</div>;
}

ReactDOM.render(<HelloWorld />, document.querySelector("#root"));

```

There are 3 important parts in this code:

1. First, we import `React`. This is important because JSX is converted to `React.createElement` calls. If the `React` variable is undefined then this will fail.
2. We create a React component called `HelloWorld`.
3. We *render* the `HelloWorld` component into the element with the id of `root`.

DEFINITION

The process of *rendering* is turning the JSX elements returned by the component function into DOM elements on the screen. This is done by React for you.

## Embedding JavaScript into JSX

So far all of the components we have looked at haven't been able to change - they are *hard-coded*. But this doesn't make very interesting websites. We want to use variables with different data. We can insert variables (and some other things) into our React components.

Anything in the JSX that is inside curly braces `{}` is interpreted as a regular JavaScript *expression*. That means you can use every object or function from JavaScript that we have learned so far.

```
function Greeting() {
const greetingWord = "Hello";

return <span>{greetingWord}</span>;
}

```

Now instead of hard-coding the greeting in the `Greeting` component, we are using a variable. Remember that everything between the curly braces is just regular JavaScript. So we can use more than just variables.

```
function Mentor() {
const mentors = ["Ali", "Kash", "Davide", "German", "Gerald"];
return <span>{mentors.join(", ")}</span>;
}

```

Now we have modified the `Mentor` component to use the `Array.join` method so that it lists several mentors' names. This works with other JS types:

```
function Addition() {
return <span>{1 + 2 + 3}</span>;
}

```

```
function Weather() {
const weatherData = {
    temperature: 5,
    location: "London",
  };

return (
    <p>
      The temperaturein {weatherData.location} is {weatherData.temperature}
    </p>
  );
}

```

```
function formatName(user) {
return user.firstName + " " + user.lastName;
}

function Name() {
const user = {
    firstName: "Bob",
    lastName: "Marley",
  };
return <span>{formatName(user)}</span>;
}

```

A common pattern in React is to use `Array.map` to loop through a list of items and render a component for each one

```
const mentors = ["Ali", "Kash", "Davide", "German", "Gerald"];

function MentorsList() {
return (
    <ul>
      {mentors.map((name) => (
        <li>{name}</li>
      ))}
    </ul>
  );
}

```

Here we are using `Array.map` to turn an array of strings into an array of components.

# React Component Composition

In React, we can make components more generic by accepting `props`, which are to React components what parameters are to functions.

Component composition is the name for passing components as props to other components, thus creating new components with other components.

### How can composition help performance?

Composition is also a great ally if you try to reduce the number of re-renders in your application.
![Employee Component Composition](/week-3/employee-component-flow-chart.png)

```jsx
<App/>
	<HomePage/>
		<Header/>
		<SearchBar/>
		<EmployeeList/>
			<EmployeeListItem/>
	<EmployeePage/>
		<Header/>
		<EmployeeDetail/>
```

Step 1. `import` `HomePage` and `EmployeePage` components into `App` component and render them on the browser.

Step 2. `import` `Header`, `SearchBar`, and `EmployeeList` inside the `HomePage` component and render them on the browser

Step 3. `import` the `EmployeeListItem` component into the `EmployeeList` component

Step 4. `import` the `Header` and `EmployeeDetail` components into `EmployeePage` components and take a screenshot of what is rendered on the browser
