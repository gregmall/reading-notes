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


