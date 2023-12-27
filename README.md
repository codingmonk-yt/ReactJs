# What is ReactJS?

ReactJS is an open-source, component based front end library responsible only for the **view layer** of the application. It is maintained by Facebook.

ReactJS uses virtual DOM based mechanism to fill in data (views) in HTML DOM. The virtual DOM works fast owning to the fact that it only changes individual DOM elements instead of reloading complete DOM every time

> A React application is made up of multiple **components**, each responsible for outputting a small, reusable piece of HTML. Components can be nested within other components to
> allow complex applications to be built out of simple building blocks. A component may also maintain internal state - for example, a TabList component may store a variable
> corresponding to the currently open tab.

* React allows us to write components using a domain-specific language called **JSX**. 
* JSX allows us to write our components using HTML, whilst mixing in JavaScript events. 
* React will internally convert this into a virtual DOM, and will ultimately output our HTML for us.

* React "reacts" to state changes in your components quickly and automatically to rerender the components in the HTML DOM by utilizing the virtual DOM.
* The virtual DOM is an in-memory representation of an actual DOM. By doing most of the processing inside the virtual DOM rather than directly in the browser's DOM, React can act quickly and only add, update, and remove components which have changed since the last render cycle occurred.

## Section 1.2: Installation or Setup

ReactJS is a JavaScript library contained in a single file react-<version>.js that can be included in any HTML page. People also commonly install the React DOM library react-dom-<version>.js along with the main React file:

### Basic Inclusion

```html
<!DOCTYPE html>
<html>
    <head></head>
    <body>
    <script type="text/javascript" src="/path/to/react.js"></script>
    <script type="text/javascript" src="/path/to/react-dom.js"></script>
    <script type="text/javascript">
      // Use react JavaScript code here or in a separate file
    </script>
    </body>
</html>
```

To get the JavaScript files, go to [the installation page](https://facebook.github.io/react/docs/installation.html) of the official React documentation.

React also supports [JSX syntax](https://facebook.github.io/react/docs/jsx-in-depth.html). JSX is an extension created by Facebook that adds XML syntax to JavaScript. In order
to use JSX you need to include the Babel library and change <script type="text/babel"> in order to translate JSX to Javascript code.

```html
<!DOCTYPE html> <html>
<head></head>
  <body>
  <script type="text/javascript" src="/path/to/react.js"></script>
  <script type="text/javascript" src="/path/to/react-dom.js"></script>
  <script src="https://npmcdn.com/babel-core@5.8.38/browser.min.js"></script>
  <script type="text/babel">
        // Use react JSX code here or in a separate file
  </script>
    </body>
</html>
```

### Installing via npm

You can also install React using [npm](https://www.npmjs.com/) by doing the following:

```sh
npm install --save react react-dom
```
To use React in your JavaScript project, you can do the following:

```js
let React = require('react');
let ReactDOM = require('react-dom');
ReactDOM.render(<App />, ...);
```

### Installing via Yarn

Facebook released its own package manager named [Yarn](https://yarnpkg.com/), which can also be used to install React. 

After installing Yarn you just need to run this command:

```sh
yarn add react react-dom
```

You can then use React in your project in exactly the same way as if you had installed React via npm.

## Section 1.3: Hello World with Stateless Functions

Stateless components are getting their philosophy from functional programming. Which implies that: 
A function returns all time the same thing exactly on what is given to it.

### For example:

```js
const statelessSum = (a, b) => a + b;
let a = 0;
const statefulSum = () => a++;
```

* As you can see from the above example that, statelessSum is always will return the same values given a and b. However, statefulSum function will not return the same values given even no parameters.
* This type of function's behaviour is also called as a side-effect. Since, the component affects somethings beyond.
* So, it is advised to use stateless components more often, since they are side-effect free and will create the same behaviour always.
* That is what you want to be after in your apps because fluctuating state is the worst case scenario for a maintainable program.
* The most basic type of react component is one without state. React components that are pure functions of their props and do not require any internal state management can be written as simple JavaScript functions.
* These are said to be Stateless Functional Components because they are a function only of props, without having any state to keep track of.

Here is a simple example to illustrate the concept of a Stateless Functional Component:

```jsx
// In HTML
<div id="element"></div>

// In React
const MyComponent = props => {
return <h1>Hello, {props.name}!</h1>;
};
ReactDOM.render(<MyComponent name="Arun" />, element); // Will render <h1>Hello, Arun!</h1>
```

Note that all that this component does is render an h1 element containing the name prop. This component doesn't keep track of any state. Here's an ES6 example as well:

```jsx
import React from 'react'
const HelloWorld = props => ( <h1>Hello, {props.name}!</h1>
)

HelloWorld.propTypes = {
    name: React.PropTypes.string.isRequired
}
export default HelloWorld
```

## Section 1.4: Absolute Basics of Creating Reusable Components

### Components and Props

* As React concerns itself only with an application's view, the bulk of development in React will be the creation of components.
* A component represents a portion of the view of your application. "Props" are simply the attributes used on a JSX node (e.g.```jsx
  <SomeComponent someProp="some prop's value" /> ```), and are the primary way our application interacts with our components.
* In the snippet above, inside of SomeComponent, we would have access to this.props, whose value would be the object {someProp: "some prop's value"}.

* It can be useful to think of React components as simple functions - they take input in the form of "props", and produce output as markup.
*  Many simple components take this a step further, making themselves "Pure Functions", meaning they do not issue side effects, and are idempotent (given a set of inputs, the component will always produce the same output).
*  This goal can be formally enforced by actually creating components as functions, rather than "classes".
*  There are three ways of creating a React component:

**1. Functional ("Stateless") Components**

```jsx
const FirstComponent = props => (
  <div>{props.content}</div>
);
```

**2.React.createClass()**

```jsx
const SecondComponent = React.createClass({
  render: function () {
    return (
      <div>{this.props.content}</div>
    );
  }
});
```

**3.ES2015 Classes**
```jsx
class ThirdComponent extends React.Component {
    render() {
      return (
        <div>{this.props.content}</div>
    );
  }
}
```

These components are used in exactly the same way:

```jsx
const ParentComponent = function (props) {
  const someText = "FooBar";
  return (
    <FirstComponent content={someText} />
    <SecondComponent content={someText} />
    <ThirdComponent content={someText} />
  );
}
```

The above examples will all produce identical markup.

* Functional components cannot have "state" within them. So if your component needs to have a state, then go for class based components. Refer Creating Components for more information.
* As a final note, react props are immutable once they have been passed in, meaning they cannot be modified from within a component. 
* If the parent of a component changes the value of a prop, React handles replacing the old props with the new, the component will rerender itself using the new values.


## Section 1.5: Create React App

[create-react-app](https://github.com/facebookincubator/create-react-app) is a React app boilerplate generator created by Facebook. It provides a development environment configured for ease-of-use with minimal setup, including:

* ES6 and JSX transpilation
* Dev server with hot module reloading
* Code linting
* CSS auto-prefixing
* Build script with JS, CSS and image bundling, and sourcemaps Jest testing framework

### Installation

First, install create-react-app globally with node package manager (npm).

```sh
npm install -g create-react-app
```

Then run the generator in your chosen directory.

```sh
create-react-app my-app
```

Navigate to the newly created directory and run the start script.

```sh
cd my-app/
npm start
```

### Configuration

create-react-app is intentionally non-configurable by default. If non-default usage is required, for example, to use a compiled CSS language such as Sass, then the eject command can be used.

```sh
npm run eject
```

This allows editing of all configuration files. N.B. this is an irreversible process.

### Build React App

To build your app for production ready, run following command

```sh
npm run build
```

## Section 1.6: Hello World

### Without JSX

Here's a basic example that uses React's main API to create a React element and the React DOM API to render the React element in the browser.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Hello React!</title>
    <!-- Include the React and ReactDOM libraries -->
    <script src="https://fb.me/react-15.2.1.js"></script>
    <script src="https://fb.me/react-dom-15.2.1.js"></script>
  </head>
  <body>
    <div id="example"></div>
    <script type="text/javascript">
      // create a React element rElement
      let rElement = React.createElement('h1', null, 'Hello, world!'); // dElement is a DOM container
      let dElement = document.getElementById('example'); // render the React element in the DOM container
      ReactDOM.render(rElement, dElement);
    </script>
  </body>
</html>
```

### With JSX

Instead of creating a React element from strings one can use JSX (a Javascript extension created by Facebook for adding XML syntax to JavaScript), which allows to write

```js
let rElement = React.createElement('h1', null, 'Hello, world!');
```

as the equivalent (and easier to read for someone familiar with HTML)

```jsx
let rElement = <h1>Hello, world!</h1>;
```

The code containing JSX needs to be enclosed in a **<script type="text/babel">** tag. Everything within this tag will be transformed to plain Javascript using the Babel library (that needs to be included in addition to the React libraries).

So finally the above example becomes:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Hello React!</title>
    <!-- Include the React and ReactDOM libraries -->
    <script src="https://fb.me/react-15.2.1.js"></script>
    <script src="https://fb.me/react-dom-15.2.1.js"></script>
    <!-- Include the Babel library -->
    <script src="https://npmcdn.com/babel-core@5.8.38/browser.min.js"></script>
  </head>
  <body>
   <div id="example"></div>
    <script type="text/babel">
      // create a React element rElement using JSX
      let rElement = <h1>Hello, world!</h1>; // dElement is a DOM container
      let dElement = document.getElementById('example'); // render the React element in the DOM container
      ReactDOM.render(rElement, dElement);
    </script>
  </body>
</html>
```

## Section 1.7: Hello World Component

* A React component can be defined as an ES6 class that extends the base React.Component class.
* In its minimal form, a component must define a render method that specifies how the component renders to the DOM.
* The render method returns React nodes, which can be defined using JSX syntax as HTML-like tags.
* The following example shows how to define a minimal Component:

```js
import React from 'react'
class HelloWorld extends React.Component {
    render() {
      return <h1>Hello, World!</h1>
    }
}
export default HelloWorld
```

* A Component can also receive props. These are properties passed by its parent in order to specify some values the component cannot know by itself; a property can also contain a function that can be called by the component after certain events occur - for example, a button could receive a function for its onClick property and call it whenever it is clicked.
* When writing a component, its props can be accessed through the props object on the Component itself:

```js
import React from 'react'
class Hello extends React.Component {
    render() {
      return <h1>Hello, {this.props.name}!</h1>
    }
}
export default Hello
```

* The example above shows how the component can render an arbitrary string passed into the name prop by its parent. 

* Note that a component cannot modify the props it receives.

* A component can be rendered within any other component, or directly into the DOM if it's the topmost component, using ReactDOM.render and providing it with both the component and the DOM Node where you want the React tree to be rendered:

```jsx
import React from 'react'
import ReactDOM from 'react-dom'
import Hello from './Hello'

ReactDOM.render(<Hello name="Billy James" />, document.getElementById('main'))
```

By now you know how to make a basic component and accept props. Lets take this a step further and introduce state.

For demo sake, let's make our Hello World app, display only the first name if a full name is given.

```jsx
import React from 'react'
class Hello extends React.Component {
    constructor(props){
      //Since we are extending the default constructor, //handle default activities first.
      super(props);
      //Extract the first-name from the prop
      let firstName = this.props.name.split(" ")[0];
      //In the constructor, feel free to modify the //state property on the current context. this.state = {
      name: firstName
    }
}
//Look maa, no comma required in JSX based class defs!
render() {
    return <h1>Hello, {this.state.name}!</h1>
  }
}
export default Hello
```

**Note**: Each component can have it's own state or accept it's parent's state as a prop.

_____________

# Components

## Section 2.1: Creating Components

This is an extension of Basic Example:

### Basic Structure

```ts
import React, { Component } from 'react';
import { render } from 'react-dom';
class FirstComponent extends Component {
    render() {
        return ( <div>
                    Hello, {this.props.name}! I am a FirstComponent. </div>
               );
    }
}
render(
    <FirstComponent name={ 'User' } />,
    document.getElementById('content')
);
```

The above example is called a **stateless** component as it does not contain state (in the React sense of the word).

In such a case, some people find it preferable to use Stateless Functional Components, which are based on [ES6
arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions).

### Stateless Functional Components

- In many applications there are smart components that hold state but render dumb components that simply receive props and return HTML as JSX.
- Stateless functional components are much more reusable and have a positive performance impact on your application.

They have 2 main characteristics:

1. When rendered they receive an object with all the props that were passed down.
2. They must return the JSX to be rendered.

```ts
// When using JSX inside a module you must import React
import React from 'react';
import PropTypes from 'prop-types';
const FirstComponent = props => (
    <div>
        Hello, {props.name}! I am a FirstComponent.
    </div>
);
//arrow components also may have props validation
FirstComponent.propTypes = {
    name: PropTypes.string.isRequired,
}
// To use FirstComponent in another file it must be exposed through an export call:
export default FirstComponent;
```

### Stateful Components

In contrast to the 'stateless' components shown above, 'stateful' components have a state object that can be updated with the setState method. The state must be initialized in the constructor before it can be set:

```ts
import React, { Component } from 'react';

class SecondComponent extends Component {
    constructor(props) {
        super(props);

            this.state = {
                toggle: true
            };
            // This is to bind context when passing onClick as a callback

            this.onClick = this.onClick.bind(this);
    }
    onClick() {
            this.setState((prevState, props) => ({
                toggle: !prevState.toggle
            }));
    }
    render() {
        return (
            <div onClick={this.onClick}>
                Hello, {this.props.name}! I am a SecondComponent.
                <br />
                Toggle is: {this.state.toggle}
            </div>
        );
    }
}
```

- Extending a component with [PureComponent](https://facebook.github.io/react/docs/react-api.html#react.purecomponent) instead of Component will automatically implement the shouldComponentUpdate() lifecycle method with shallow prop and state comparison.
- This keeps your application more performant by reducing the amount of un-necessary renders that occur. This assumes your components are 'Pure' and always render the same output with the same state and props input.

### Higher Order Components

Higher order components (HOC) allow to share component functionality.

```ts
import React, { Component } from 'react';
const PrintHello = ComposedComponent => class extends Component {
    onClick() {
        console.log('hello');
    }

    /* The higher order component takes another component as a parameter
    and then renders it with additional props */
    render() {
        return <ComposedComponent {...this.props } onClick={this.onClick} />
    }
}

const FirstComponent = props => (
    <div onClick={ props.onClick }>
        Hello, {props.name}! I am a FirstComponent.
    </div>
);

const ExtendedComponent = PrintHello(FirstComponent);
```

Higher order components are used when you want to share logic across several components regardless of how different they render.

## Section 2.2: Basic Component

Given the following HTML file:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>React Tutorial</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/react/15.2.1/react.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/react/15.2.1/react-dom.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.34/browser.min.js"></script>
  </head>
  <body>
    <div id="content"></div>
    <script type="text/babel" src="scripts/example.js"></script>
  </body>
</html>
```

You can create a basic component using the following code in a separate file:

### scripts/example.js

```jsx
import React, { Component } from 'react';
import ReactDOM from 'react-dom';
class FirstComponent extends Component {
  render() {
    return (
        <div className="firstComponent">
            Hello, world! I am a FirstComponent.
        </div>
    );
  }
}
ReactDOM.render(
<FirstComponent />, // Note that this is the same as the variable you stored above
  document.getElementById('content')
);
```

You will get the following result (note what is inside of div#content):

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>React Tutorial</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/react/15.2.1/react.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/react/15.2.1/react-dom.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.34/browser.min.js"></script>
  </head>
  <body>
        <div id="content">
            <div className="firstComponent">
                Hello, world! I am a FirstComponent.
            </div>
        </div>
        <script type="text/babel" src="scripts/example.js"></script>
    </body>
</html>
```

## Section 2.3: Nesting Components

A lot of the power of ReactJS is its ability to allow nesting of components. Take the following two components:

```jsx
let React = require('react');
let createReactClass = require('create-react-class');

let CommentList = reactCreateClass({
    render: function() {
        return (
            <div className="commentList">
                Hello, world! I am a CommentList.
            </div>
        );
    }
});
let CommentForm = reactCreateClass({
    render: function() {
        return (
            <div className="commentForm">
                Hello, world! I am a CommentForm.
            </div>
        );
    }
});
```

You can nest and refer to those components in the definition of a different component:

```jsx
let React = require('react');
let createReactClass = require('create-react-class');
let CommentBox = reactCreateClass({
        render: function() {
            return (
                <div className="commentBox">
                    <h1>Comments</h1>
                    <CommentList /> // Which was defined above and can be reused
                    <CommentForm /> // Same here
                </div>
            );
        }
});
```

### 1. Nesting without using children

(continued from above)

```jsx
let CommentList = reactCreateClass({
    render: function() {
        return (
            <div className="commentList">
                <ListTitle/>
                Hello, world! I am a CommentList.
            </div>
        );
    }
});
```

This is the style where A composes B and B composes C.

#### Pros

- Easy and fast to separate UI elements
- Easy to inject props down to children based on the parent component's state

#### Cons

- Less visibility into the composition architecture
- Less reusability
  
#### Good if

- B and C are just presentational components
- B should be responsible for C's lifecycle


### 2. Nesting using children

(continued from above)

```jsx
let CommentBox = reactCreateClass({
    render: function() {
        return (
            <div className="commentBox">
                <h1>Comments</h1>
                <CommentList>
                    <ListTitle/> // child
                </CommentList>
                <CommentForm />
              </div>
        );
    }
});
```

This is the style where A composes B and A tells B to compose C. More power to parent components.

#### Pros

- Better components lifecycle management
- Better visibility into the composition architecture
- Better reusuability


#### Cons

- Injecting props can become a little expensive
- Less flexibility and power in child components

#### Good if

- B should accept to compose something different than C in the future or somewhere else
- A should control the lifecycle of C

* B would render C using this.props.children, and there isn't a structured way for B to know what those children are for.
* So, B may enrich the child components by giving additional props down, but if B needs to know exactly what they are, #3 might be a better option.

### 3. Nesting using props

(continued from above)

```jsx
let CommentBox = reactCreateClass({
    render: function() {
        return (
            <div className="commentBox">
                <h1>Comments</h1>
                <CommentList title={ListTitle}/> //prop <CommentForm />
            </div>
        );
    }
});
```

This is the style where A composes B and B provides an option for A to pass something to compose for a specific purpose. More structured composition.

#### Pros

- Composition as a feature
- Easy validation
- Better composaiblility

#### Cons

- Injecting props can become a little expensive
- Less flexibility and power in child components

#### Good if

- B has specific features defined to compose something
- B should only know how to render not what to render

#3 is usually a must for making a public library of components but also a good practice in general to make composable components and clearly define the composition features. #1 is the easiest and fastest to make something that works, but #2 and #3 should provide certain benefits in various use cases.

## Section 2.4: Props

Props are a way to pass information into a React component, they can have any type including functions - sometimes referred to as callbacks.

In JSX props are passed with the attribute syntax

```jsx
<MyComponent userID={123} />
```

Inside the definition for MyComponent userID will now be accessible from the props object

```jsx
// The render function inside MyComponent
render() {
    return (
        <span>The user's ID is {this.props.userID}</span>
    )
}
```

It's important to define all props, their types, and where applicable, their default value:

```jsx
// defined at the bottom of MyComponent
MyComponent.propTypes = {
    someObject: React.PropTypes.object,
    userID: React.PropTypes.number.isRequired,
    title: React.PropTypes.string
};
MyComponent.defaultProps = {
    someObject: {},
    title: 'My Default Title'
}
```

- In this example the prop someObject is optional, but the prop userID is required.
- If you fail to provide userID to MyComponent, at runtime the React engine will show a console warning you that the required prop was not provided.
- Beware though, this warning is only shown in the development version of the React library, the production version will not log any warnings.

Using defaultProps allows you to simplify

```jsx
const { title = 'My Default Title' } = this.props;
console.log(title);
```

to 

```jsx
console.log(this.props.title);
```

It's also a safeguard for use of object array and functions. If you do not provide a default prop for an object, the following will throw an error if the prop is not passed:

```jsx
if (this.props.someObject.someKey)
```

In example above, this.props.someObject is undefined and therefore the check of someKey will throw an error and the code will break. With the use of defaultProps you can safely use the above check.

## Section 2.5: Component states - Dynamic user-interface

Suppose we want to have the following behaviour - We have a heading (say h3 element) and on clicking it, we want it to become an input box so that we can modify heading name. React makes this highly simple and intuitive using component states and if else statements. (Code explanation below)

```jsx
// I have used ReactBootstrap elements. But the code works with regular html elements also
let Button = ReactBootstrap.Button;
let Form = ReactBootstrap.Form;

let FormGroup = ReactBootstrap.FormGroup;
let FormControl = ReactBootstrap.FormControl;

let Comment = reactCreateClass({
    getInitialState: function() {
        return {show: false, newTitle: ''};
    },

    handleTitleSubmit: function() {
        //code to handle input box submit - for example, issue an ajax request to change name in database
    },

    handleTitleChange: function(e) {

        //code to change the name in form input box. newTitle is initialized as empty string. We need to update it with the string currently entered by user in the form
        this.setState({newTitle: e.target.value});
    },
    changeComponent: function() {
        // this toggles the show variable which is used for dynamic UI this.setState({show: !this.state.show)};
    },

render: function() {

    let clickableTitle;
    if(this.state.show) {
        clickableTitle = <Form inline onSubmit={this.handleTitleSubmit}>
                            <FormGroup controlId="formInlineTitle">
                                <FormControl type="text" onChange={this.handleTitleChange}>
                            </FormGroup>
                         </Form>;
    } else {
        clickabletitle = <div>
                            <Button bsStyle="link" onClick={this.changeComponent}>
                                <h3> Default Text </h3>
                            </Button>
                        </div>;
        }
        return (
            <div className="comment">
                {clickableTitle}
            </div>
        );
    }
});
ReactDOM.render(
    <Comment />, document.getElementById('content')
);
```

- The main part of the code is the **clickableTitle** variable. Based on the state variable **show**, it can be either be a Form element or a Button element. React allows nesting of components.
- So we can add a {clickableTitle} element in the render function. It looks for the clickableTitle variable. Based on the value 'this.state.show', it displays the corresponding element.

## Section 2.6: Variations of Stateless Functional Components

```js
const languages = [
    'JavaScript',
    'Python',
    'Java',
    'Elm',
    'TypeScript',
    'C#',
    'F#'
]
```

```js
// one liner
const Language = ({language}) => <li>{language}</li>

Language.propTypes = {
  message: React.PropTypes.string.isRequired
}
```

```js
/**
* If there are more than one line.
* Please notice that round brackets are optional here, * However it's better to use them for readability
*/
const LanguagesList = ({languages}) => {
      <ul>
        {languages.map(language => <Language language={language} />)}
      </ul>
}
LanguagesList.PropTypes = {
  languages: React.PropTypes.array.isRequired
}
```

```jsx
/**
 * This syntax is used if there are more work beside just JSX presentation
 * For instance some data manipulations needs to be done.
 * Please notice that round brackets after return are required,
 * Otherwise return will return nothing (undefined)
 */
const LanguageSection = ({header, languages}) => {
// do some work
const formattedLanguages = languages.map(language => language.toUpperCase()) return (
    <fieldset>
      <legend>{header}</legend>
      <LanguagesList languages={formattedLanguages} />
    </fieldset>
  )
}
LanguageSection.PropTypes = {
  header: React.PropTypes.string.isRequired,
  languages: React.PropTypes.array.isRequired
}
ReactDOM.render(
  <LanguageSection
    header="Languages"
    languages={languages}
  />,
  document.getElementById('app')
)
```

## Section 2.7: setState pitfalls

You should use caution when using setState in an asynchronous context. For example, you might try to call setState in the callback of a get request:

```jsx
class MyClass extends React.Component {
    constructor() {
        super();

        this.state = {
            user: {}
        };
    }

    componentDidMount() {
        this.fetchUser();
    }

    fetchUser() {
        $.get('/api/users/self')
            .then((user) => {
                this.setState({user: user});
        });
    }
    render() {
        return <h1>{this.state.user}</h1>;
    }
}
```

This could call problems - if the callback is called after the Component is dismounted, then this.setState won't be a function. Whenever this is the case, you should be careful to ensure your usage of setState is cancellable.

In this example, you might wish to cancel the XHR request when the component dismounts:

```jsx
class MyClass extends React.Component {
    constructor() {
        super();
        this.state = {
            user: {},
            xhr: null
        };
    }

    componentWillUnmount() {
        let xhr = this.state.xhr;

        // Cancel the xhr request, so the callback is never called
        if (xhr && xhr.readyState != 4) {
            xhr.abort();
        }    
    }
    componentDidMount() {
        this.fetchUser();
    }
    fetchUser() {
        let xhr = $.get('/api/users/self')
                    .then((user) => {
                        this.setState({user: user});
                    });
                this.setState({xhr: xhr});
    }
}
```

The async method is saved as a state. In the componentWillUnmount you perform all your cleanup - including canceling the XHR request.

You could also do something more complex. In this example, I'm creating a 'stateSetter' function that accepts the this object as an argument and prevents this.setState when the function cancel has been called:

```jsx
function stateSetter(context) {
    var cancelled = false;
    return {
        cancel: function () {
            cancelled = true;
        },
        setState(newState) {
            if (!cancelled) {
                context.setState(newState);
            }
        }
    }
}
class Component extends React.Component {
    constructor(props) {
    super(props);
    this.setter = stateSetter(this);
    this.state = {
            user: 'loading'
        };
    }
    componentWillUnmount() {
        this.setter.cancel();
    }
    componentDidMount() {
        this.fetchUser();
    }
    fetchUser() {
        $.get('/api/users/self')
            .then((user) => {
                this.setter.setState({user: user});
        });
    }
    render() {
        return <h1>{this.state.user}</h1>
    }
}
```

This works because the cancelled variable is visible in the setState closure we created.

------------------




