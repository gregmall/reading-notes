# Composition vs Inheritance
* **Containment**
- some components don't know their children
- they need to use special children prop to pass children elements into their output
- Example:
```
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}
    </div>
  );
}
```
- this lets other components pass arbitrary children to them by nesting the JSX:
```
function WelcomeDialog() {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        Welcome
      </h1>
      <p className="Dialog-message">
        Thank you for visiting our spacecraft!
      </p>
    </FancyBorder>
  );
}
```
- Anything inside the FancyBorder JSX tag gets passed into the FancyBorder component as a children prop
- Since FancyBorder renders {props.children} inside a div, the passed elements appear in the final output
* **Specialization**
- sometimes components are thought of as being special cases of other components.
- in React, this is achieved by composition where a smore specific component renders a more generic one and configures it with props
- Example:
```
function Dialog(props) {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        {props.title}
      </h1>
      <p className="Dialog-message">
        {props.message}
      </p>
    </FancyBorder>
  );
}

function WelcomeDialog() {
  return (
    <Dialog
      title="Welcome"
      message="Thank you for visiting our spacecraft!" />
  );
}
```
* **So What About Inheritance**
- basically, inheritance is rarely recommended 
- props and composition give you all the flexibility you need



