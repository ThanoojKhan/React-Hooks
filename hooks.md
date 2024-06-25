React hooks are functions that let you "hook into" React state and lifecycle features from function components. They were introduced in React 16.8 to enable functional components to manage state and side effects, which were previously only possible in class components.

Here are some of the most commonly used React hooks:


1. useState
useState is a hook that lets you add React state to function components.

jsx
Copy code
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}



2. useEffect
useEffect is a hook that lets you perform side effects in function components. It's similar to componentDidMount, componentDidUpdate, and componentWillUnmount combined.

jsx
Copy code
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count]); // Only re-run the effect if count changes

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}



3. useContext
useContext is a hook that lets you subscribe to React context without introducing nesting.

jsx
Copy code
import React, { useContext } from 'react';

const MyContext = React.createContext();

function MyComponent() {
  const value = useContext(MyContext);
  return <div>{value}</div>;
}



4. useReducer
useReducer is usually preferable to useState when you have complex state logic that involves multiple sub-values or when the next state depends on the previous one.

jsx
Copy code
import React, { useReducer } from 'react';

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>
        +
      </button>
      <button onClick={() => dispatch({ type: 'decrement' })}>
        -
      </button>
    </div>
  );
}




5. useRef
useRef is a hook that lets you create a mutable object which persists for the lifetime of the component. It's often used to access a child directly or to keep a mutable variable that doesn’t cause a re-render when changed.

jsx
Copy code
import React, { useRef, useEffect } from 'react';

function TextInputWithFocusButton() {
  const inputEl = useRef(null);

  const onButtonClick = () => {
    inputEl.current.focus();
  };

  return (
    <div>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </div>
  );
}




6. useMemo
useMemo is a hook that memoizes a computed value and recomputes it only when the dependencies change. It's used to optimize performance.

jsx
Copy code
import React, { useMemo, useState } from 'react';

function ExpensiveCalculation({ num }) {
  const computeExpensiveValue = (num) => {
    console.log('Calculating...');
    // Expensive calculation
    return num * 2;
  };

  const memoizedValue = useMemo(() => computeExpensiveValue(num), [num]);

  return <div>{memoizedValue}</div>;
}

function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <ExpensiveCalculation num={count} />
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}



7. useCallback
useCallback returns a memoized callback function and is useful for optimizing performance when passing callbacks to child components.

jsx
Copy code
import React, { useState, useCallback } from 'react';

function Child({ onClick }) {
  return (
    <div>
      <button onClick={onClick}>Click me</button>
    </div>
  );
}

function Parent() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    setCount(count + 1);
  }, [count]);

  return (
    <div>
      <Child onClick={handleClick} />
      <p>Count: {count}</p>
    </div>
  );
}


These are some of the most commonly used React hooks. They allow you to manage state, perform side effects, and optimize performance in your functional components.