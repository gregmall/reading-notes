# Architectural Styles and Architectural Patterns
* purpose of *Architectural Patterns* is to understand how the major parts of a system fit together and how messages and data flow through the system
 ## **Architectural Patterns VS Design Patterns
  - *Design Patterns* impact a specific section of the code base
  - *Architectural Patterns* are high-level strategies that concern large-scale components, the global properties and mechanisms of a system
 ## **Styles and Patterns**
  - *Architectural Pattern* is a way to solve a recurring architectural problem
  - *Architectural Style* is a name given to a recurrent Architectural Design
    - Doesn't exist to solve a problem
## Idiom
* Low-level pattern specific to a programming language
  - Describes how to implement particular aspects of the components or the relationships between them using the features of a given language
## Some major Architectural Patterns and Architectural Patterns Styles
* **Layered**
- Four layers
  - Presentation layer or UI layer
  - Application layer or Service layer
  - Business logic layer or Domain layer
  - Data access layer or Persistence layer
* **Event Driven**
- organizes a system around the production, detection and consumption of events
- event Emitter
  - event source and only knows that the event has occurred
- event Consumer
  - subscribe to an event manager receives notifications when events are emitted and forward events to all registered Consumers
* **Domain Driven Design**
- software based on the Business Domain, its elements and behaviors, and the relationships between them
- eases communication and improves flexibility
* **Pipes and Filters**
- Filter transforms the data it receives through Pipes with which it is connected
- Pipe is some kind of connector that passes data from one Filter to the next
* **Microservices**
- create several tiny programs
- requires every service to be completely independent of the others
# Container and Presentation Pattern
* The container and presentation pattern splits code into two distinct places:
  - containers : are stateful components that contain your business login
  - presentations : are stateless components that present your data
### Containers
* they manage state, fetch data from APIs, setup event handlers, and pass information to other components via props
### Presentations
* receive props and use those props to render and style DOM.
```
my-app
└── src
    ├── assets
    │   └── myImg.png
    ├── components
    │   ├── ComponentName
    │   │   ├── ComponentName.css
    │   │   ├── ComponentName.jsx
    │   │   └── ComponentName.test.jsx
    ├── containers
    │   ├── ContainerName
    │   │   ├── ContainerName.jsx
    │   │   └── ContainerName.test.jsx
    ├── services
    │   └── myService.js
    └── index.jsx
```
# Container Component Details
* responsible for specifying how a section of an application works.
  - they manage state, fetch data from apis and set up event handlers
### Class Containers
* Class container components are created by extending the react Component class.
```
import React, { Component } from 'react';

export default class MyContainer extends Component {

}
```
* **initializing state**
- done in 2 ways
  - class properties
```
import React, { Component } from 'react';

export default class MyContainer extends Component {
  state = {
    someStateField: ''
  }
}
```
  - inside a constructor
```
import React, { Component } from 'react';

export default class MyContainer extends Component {
  constructor(props) {
    super(props);
    this.state = {
      someStateField: ''
    };
  }
}
```
* **Setting State**
- use this.setState
- independent state change:
```
import React, { Component } from 'react';

export default class MyContainer extends Component {
  state = {
    someStateField: ''
  }

  updateSomeState = newSomeState => {
    this.setState({ someStateField: newSomeState });
  }
}
```
- Dependent state change:
```
import React, { Component } from 'react';

export default class MyContainer extends Component {
  state = {
    count: 0
  }

  incrementCount = (by = 1) => {
    this.setState(state => ({ count: state.count + by }));
  }
}
```
* **fetching date**
- using componentDidMount
```
import React, { Component } from 'react';
import { fetchData } from 'src/services/api.js'

export default class MyContainer extends Component {
  state = {
    myData: []
  }

  componentDidMount() {
    fetchData()
      .then(myData => this.setState({ myData }));
  }
}
```
- using componentDidUpdate
```
import React, { Component } from 'react';
import { fetchData } from 'src/services/api.js'

export default class MyContainer extends Component {
  state = {
    page: 1,
    myData: []
  }

  componentDidUpdate(prevProps, prevState) {
    if(prevState.page !== this.state.page) {
      fetchData(this.state.page)
        .then(myData => this.setState({ myData }));
    }
  }
}

## Functional Containers with Hooks

Functional container components can also be written by utilizing react hooks.

 ```js
import React from 'react'

const MyContainer = () => {

}

export default MyContainer;
```
* **Initializing state**
- useState
```
import React, { useState } from 'react'

const MyContainer = () => {
  const [someState, setSomeState] = useState('');
}

export default MyContainer;
```
* **Setting State**
- independent state change
- setSomeState
```
import React, { useState } from 'react'

const MyContainer = () => {
  const [someState, setSomeState] = useState('');

  const handleChange = ({ target }) => setSomeState(target.value);
}

export default MyContainer;
```
- dependent state change
- someState
```
import React, { useState } from 'react'

const MyContainer = () => {
  const [count, setCount] = useState('');

  const increment = (by = 1) => setCount(oldCount => oldCount + by);
}

export default MyContainer;
```
* **Fetching Data**
- useEffect
```
import React, { useState, useEffect } from 'react'
import { fetchData } from 'src/services/api.js'

const MyContainer = () => {
  const [myData, setMyData] = useState([]);

  useEffect(() => {
    fetchData()
      .then(data => setMyData(data));
  }, []);
}

export default MyContainer;
```
### Containers as Hooks
* containers can be written as custom hooks:
```
import { useState, useEffect } from 'react'
import { fetchData } from 'src/services/api.js'

const useMyContainerHook = () => {
  const [myData, setMyData] = useState([]);

  useEffect(() => {
    fetchData()
      .then(data => setMyData(data));
  }, []);

  return myData;
}
```
# Presentation Details
* responsible for specifying how a section of our page looks
### Creating A Presentation Component
* written as functional components
  - return the markup that is going to get rendered to the DOM
```
import React from 'react';
import PropTypes from 'prop-types';

const MyPresentationalComponent = () => (
  <section>
    <h1>My Presentational Component</h1>
    <p>Is great!</p>
  </section>
);

export default MyPresentationalComponent;
```
- pass props into our presentational components in order to make them reusable
```
import React from 'react';
import PropTypes from 'prop-types';

const MyPresentationalComponent = ({ title, body }) => (
  <section>
    <h1>{title}</h1>
    <p>{body}</p>
  </section>
);

MyPresentationalComponent = {
  title: PropTypes.string.isRequired,
  body: PropTypes.string.isRequired
}

export default MyPresentationalComponent;
```
- When we pass props into our component we should use the prop-types package to specify the props our component receives
# Functional vs Class Components
### Differences
* **Syntax**
- functional component is plain javascript function accepting props and returns a react element
- class component requires you to extend from react.component and create a render function
* **State**
- cannot use setState with functional component
  - must be passed state through props
* **Lifecycle Hooks**
- cannot use in functional components
# Conditional Rendering

