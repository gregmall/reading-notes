# Understanding React 'setState'
## Workings of 'setState()'
* setState() is the only legitimate way to update state after the initial state setup
```
import React, { Component } from 'react'

class Search extends Component {
  constructor(props) {
    super(props)

    state = {
      searchTerm: ''
    }
  }
}
```
- passing an empty string as a value and, to update the state of searchTerm, we have to call setState()
```
setState({ searchTerm: event.target.value })
```
- The object contains the part of the state we want to update which, in this case, is the value of searchTerm
  - React takes this value and merges it into the object that needs it
* Reconciliation
  - the way React updates the DOM, by making changes to the component based on the change in state
## Passing a function to 'setState()'
```
lass App extends React.Component {

state = { count: 0 }

handleIncrement = () => {
  this.setState({ count: this.state.count + 1 })
}

handleDecrement = () => {
  this.setState({ count: this.state.count - 1 })
}
  render() {
    return (
      <div>
        <div>
          {this.state.count}
        </div>
        <button onClick={this.handleIncrement}>Increment by 1</button>
        <button onClick={this.handleDecrement}>Decrement by 1</button>
      </div>
    )
  }
}
```
- call setState() three times in the handleDecrement and handleIncrement functions like this:
```
handleIncrement = () => {
  this.setState((prevState) => ({ count: prevState.count + 1 }))
  this.setState((prevState) => ({ count: prevState.count + 1 }))
  this.setState((prevState) => ({ count: prevState.count + 1 }))
}
```

## Access Previous State Using Updater
* You cannot always trust this.state to hold the correct state immediately after calling setState(), as it is always equal to the state rendered on the screen

# Lists and Keys
* **Rendering multiple components**
- You can build collections of elements and include them in JSX using curly braces {}
* **Basic list component**
- Usually you would render lists inside a component
```
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li>{number}</li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```
- assign a key to our list items inside numbers.map() and fix the missing key issue.
```
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>
      {number}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```
## Keys
* Keys help React identify which items have changed, are added, or are removed
  - should be given to the elements inside the array to give the elements a stable identity:
```
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);
```
* **Extracting Components with Keys**
- Keys only make sense in the context of the surrounding array
```
function ListItem(props) {
  // Correct! There is no need to specify the key here:
  return <li>{props.value}</li>;
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // Correct! Key should be specified inside the array.
    <ListItem key={number.toString()} value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```
* **Keys Must Only be Unique Among Siblings**
- Keys used within arrays should be unique among their siblings. However they don’t need to be globally unique. 
- We can use the same keys when we produce two different arrays:
```
function Blog(props) {
  const sidebar = (
    <ul>
      {props.posts.map((post) =>
        <li key={post.id}>
          {post.title}
        </li>
      )}
    </ul>
  );
  const content = props.posts.map((post) =>
    <div key={post.id}>
      <h3>{post.title}</h3>
      <p>{post.content}</p>
    </div>
  );
  return (
    <div>
      {sidebar}
      <hr />
      {content}
    </div>
  );
}

const posts = [
  {id: 1, title: 'Hello World', content: 'Welcome to learning React!'},
  {id: 2, title: 'Installation', content: 'You can install React from npm.'}
];
ReactDOM.render(
  <Blog posts={posts} />,
  document.getElementById('root')
);
```
* **Embedding map() in JSX**
- JSX allows embedding any expression in curly braces so we could inline the map() result:
```
function NumberList(props) {
  const numbers = props.numbers;
  return (
    <ul>
      {numbers.map((number) =>
        <ListItem key={number.toString()}
                  value={number} />
      )}
    </ul>
  );
}
```

# Typechecking With PropTypes
* To run typechecking on the props for a component, you can assign the special propTypes property:
```
import PropTypes from 'prop-types';

class Greeting extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}

Greeting.propTypes = {
  name: PropTypes.string
};
```
- PropTypes exports a range of validators that can be used to make sure the data you receive is valid
* **PropTypes**
- Here is an example documenting the different validators provided:
```
import PropTypes from 'prop-types';

MyComponent.propTypes = {
  // You can declare that a prop is a specific JS type. By default, these
  // are all optional.
  optionalArray: PropTypes.array,
  optionalBool: PropTypes.bool,
  optionalFunc: PropTypes.func,
  optionalNumber: PropTypes.number,
  optionalObject: PropTypes.object,
  optionalString: PropTypes.string,
  optionalSymbol: PropTypes.symbol,

  // Anything that can be rendered: numbers, strings, elements or an array
  // (or fragment) containing these types.
  optionalNode: PropTypes.node,

  // A React element.
  optionalElement: PropTypes.element,

  // A React element type (ie. MyComponent).
  optionalElementType: PropTypes.elementType,
  
  // You can also declare that a prop is an instance of a class. This uses
  // JS's instanceof operator.
  optionalMessage: PropTypes.instanceOf(Message),

  // You can ensure that your prop is limited to specific values by treating
  // it as an enum.
  optionalEnum: PropTypes.oneOf(['News', 'Photos']),

  // An object that could be one of many types
  optionalUnion: PropTypes.oneOfType([
    PropTypes.string,
    PropTypes.number,
    PropTypes.instanceOf(Message)
  ]),

  // An array of a certain type
  optionalArrayOf: PropTypes.arrayOf(PropTypes.number),

  // An object with property values of a certain type
  optionalObjectOf: PropTypes.objectOf(PropTypes.number),

  // An object taking on a particular shape
  optionalObjectWithShape: PropTypes.shape({
    color: PropTypes.string,
    fontSize: PropTypes.number
  }),
  
  // An object with warnings on extra properties
  optionalObjectWithStrictShape: PropTypes.exact({
    name: PropTypes.string,
    quantity: PropTypes.number
  }),   

  // You can chain any of the above with `isRequired` to make sure a warning
  // is shown if the prop isn't provided.
  requiredFunc: PropTypes.func.isRequired,

  // A value of any data type
  requiredAny: PropTypes.any.isRequired,

  // You can also specify a custom validator. It should return an Error
  // object if the validation fails. Don't `console.warn` or throw, as this
  // won't work inside `oneOfType`.
  customProp: function(props, propName, componentName) {
    if (!/matchme/.test(props[propName])) {
      return new Error(
        'Invalid prop `' + propName + '` supplied to' +
        ' `' + componentName + '`. Validation failed.'
      );
    }
  },

  // You can also supply a custom validator to `arrayOf` and `objectOf`.
  // It should return an Error object if the validation fails. The validator
  // will be called for each key in the array or object. The first two
  // arguments of the validator are the array or object itself, and the
  // current item's key.
  customArrayProp: PropTypes.arrayOf(function(propValue, key, componentName, location, propFullName) {
    if (!/matchme/.test(propValue[key])) {
      return new Error(
        'Invalid prop `' + propFullName + '` supplied to' +
        ' `' + componentName + '`. Validation failed.'
      );
    }
  })
};
```
* **Requiring Single Child**
- With PropTypes.element you can specify that only a single child can be passed to a component as children
```
import PropTypes from 'prop-types';

class MyComponent extends React.Component {
  render() {
    // This must be exactly one element or it will warn.
    const children = this.props.children;
    return (
      <div>
        {children}
      </div>
    );
  }
}

MyComponent.propTypes = {
  children: PropTypes.element.isRequired
};
```
* **Default Prop Values**
- You can define default values for your props by assigning to the special defaultProps property:
```
class Greeting extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}

// Specifies the default values for props:
Greeting.defaultProps = {
  name: 'Stranger'
};

// Renders "Hello, Stranger":
ReactDOM.render(
  <Greeting />,
  document.getElementById('example')
);
```
- If you are using a Babel transform like transform-class-properties , you can also declare defaultProps as static property within a React component class
```
class Greeting extends React.Component {
  static defaultProps = {
    name: 'stranger'
  }

  render() {
    return (
      <div>Hello, {this.props.name}</div>
    )
  }
}
```
- The defaultProps will be used to ensure that this.props.name will have a value if it was not specified by the parent component.

# Components and Props
* Components let you split the UI into independent, reusable pieces, and think about each piece in isolation
## Function and Class Components
```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```
- class defined 
```
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```
- The above two components are equivalent from React’s point of view
## Rendering a Component
```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```
## Composing Components
- Components can refer to other components in their output
```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```
## Extracting Components
 * Basically, we can extract components in nested divs in React to simplify 
 ## Props are Read-Only
 * Whether you declare a component as a function or a class, it must never modify its own props

# Handling Events
* React events are named using camelCase, rather than lowercase.
* With JSX you pass a function as the event handler, rather than a string.
```
function ActionLink() {
  function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
  }

  return (
    <a href="#" onClick={handleClick}>
      Click me
    </a>
  );
}
```
## Passing Arguments to Event Handlers
* Inside a loop, it is common to want to pass an extra parameter to an event handler. For example, if id is the row ID, either of the following would work:
```
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this, id)}>Delete Row</button>
```
# Snapshot Testing
* very useful tool whenever you want to make sure your UI does not change unexpectedly

* **Snapshot Testing with Jest**
- A similar approach can be taken when it comes to testing your React components.
- Instead of rendering the graphical UI, which would require building the entire app, you can use a test renderer to quickly generate a serializable value for your React tree
* **Updating Snapshots**
- snapshot test case is failing because the snapshot for  updated component no longer matches the snapshot artifact for this test case
- To resolve this, we will need to update our snapshot artifacts:
```
jest --updateSnapshot
```
* **Interactive Snapshot Mode**
- Failed snapshots can also be updated interactively in watch mode
- Once you enter Interactive Snapshot Mode, Jest will step you through the failed snapshots one test at a time and give you the opportunity to review the failed output
- From here you can choose to update that snapshot or skip to the next
* **inline Snapshots**
- behave identically to external snapshots except the snapshot values are written automatically back into the source code
* **Property Matchers**
- Jest allows providing an asymmetric matcher for any property
- These matchers are checked before the snapshot is written or tested, and then saved to the snapshot file instead of the received value
- Any given value that is not a matcher will be checked exactly and saved to the snapshot
* **Best Practices**
1. Treat snapshots as code
  - Commit snapshots and review them as part of your regular code review process
  -Ensure that your snapshots are readable by keeping them focused, short, and by using tools that enforce these stylistic conventions
2. Tests should be deterministic
  - Running the same tests multiple times on a component that has not changed should produce the same results every time
  - You're responsible for making sure your generated snapshots do not include platform specific or other non-deterministic data
3. Use descriptive snapshot names
  - Always strive to use descriptive test and/or snapshot names for snapshots
  - The best names describe the expected snapshot content
# React Testing Library
* The react-testing-library is a very light-weight solution for testing React components
- It provides light utility functions on top of react-dom and react-dom/test-utils, in a way that encourages better testing practices
- tests work with DOM nodes
- basic example:
```
// hidden-message.js
import React from 'react'
// NOTE: React Testing Library works with React Hooks _and_ classes just as well
// and your tests will be the same however you write your components.
function HiddenMessage({children}) {
  const [showMessage, setShowMessage] = React.useState(false)
  return (
    <div>
      <label htmlFor="toggle">Show Message</label>
      <input
        id="toggle"
        type="checkbox"
        onChange={e => setShowMessage(e.target.checked)}
        checked={showMessage}
      />
      {showMessage ? children : null}
    </div>
  )
}
export default HiddenMessage
// __tests__/hidden-message.js
// These imports are something you'd normally configure Jest to import for you automatically.
// Learn more in the setup docs: https://testing-library.com/docs/react-testing-library/setup#skipping-auto-cleanup
import '@testing-library/jest-dom/extend-expect'
// NOTE: jest-dom adds handy assertions to Jest and is recommended, but not required
import {render, screen} from '@testing-library/react'
import userEvent from '@testing-library/user-event'
import React from 'react'
import HiddenMessage from '../hidden-message'
test('shows the children when the checkbox is checked', () => {
  const testMessage = 'Test Message'
  render(<HiddenMessage>{testMessage}</HiddenMessage>)
  // query* functions will return the element or null if it cannot be found
  // get* functions will return the element or throw an error if it cannot be found
  expect(screen.queryByText(testMessage)).toBeNull()
  // the queries can accept a regex to make your selectors more resilient to content tweaks and changes.
  userEvent.click(screen.getByLabelText(/show/i))
  // .toBeInTheDocument() is an assertion that comes from jest-dom
  // otherwise you could use .toBeDefined()
  expect(screen.getByText(testMessage)).toBeInTheDocument()
})
```
- practical example:
```
// login.js
import React from 'react'
function Login() {
  const [state, setState] = React.useReducer((s, a) => ({...s, ...a}), {
    resolved: false,
    loading: false,
    error: null,
  })
  function handleSubmit(event) {
    event.preventDefault()
    const {usernameInput, passwordInput} = event.target.elements
    setState({loading: true, resolved: false, error: null})
    window
      .fetch('/api/login', {
        method: 'POST',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify({
          username: usernameInput.value,
          password: passwordInput.value,
        }),
      })
      .then(r => r.json())
      .then(
        user => {
          setState({loading: false, resolved: true, error: null})
          window.localStorage.setItem('token', user.token)
        },
        error => {
          setState({loading: false, resolved: false, error: error.message})
        },
      )
  }
  return (
    <div>
      <form onSubmit={handleSubmit}>
        <div>
          <label htmlFor="usernameInput">Username</label>
          <input id="usernameInput" />
        </div>
        <div>
          <label htmlFor="passwordInput">Password</label>
          <input id="passwordInput" type="password" />
        </div>
        <button type="submit">Submit{state.loading ? '...' : null}</button>
      </form>
      {state.error ? <div role="alert">{state.error.message}</div> : null}
      {state.resolved ? (
        <div role="alert">Congrats! You're signed in!</div>
      ) : null}
    </div>
  )
}
export default Login
// __tests__/login.js
// again, these first two imports are something you'd normally handle in
// your testing framework configuration rather than importing them in every file.
import '@testing-library/jest-dom/extend-expect'
import {render, screen} from '@testing-library/react'
import userEvent from '@testing-library/user-event'
import React from 'react'
import Login from '../login'
test('allows the user to login successfully', async () => {
  // mock out window.fetch for the test
  const fakeUserResponse = {token: 'fake_user_token'}
  jest.spyOn(window, 'fetch').mockImplementationOnce(() => {
    return Promise.resolve({
      json: () => Promise.resolve(fakeUserResponse),
    })
  })
  render(<Login />)
  // fill out the form
  userEvent.type(screen.getByLabelText(/username/i), 'chuck')
  userEvent.type(screen.getByLabelText(/password/i), 'norris')
  userEvent.click(screen.getByText(/submit/i))
  // just like a manual tester, we'll instruct our test to wait for the alert
  // to show up before continuing with our assertions.
  const alert = await screen.findByRole('alert')
  // .toHaveTextContent() comes from jest-dom's assertions
  // otherwise you could use expect(alert.textContent).toMatch(/congrats/i)
  // but jest-dom will give you better error messages which is why it's recommended
  expect(alert).toHaveTextContent(/congrats/i)
  expect(window.localStorage.getItem('token')).toEqual(fakeUserResponse.token)
})
```




