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
    -
