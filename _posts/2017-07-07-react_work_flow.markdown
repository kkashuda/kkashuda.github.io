---
layout: post
title:  "React Work Flow "
date:   2017-07-07 23:44:48 +0000
---


React is a JavaScript library, so it requires a basic understanding of the language. 

### Introducing JSX 

JSX is a syntax extension to JavaScript. Here is an example: 

```
const element = <h1>Hello, world!</h1>;
```

If you want to spread the declaration over multiple lines you can use braces like so: 

```
const element = (
  <h1>
    Hello, world!
  </h1>
);
```

This syntax is used to describe what the UI should look like. It is used to build React elements that are rendered to the DOM. You can also embed expressions using JSX syntax. You do so by wrapping the expression in curly braces. For example: 

```
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};
```

JSX is an expression too. Once compiled, JSX expressions become JavaScript objects. JavaScript objects are hashes: 
```
var car = {type:"Fiat", model:"500", color:"white"};
```

React.createElement() is responsible for creating the JavaScript object. 

```
const element = (
  <h1 className="greeting">
    Hello world!
  </h1>
);
```

boils down to: 

```
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello world!'
  }
};
```

These objects are called "React elements". They describe the data you want to see on the screen. React processes or reads them and uses them to construct the DOM.

Specifying attributes in JSX can be done a couple of ways. You may use quotes to specify string literals as attributes:

```
const element = <div tabIndex="0"></div>;
```

You may also use curly braces to embed a JavaScript expression in an attribute:

```
const element = <img src={user.webURL}></img>;
```

So quotes for *string values* and curly braces for *expressions*. 


#### JSX tags 

If a tag is empty, you may close it immediately with />, like XML:

```
const element = <img src={user.webUrl} />;
```

JSX tags may contain children:

```
const element = (
  <div>
    <h1>Hello World!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```

#### Rendering an Element into the DOM

A react element is the smallest building block of a react Application. They describe what you want to see on the screen. React also has components. Components are made up of React elements. 

Applications built with just React usually have a single root DOM node where elements will be rendered: 

```
<div id="root"></div>
```

To render an element in the root node pass ReactDOM.render() both the root node and the element: 

```
const element = <h1>Hello world!</h1>;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

### Components and Props

Components allow you to split the UI into individual pieces so that you don't have to think about everything at once. Components are similar to JavaScript functions in that they accept arguments known as *props* returning React elements to be displayed on the screen. 

You can define a functional React component using vanilla JS: 

```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

You can also use an ES6 class to define a component:

```
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

Elements can also represent user-defined components:

```
const element = <Welcome name="Kelly" />;
```

React passes JSX attributes to this component as a single object. We call this object "props".

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

1. We call ReactDOM.render() with the ```<Welcome name="Kelly" />``` element.
2. React calls the Welcome component with {name: 'Kelly'} as the props.
3. Our Welcome component returns a ```<h1>Hello, Kelly</h1>``` element as the result.
4. React DOM efficiently updates the DOM to match ```<h1>Hello, Kelly</h1>```.

*Note: Always start component names with a capital letter.
```<div />``` represents a DOM tag, but ```<Welcome />``` represents a component and requires Welcome to be in scope.*


#### Props are Read-Only!

All React components must act like pure functions with respect to their props. Functions are considered "pure" if they always return the same result for the same inputs


# To Be Continued.. 



