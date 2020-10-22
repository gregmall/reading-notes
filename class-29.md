# Model View Controller
* Software design pattern
  - divides related program logic into three interconnected elements.
### Components
**Model**
- The central component of the pattern
**View**
- representation of data(chart, diagram, table)
**Controller**
- accepts input, converts it to commands for the model or view
### History
- MVC became one of the first approaches to describe and implement software constructs in terms of their responsibilities
- The MVC pattern has subsequently evolved,[14] giving rise to variants such as hierarchical model–view–controller
- MVC web frameworks now hold large market-shares relative to non-MVC web toolkits
### Use in web applications
- MVC has been widely adopted as a design for World Wide Web applications in major programming languages
- Some web MVC frameworks take a thin client approach that places almost the entire model, view and controller logic on the server
# 4 Layers of Single Page Applications You Need to Know
* **Presentational Components**
  - receive state through props 
  - emit new state through events
* **Container components**
  - receive state from the store
  - supply state to presentational components
  - send new state to the store
* **Application Services**
- project (interpret) state
- orchestrate external operations
* **Store**
  - holds the state
  - state is immutable
  - acts as a publisher
  - notifies subscribers about state changes
* **Domain**
  - represents the state
* **Domain Services**
  - encapsulate business logic
  - side-effect free
# React MVC
### Implementing MVC Patterns in React
* **Presentation Layer of controller and View React Components**
- categorize by components
  1. controller components
    - knows a lot about the rest of the world
    - knows how to access and update “domain data” (application state) and how to choose and execute “domain logic”
  2. view components
    - A view component shouldn’t know anything about application state (reading or writing), network protocols, or non-UI providers farther up the chain
* Views and controllers are both allowed to have their own state, but state in views is only for UI purposes.

### UI-Agnostic Data Model
```
function App() {
  return <EditCustomer id={1} />;
}

function EditCustomer({ id }) {
  let { customers, dispatch } = useCustomers(); // access context and probably trigger side effects

  let customer = customers.find(c => c.id === customerId);
  if (!customer) {
    return <NotFound />;
  }

  let [errors, setErrors] = React.useState()
  let [saving, setSaving] = React.useState(false)
  let [name, setName] = React.useState(customer.name);
  let [email, setEmail] = React.useState(customer.email);

  let saveCustomer = () => {
    setSaving(true)
    fetch({
      url: `/api/customers/${id}`,
      method: "PUT",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ name, email })
    })
      .then(response => response.json())
      .then(apiCustomer => {
        // Formatting for differences between backend and frontend
        //   e.g. Rails/Django snake_case into JavaScript camelCase
        dispatch({
          type: "UPDATE_CUSTOMER",
          payload: formatChangeForFrontend(apiCustomer)
        });
      })
      .catch(error => {
        setErrors(error)
      });
      .finally(() => {
        setSaving(false)
      })
  };

  return (
    <div>
      {errors && <ErrorDisplay errors={errors} />}
      <input
        type="text"
        name="name"
        value={name}
        onChange={e => setName(e.target.value)}
      />
      <input
        type="text"
        name="email"
        value={email}
        onChange={e => setEmail(e.target.value)}
      />
      <button onClick={saveCustomer} disabled={saving}>Save</button>
    </div>
  );
}
```
* Refactor to controller-view pattern
```
function App() {
  return (
    <EditCustomerController id={1} />;
  )
}

// Notice explicit suffix "Controller"
function EditCustomerController({ id }) {
  let { customers, dispatch } = useCustomers();

  let customer = customers.find(c => c.id === id);
  if (!customer) {
    return <NotFound />;
  }

  let onSave = (newCustomerData) => {
    return fetch({
      url: `/api/customers/${id}`,
      method: "PUT",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify(newCustomerData)
    })
      .then(response => response.json())
      .then(apiCustomer => {
        // Formatting for differences between backend and frontend
        //   e.g. Rails/Django snake_case into JavaScript camelCase
        dispatch({
          type: "UPDATE_CUSTOMER",
          payload: formatChangeForFrontend(apiCustomer)
        });
      })
  };

  return <CustomerForm onSave={onSave} initialName={customer.name} initialEmail={customer.email} />
}

// Notice no special name; just a React component that knows about React things
function CustomerForm({onSave, initialName, initialEmail}) {
  let [errors, setErrors] = React.useState()
  let [saving, setSaving] = React.useState(false)
  let [name, setName] = React.useState(initialName);
  let [email, setEmail] = React.useState(initialEmail);

  let onSaveWrapped = () => {
    setSaving(true)
    onSave({name, email})
      .catch((error) => {
        setErrors(error)
      })
      .finally(() => {
        setSaving(false)
      })
  }

  return (
    <div>
      {errors && <ErrorDisplay errors={errors} />}
      <input
        type="text"
        name="name"
        value={name}
        onChange={e => setName(e.target.value)}
      />
      <input
        type="text"
        name="email"
        value={email}
        onChange={e => setEmail(e.target.value)}
      />
      <button onClick={onSaveWrapped} disabled={saving}>Save</button>
    </div>
  );
}
```
### Contrast: Container and Presentation Components
* Container and Presentational Components came from Dan Abramov, and the idea has been important in the Redux community
-  Controller == Container && View == Presentational

# Reconciliation
* React provides a declarative API so that you don’t have to worry about exactly what changes on every update
### The Diffing Algorithm
* **Elements Of Different Types**
- Whenever the root elements have different types, React will tear down the old tree and build the new tree from scratch
- When tearing down a tree, old DOM nodes are destroyed
* **DOM elements Of The Same Type**
- When comparing two React DOM elements of the same type, React looks at the attributes of both, keeps the same underlying DOM node, and only updates the changed attributes
* **Component Elements Of The Same Type**
- When a component updates, the instance stays the same, so that state is maintained across renders
- React updates the props of the underlying component instance to match the new element, and calls componentWillReceiveProps() and componentWillUpdate() on the underlying instance
* **Recursing On Children**
- By default, when recursing on the children of a DOM node, React just iterates over both lists of children at the same time and generates a mutation whenever there’s a difference.
* **Keys**
- In order to solve this issue, React supports a key attribute. When children have keys, React uses the key to match children in the original tree with children in the subsequent tree




