# Context API
* Context provides a way to pass data through the component tree without having to pass props down manually at every level
  - provides a way to share values between components without having to explicitly pass a prop through every level of the tree
### When to Use Context
* Context is designed to share data that can be considered “global” for a tree of React components, such as the current authenticated user, theme, or preferred language

### Before You Use Context
* primarily used when some data needs to be accessible by many components at different nesting levels
  - apply it sparingly because it makes component reuse more difficult
### API
* **React.createContext**
- Creates a Context object
  - it will read the current context value from the closest matching Provider above it in the tree
* **Context.Provider**
- Every Context object comes with a Provider React component that allows consuming components to subscribe to context changes.
  - accepts a value prop to be passed to consuming components that are descendants of this Provider
  - One Provider can be connected to many consumers
* **Class.contextType**
```
class MyClass extends React.Component {
  componentDidMount() {
    let value = this.context;
    /* perform a side-effect at mount using the value of MyContext */
  }
  componentDidUpdate() {
    let value = this.context;
    /* ... */
  }
  componentWillUnmount() {
    let value = this.context;
    /* ... */
  }
  render() {
    let value = this.context;
    /* render something based on the value of MyContext */
  }
}
MyClass.contextType = MyContext;
```
- the contextType property on a class can be assigned a Context object created by React.createContext()
  - lets you consume the nearest current value of that Context type using this.context
* **Context.Consumer**
- A React component that subscribes to context changes.
  - lets you subscribe to a context within a function component
  - Requires a function as a child
* **Context.displayName**
- Context object accepts a displayName string property
- React DevTools uses this string to determine what to display for the context









