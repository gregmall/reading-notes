# Intro to Webpack
* Webpack is a static module bundler.
  - goes through your package and creates what it calls a dependency graph which consists of various modules which your webapp would require to function as expected.
  -  it creates a new package which consists of the very bare minimum number of files required, often just a single bundle.js file which can be plugged in to the html file easily and used for the application

* setting up
  - npm init 
    - create a starter package and add a package.json file
  - npm i react react-dom --save 
    - adds React and ReactDOM libraries
  - npm i webpack webpack-dev-server webpack-cli --save--dev
    -  --save--dev is to specify that these modules are just dev dependencies
  - npm i babel-core babel-loader @babel/preset-react
    - babel, we have loaded the core babel library first, then the loader, and finally 2 plugins or presets to work specifically with React and all the new ES2015 and ES6 onwards code
  * webpack.config.js
    - First we start by requiring the default path module to access the file location and make changes to the file location.
    - Next we require the HTMLWebpackPlugin to generate an HTML file to be used for serving bundled JavaScript file/files

# Webpack Concepts
* webpack is a static module bundler for modern JavaScript applications
  -  it internally builds a dependency graph which maps every module your project needs and generates one or more bundles
## Entry
* An entry point indicates which module webpack should use to begin building out its internal dependency graph
- Example: webpack.config.js
```
module.exports = {
  entry: './path/to/my/entry/file.js'
};
```
## Output
* output property tells webpack where to emit the bundles it creates and how to name these files
  - defaults to ./dist/main.js for the main output file and to the ./dist folder for any other generated file
- Example: webpack.config.js
```
const path = require('path');

module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'my-first-webpack.bundle.js'
  }
};
```
## Loaders
* Loaders allow webpack to process other types of files and convert them into valid modules that can be consumed by your application and added to the dependency graph
- Loaders have tow properties in your webpack configuration
  1. The **test** property identifies which file or files should be transformed.
  2. The **use** property indicates which loader should be used to do the transforming
- Example: webpack.config.js
```
const path = require('path');

module.exports = {
  output: {
    filename: 'my-first-webpack.bundle.js'
  },
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  }
};
```
## Plugins
* Plugins can be leveraged to perform a wider range of tasks like bundle optimization, asset management and injection of environment variables
- Example: webpack.config.js
```
const HtmlWebpackPlugin = require('html-webpack-plugin'); //installed via npm
const webpack = require('webpack'); //to access built-in plugins

module.exports = {
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};
```
## Mode
* By setting the mode parameter to either development, production or none, you can enable webpack's built-in optimizations that correspond to each environment
```
module.exports = {
  mode: 'production'
};
```
## Browser Compatibility
* webpack supports all browsers that are ES5-compliant
- webpack needs Promise for import() and require.ensure()
## Environment
* webpack runs on Node.js version 8.x and higher

# Rendering Elements
* Elements are the smallest building blocks of React apps
## Rendering and Element into the DOM
```
<div id="root"></div>
```
- To render a React element into a root DOM node, pass both to ReactDOM.render():
```
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```
## Updating the Rendering Element
* React elements are immutable
  - Once you create an element, you can’t change its children or attributes
## React Only Updates What's Necessary
* React DOM compares the element and its children to the previous one, and only applies the DOM updates necessary to bring the DOM to the desired state

# React Hello World
* Smallest react example:
```
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
);
```
# Introducing JSX
* JSX is a syntax extension to JavaScript
  - produces React 'elements'. 
  - it is helpful as a visual aid when working with UI inside the JavaScript code.
  - allows react to show more useful error and warning messages.
## Embedding Expressions in JSX
```
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>;

ReactDOM.render(
  element,
  document.getElementById('root')
);
```
- You can put any valid JavaScript expression inside the curly braces in JSX
- example below, we embed the result of calling a JavaScript function, formatName(user), into an <h1> element
```
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};

const element = (
  <h1>
    Hello, {formatName(user)}!
  </h1>
);

ReactDOM.render(
  element,
  document.getElementById('root')
);
```
- We split JSX over multiple lines for readability
## JSX is an Expression Too
* JSX expressions become regular JavaScript function calls and evaluate to JavaScript objects
  - you can use JSX inside of if statements and for loops, assign it to variables, accept it as arguments, and return it from functions
```
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```
## Specifying Attributes with JSX
- You may use quotes to specify string literals as attributes
```
const element = <div tabIndex="0"></div>;
```
- You may also use curly braces to embed a JavaScript expression in an attribute
```
const element = <img src={user.avatarUrl}></img>;
```
- Don’t put quotes around curly braces when embedding a JavaScript expression in an attribute
  - You should either use quotes (for string values) or curly braces (for expressions), but not both in the same attribute
## Specifying Children with JSX
- If a tag is empty, you may close it immediately with />, like XML
```
const element = <img src={user.avatarUrl} />;
```
- JSX tags may contain children
```
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```
## JSX Prevents Injection Attacks
- It is safe to embed user input in JSX
```
const title = response.potentiallyMaliciousInput;
// This is safe:
const element = <h1>{title}</h1>;
```
- React DOM escapes any values embedded in JSX before rendering them
  - ensures that you can never inject anything that’s not explicitly written in your application
## JSX Represents Objects
* Babel compiles JSX down to React.createElement() calls.
- These two examples are identical:
```
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```
```
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```
- React.createElement() performs a few checks to help you write bug-free code but essentially it creates an object like this
```
// Note: this structure is simplified
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!'
  }
};
```
- These objects are called 'React elements'.  
- React reads these objects and uses them to construct the DOM and keep it up to date 