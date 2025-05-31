# React.js Notes

## Table of Contents

- [Introduction: How React Works](#introduction-how-react-works)
- [JSX](#jsx)
- [Components](#components)
- [Props](#props)
- [State](#state)
- [State vs Props](#state-vs-props)
- [Children Prop](#children-prop)
- [Handling Events](#handling-events)
- [State Management](#state-management)
- [Context API](#context-api)
- [Hooks](#hooks)
- [React Router](#react-router)
- [Thinking in React Components](#thinking-in-react-components)
- [Effect and Data Fetching](#effect-and-data-fetching)

---

## Introduction: How React Works

### Component vs Instance vs Element

#### Component

![alt text](how-react-works/components-react.png)

#### Instance

![alt text](how-react-works/component-instance.png)

#### Element

![alt text](how-react-works/react-element.png)

#### Element to DOM (HTML)

![alt text](how-react-works/elemet-to-dom.png)

#### Why can't we call component as function

```jsx
{
  TabContent({ item: content.at(activeTab) });
}
```

- It does not create an instance of the component
- It can't contain its name
- Renders its return value as a child of the parent component (becomes a **div** of parent component)

![alt text](how-react-works/wrong-way-to-use-components.png)
![alt text](how-react-works/cant-even-mahange-own-state.png)

#### How components displayed on the screen

![alt text](how-react-works/how-component-displayed-on-the-screen.png)

#### How render is triggered

![alt text](how-react-works/how-render-is-trigered.png)

#### How state updates are batched

![alt text](how-react-works/how-stateUpdate-areBatched.png)

#### State update is asynchronous

![alt text](how-react-works/updating-stateIs-asynchronous.png)

#### The render phase

![alt text](how-react-works/render-phase.png)

#### What is virtual DOM

![alt text](how-react-works/virtual-dom.png)

#### What is reconciliation

![alt text](how-react-works/reconciliation.png)

#### The reconciler Fiber

![alt text](how-react-works/the-reconciler-FIBER.png)

#### Reconciliation in action

![alt text](how-react-works/reconciliation-in-action.png)

#### Commit and Browser paint phase

![alt text](how-react-works/the-commit-and-browserpain-phase.png)

#### It is ReactDOM who writes the DOM

![alt text](how-react-works/commit-and-browserpaint-2.png)

#### Recap

![alt text](how-react-works/recape.png)

#### How diffing (algorithm) works

![alt text](how-react-works/how-diffing-works.png)
![alt text](how-react-works/how-diffing-works-2.png)

#### The key prop

![alt text](how-react-works/the-key-prop.png)

##### Stable Key (keys in lists)

![alt text](how-react-works/keys-in-lists-stableKey.png)

##### Changing key (key prop to reset state)

![alt text](how-react-works/key-prop-to-reset-state-ChangingKey.png)

---

## JSX

### JSX (JavaScript XML)

![JavaScript XML](pizza-menu/JSX.png)

#### JSX vs HTML

![jsx-vs-html](pizza-menu/jsx-vs-html.png)

#### JSX is declarative

- "Declarative" refers to a programming paradigm where you describe what you want to see in your UI, rather than how to achieve it.

![declarative](pizza-menu/JSX-declarative.png)

#### Basic styling in React

- Inline CSS uses double curly brackets: `{{}}` (first for JS, second for object)
- Use `className` instead of `class`

```js
function Header() {
  return (
    <h1 style={{ color: "red", fontSize: "48px", fontStyle: "uppercase" }}>
      Fast React Pizza CO.
    </h1>
  );
}
```

---

## Components

![Components](pizza-menu/about%20components.png)

- The first letter of a component name should be capitalized
- Function needs to return some markup (JSX) or null.

#### Components tree

- A hierarchical structure of React components
- Each node represents a component, edges represent parent-child relationships
- Used by React to manage rendering and updating of components

```jsx
<AppComponent>
  <Header />
  <MainContent>
    <Sidebar />
    <Article />
  </MainContent>
  <Footer />
</AppComponent>
```

Becomes:

```
AppComponent
  ├── Header
  ├── MainContent
  │   ├── Sidebar
  │   └── Article
  └── Footer
```

![components tree](pizza-menu/components%20tree.png)

---

## Props

- Short for "properties"
- Way to pass data from parent to child component
- Immutable (can't be changed by child component)
- Passed like function arguments
- Can be any data type (strings, numbers, booleans, arrays, objects, functions, even other components)

```js
// Parent component
function Menu() {
  return (
    <main className="menu">
      <h2>Our Menu</h2>
      <Pizza
        name="Pizza Spinaci"
        ingredients="tomato, mozarella, spinach, and ricotta cheese"
      />
    </main>
  );
}
```

---

## State

![state](steps/state.png)
![state-example](steps/state-example.png)

- useState is a React hook that allows you to add state to functional components
- Returns an array with two elements: the current state value and a function to update that value
- The update function is typically used in event handlers or other functions to update the state
- The state is re-rendered whenever the state value changes
- The state value should be immutable

```js
const [step, setStep] = useState(1);

function handleNext() {
  if (step < 3) setStep(step + 1);
}

function handlePrevious() {
  if (step > 1) setStep(step - 1);
}
```

#### Practical state guideline

![state-guide-line](steps/practicak-state-guideline.png)

---

## State vs Props

![state vs props](steps/state-vs-props.png)

---

## Children Prop

- In React, the `children` prop is a special prop that allows you to pass components, strings, numbers, or arrays of components as props to other components.

**Simple Example:**

```jsx
import React from "react";

const Parent = ({ children }) => {
  return <div>{children}</div>;
};

const App = () => {
  return (
    <Parent>
      <h1>Hello World!</h1>
      <p>This is a paragraph.</p>
    </Parent>
  );
};
```

![children-prop](steps/children-prop.png)

---

## Handling Events

- Pass a function reference to the event handler, like this: `onClick={() => alert("previous")}`
- Ensure the event handler is a function that takes an event object as an argument
- Correct prop name for mouse enter event: `onMouseEnter`

```js
const handlePrevious = function(){
    alert("previous")
}
<button
  // right way
  onClick={() => alert("previous")}
  onClick={handlePrevious}

  //   wrong way
  onClick={alert("wrong")}
  onClick={handlePrevious()}
>
  Previous
</button>
```

---

## State Management

![thinking in react](state-management/thinking-in-react.png)

### What is state management

![state management](state-management/what-is-State-managment.png)

### Local VS Global State

![local Vs Global state](state-management/localVSglobal-state.png)

### When and where to create state

![When and where to create state](state-management/when%26where-crerate-state%2B.png)

---

## Context API

![alt text](Atomic-blog/context-Api.png)
![alt text](Atomic-blog/what-is-context-api.png)

### What is Context API?

Context API is a React feature that enables sharing state across the component tree without prop drilling. It's perfect for managing global state like:

- Theme preferences
- User authentication
- Language settings
- Application-wide data

#### Real Implementation Example

```jsx
// 1. Creating Context
const PostContext = createContext();

// 2. Provider Setup
<PostContext.Provider
  value={{
    posts,
    searchQuery,
    setSearchQuery,
    onAddPost,
    onClearPost,
  }}
>
  {/* Components */}
</PostContext.Provider>;

// 3. Consuming Context
function SearchPosts() {
  const { searchQuery, setSearchQuery } = useContext(PostContext);
  return (
    <input
      value={searchQuery}
      onChange={(e) => setSearchQuery(e.target.value)}
      placeholder="Search posts..."
    />
  );
}
```

#### Context API Implementation Steps

1. **Create Context**
   ```jsx
   const MyContext = createContext();
   ```
2. **Provide Context**
   ```jsx
   <MyContext.Provider value={/* shared data */}>
     {/* Child components */}
   </MyContext.Provider>
   ```
3. **Consume Context**
   ```jsx
   const contextData = useContext(MyContext);
   ```

#### Best Practices

- Use for global state management
- Avoid for small component trees or frequently changing state
- Context triggers re-renders for all consumers
- Split contexts by functionality
- Use `useMemo` for complex context values
- Consider state management libraries for complex apps

---

## Hooks

### useState

- Allows you to add state to functional components
- Returns an array with the current state and a function to update it

### useReducer

![alt text](react-quiz/why-useReducer.png)

#### Managing state with useReducer

![alt text](react-quiz/state-with-useReducer.png)

#### How useReducer updates state

![alt text](react-quiz/how-reducer-update-state.png)

#### useReducer mental model

![alt text](react-quiz/useReducer-mentalModel.png)

#### useReducer vs useState

![alt text](react-quiz/useState-VS-useReducer.png)

#### When to use useReducer

![alt text](react-quiz/when-useReducer.png)

#### useReducer live action

```js
import { useReducer, useState } from "react";
const initialState = { count: 0, step: 1 };

function reducer(state, action) {
  switch (action.type) {
    case "inc":
      return { ...state, count: state.count + state.step };
    case "dec":
      return { ...state, count: state.count - state.step };
    case "setCount":
      return { ...state, count: action.payload };
    case "setStep":
      return { ...state, step: action.payload };
    case "reset":
      return initialState;
    default:
      throw new Error("unknown action type");
  }
}

function DateCounter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  const { count, step } = state;

  const date = new Date("june 21 2027");
  date.setDate(date.getDate() + count);

  const dec = function () {
    dispatch({ type: "dec" });
  };

  const inc = function () {
    dispatch({ type: "inc" });
  };

  const defineCount = function (e) {
    dispatch({ type: "setCount", payload: Number(e.target.value) });
  };

  const defineStep = function (e) {
    dispatch({ type: "setStep", payload: Number(e.target.value) });
  };

  const reset = function () {
    dispatch({ type: "reset" });
  };

  return (
    <div className="counter">
      <div>
        <input
          type="range"
          min="0"
          max="10"
          value={step}
          onChange={defineStep}
        />
        <span>{step}</span>
      </div>
      <button onClick={dec}>-</button>
      <input type="number" value={count} onChange={defineCount} />
      <button onClick={inc}>+</button>
      <div>
        <span>{date.toDateString()}</span>
      </div>
      <button onClick={reset}>Reset</button>
    </div>
  );
}
```

---

## React Router

### React Routing

![alt text](react%20theory%20ss/react-routing.png)

### SPA (Single Page Application)

![alt text](react%20theory%20ss/single-page-app.png)

### URL for State Management

![alt text](react%20theory%20ss/url-state-management.png)

### Params & Query String

![alt text](react%20theory%20ss/params-query-string.png)

- **URL Parameters**: Used for essential data (e.g., IDs)
- **Query Strings**: Used for optional data (e.g., filters, coordinates)

### Best Practices

1. Use nested routes for related views
2. Implement 404 handling with catch-all routes
3. Use NavLink for navigation with active states
4. Keep URLs clean and semantic
5. Use proper route organization

---

## Thinking in React Components

### How to split a component

![How to split a component](react%20theory%20ss/how%20to%20split%20a%20component.png)

### When to create new components

![When to create new components](react%20theory%20ss/when-to-create-a-new-components.png)

### General components guideline

![General components guideline](react%20theory%20ss/general-components-guideline.png)

### Different Size and Reusability

![Different Size and Reusability](react%20theory%20ss/differentSize-and-Reusability.png)

### What is component Composition

![what is composition](react%20theory%20ss/what-is-composition.png)

---

## Effect and Data Fetching

### Component lifecycle

![alt text](react%20theory%20ss/component-lifeCycle.png)

### Event handler vs effect

![alt text](react%20theory%20ss/eventHandler-vs-effect.png)

### Dependency array

![alt text](react%20theory%20ss/dependency-array.png)

### useEffects synchronize mechanism

![alt text](react%20theory%20ss/use-effect-synchronize-mechanism.png)

### Synchronization and lifeCycle

![alt text](react%20theory%20ss/synchronization-and-lifeCycle.png)

### When Effect are executed

![alt text](react%20theory%20ss/when-are-effect-executed.png)

### useEffect CleanUp function

![alt text](react%20theory%20ss/use-Effect-clean-up-fn.png)

#### CleanUp data fetching with **Abort controller**

```js
useEffect(
  function () {
    const controller = new AbortController();
    async function fetchData() {
      try {
        setIsLoading(true);
        setError("");

        const response = await fetch(
          `https://www.omdbapi.com/?s=${query}&apikey=${KEY}`,
          { signal: controller.signal }
        );

        if (!response.ok) throw new Error("Error fetching movies");

        const data = await response.json();

        if (data.Response === "False") throw new Error("Movie not found");
        setMovies(data.Search);

        setError("");
      } catch (error) {
        if (error.name !== "AbortError") {
          setError(error.message);
        }
      }
      setIsLoading(false);
    }
    fetchData();
    return function () {
      controller.abort();
    };
  },
  [query]
);
```

---
