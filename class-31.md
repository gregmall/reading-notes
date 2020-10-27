# Building Your Own Hooks
* Lets you extract component logic into reusable functions
* A custom Hook is a JavaScript function whose name starts with ”use” and that may call other Hooks.
```
import { useState, useEffect } from 'react';

function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}
```
* Custom Hooks are a convention that naturally follows from the design of Hooks, rather than a React feature
* Always name your custom hooks starting with 'use'
* Custom Hooks are a mechanism to reuse stateful logic
  - every time you use a custom Hook, all state and effects inside of it are fully isolated
* Each call to a Hook gets isolated state
* we can call useState and useEffect many times in one component, and they will be completely independent

* Custom Hooks offer the flexibility of sharing logic that wasn’t possible in React components before

# Rules of Hooks
* **Only Call Hooks at the Top Level**
  - ensure that Hooks are called in the same order each time a component renders
* **Only Call Hooks from React Functions**
  - ensure that all stateful logic in a component is clearly visible from its source code
### ESLint Plugin
* included by default in Create React App
```
npm install eslint-plugin-react-hooks --save-dev
```
```
// Your ESLint configuration
{
  "plugins": [
    // ...
    "react-hooks"
  ],
  "rules": {
    // ...
    "react-hooks/rules-of-hooks": "error", // Checks rules of Hooks
    "react-hooks/exhaustive-deps": "warn" // Checks effect dependencies
  }
}
```
* React relies on the order in which Hooks are called

# The Guide to Learning React Hooks
* How to use hooks
  - side by side comparison with class components are the best way to describe hooks
![side by side](/assets/beforeandafter.gif)
* **Five important rules for hooks
  1. Never call Hooks from inside a loop, condition or nested function
  2. Hooks should sit at the top-level of your component
  3. Only call Hooks from React functional components
  4. Never call a Hook from a regular function
  5. Hooks can call other Hooks
* setState allows us to use state and a function across component react components
* useEffect can operate like componentDidMount
  - can run once or set amount of times
  - runs whe page renders
* React Hooks Reducer, similar to the JavaScript Arrays reducer, returns the accumulation of something, React state in our case

# 10 Essential React Hooks

### useArray hook
* reduces this burden by providing us with various array manipulation methods
```
import {useArray} from 'react-hanger'
```
### react-use-form-state hook
*  small React Hook that attempts to simplify managing form state, using the native form input elements you are familiar with
```
npm i react-use-form-state
```
### react-fetch-hook
* Making ajax calls is like the most basic and most performed task for a frontend developer. And the React community is quick enough to create a hook for this purpose too.
```
npm i react-fetch-hook
```
### useMedia hook
* React sensor hook that tracks the state of a CSS media query

### react-useportal hook
* React Portals provide a first-class way to render children into a DOM node that exists outside the DOM hierarchy of the parent component
  - provides us with two methods openPortal and closePortal
### react-firebaase-hooks
* We all appreciate the greatness of firebase and use it a lot in our projects, whether its for authentication or storage
```
npm i react-firebase-hooks
```
### use-onClickOutside hook
* An outside click is a way to know if the user clicks everything but a specific component
  - You may have seen this behavior when opening a dropdown menu or a modal or a dropdown list
### useIntersectionObserver hook
* React hook for using intersection observers
  - The Intersection Observer API provides a way to asynchronously observe changes in the intersection of a target element with an ancestor element or with a top-level document’s viewport
```
npm i react-use-intersection-observer
```
### use-location hook
* hook is used for getting the location of the browser
### use-redux hook
* This hook returns the store and dispatch property

SEE ALL THE CODE EXAMPLES HERE : [LINK LINK LINK](https://blog.bitsrc.io/10-react-custom-hooks-you-should-have-in-your-toolbox-aa27d3f5564d)

