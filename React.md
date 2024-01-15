
Notes from https://www.freecodecamp.org/news/the-react-handbook-b71c27b0a795/#variables

1. we load both React and React DOM. Why 2 libraries? \
   Because React is 100% independent from the browser and can be used outside it (for example on Mobile devices with React Native). Hence the need for React DOM, to add the wrappers for the browser.

**NPX**
- npx is a very cool way to run Node code, and provides many useful features. If you don’t want to install npm, you can install npx as a standalone package


- npx create-react-app todolist --> to create an react application with name 'todolist'
    - It creates file structure and initialize Git Repo
    - includes few commands, npm start -- to run application \
          --  npm build: to build the React application files in the build folder, ready to be deployed to a server \
          --  npm test: to run the testing suite using Jest \
          --  npm eject: to eject from create-react-app  \
                When you eject the action is irreversible. You will get 2 new folders in your application directory, config and scripts. Those contain the configurations - and now you can start editing them
      

**Javascript**
- A variable must be declared before you can use it. There are 3 ways to do this, using var, let or const, and those 3 ways differ in how you can interact with the variable later on.
- Var:
    - If you forget to add var you will be assigning a value to an undeclared variable, and the results might vary.
    - var a //typeof a === 'undefined'
      
| Feature             | `var`                  | `let`                          | `const`                        |
|---------------------|------------------------|--------------------------------|--------------------------------|
| **Scope**           | Function-scoped        | Block-scoped                   | Block-scoped                   |
| **Hoisting**        | Yes                    | Yes                            | Yes                            |
| **Reassignment**    | Allowed                | Allowed                        | Not allowed (except for objects and arrays)   |
| **Redeclaration**   | Allowed                | Not allowed                    | Not allowed                    |
| **Initialization**  | Undefined until assigned | Undefined until assigned       | Undefined until assigned       |

**Examples:**

1. **var:**
   ```javascript
   var x = 10;
   if (true) {
     var x = 20;
   }
   console.log(x); // Output: 20
   
2. **let:**
   ```javascript
    let y = 30;
    if (true) {
      let y = 40;
    }
    console.log(y); // Output: 30

3. **const:**
   ```javascript
    const z = 50;
    if (true) {
      const z = 60;
    }
    console.log(z); // Output: 50

**Arrow functions**
```
const myFunction = function() {
  //...
}
``` 
to
```
const myFunction = () => {
  //...
}
```
```
const myFunction = () => doSomething() // if its single line
```
```
const myFunction = (param1, param2) => doSomething(param1, param2) /// for params 
```
```
const myFunction = param => doSomething(param) // for a single param, no need of paranthesis
```

- Arrow functions allow you to have an implicit return: values are returned without having to use the return keyword.

when returning an object, remember to wrap the curly brackets in parentheses to avoid it being considered the wrapping function body brackets.
```
const myFunction = () => ({ value: 'test' })
myFunction() //{value: 'test'}
```


In summary, the behavior of the `this` keyword in arrow functions differs significantly from regular functions in JavaScript. Here are the key points:

1. **Regular Functions and `this`:**
   - In a regular function, when used as a method of an object (like a method in an object literal), `this` refers to the object.
   - Regular functions bind `this` to the object they are called on.

   ```javascript
   const car = {
     model: 'Fiesta',
     manufacturer: 'Ford',
     fullName: function() {
       return `${this.manufacturer} ${this.model}`;
     }
   };
   ```

2. **Arrow Functions and `this`:**
   - Arrow functions do not bind `this` at all; instead, they inherit it from the execution context.
   - Arrow functions do not have their own `this` value; they look up `this` in the call stack.

   ```javascript
   const car = {
     model: 'Fiesta',
     manufacturer: 'Ford',
     fullName: () => {
       return `${this.manufacturer} ${this.model}`;
     }
   };
   ```

3. **Limitations of Arrow Functions:**
   - Arrow functions are not suitable for use as object methods due to their handling of `this`.
   - They cannot be used as constructors, and attempting to instantiate an object will result in a TypeError.
   - Arrow functions are not ideal for scenarios requiring dynamic context, such as handling events.

   ```javascript
   link.addEventListener('click', () => {
     // this === window (undesirable behavior)
   });

   link.addEventListener('click', function() {
     // this === link (desired behavior)
   });
   ```

In practical terms, when dealing with dynamic contexts like object methods, constructors, or event handlers that rely on the value of `this`, it is recommended to use regular functions instead of arrow functions. Regular functions provide a more predictable behavior in these scenarios.

**Rest and spread**:

You can expand an array, an object or a string using the spread operator ....
```
const a = [1, 2, 3]
const b = [...a, 4, 5, 6]
const c = [...a] // cloning

const newObj = { ...oldObj } //Clone an object
const hey = 'hey'
const arrayized = [...hey] // ['h', 'e', 'y']

The `rest element` is useful when working with array destructuring:

const numbers = [1, 2, 3, 4, 5]
[first, second, ...others] = numbers
```

```
const { first, second, ...others } = {
  first: 1,
  second: 2,
  third: 3,
  fourth: 4,
  fifth: 5
}

first // 1
second // 2
others // { third: 3, fourth: 4, fifth: 5 }
----------------------------
const [first, second, , , fifth] = a
```

**template literal**:

Once a template literal is opened with the backtick, you just press enter to create a new line, with no special characters, and it’s rendered as-is:
```
const string = `Hey
this
string
is awesome!`
```

### CallBacks:

JavaScript is synchronous by default and is single threaded. This means that code cannot create new threads and run in parallel.

A callback is a simple function that’s passed as a value to another function, and will only be executed when the event happens. We can do this because JavaScript has first-class functions, which can be assigned to variables and passed around to other functions (called higher-order functions)

**Disadvantage:**
Callbacks are great for simple cases!
  - However every callback adds a level of nesting, and when you have lots of callbacks, the code starts to be complicated very quickly.

 XHR requests also accept a callback, in this example by assigning a function to a property that will be called when a particular event occurs (in this case, the state of the request changes):

```
const xhr = new XMLHttpRequest()
xhr.onreadystatechange = () => {
  if (xhr.readyState === 4) {
    xhr.status === 200 ? console.log(xhr.responseText) : console.error('error')
  }
}
xhr.open('GET', 'https://yoursite.com')
xhr.send()
```
**Handling errors in callbacks**
One very common strategy is to use what Node.js adopted: the first parameter in any callback function is the error object: error-first callbacks

If there is no error, the object is null. If there is an error, it contains some description of the error and other information.

```
fs.readFile('/file.json', (err, data) => {
  if (err !== null) {
    //handle error
    console.log(err)
    return
  }
  
  //no errors, process data
  console.log(data)
})
```

JavaScript introduced several features that help us with asynchronous code that do not involve using callbacks:

- Promises (ES6)
- Async/Await (ES8)

# React:

### Summary of Single Page Applications (SPAs)
- React applications are often referred to as Single Page Applications (SPAs).
- In the past, traditional web pages were loaded from the server for every user interaction, resulting in a slower user experience.

### Modern Approach:
- SPAs, popularized by frameworks like React, load the application code (HTML, CSS, JavaScript) only once.
- Instead of loading new pages from the server, SPAs use JavaScript to handle user interactions without completely refreshing the page, creating a more desktop application-like experience.

Examples: Notable examples of SPAs include Gmail, Google Maps, Facebook, Twitter, and Google Drive.

 **Pros:**
- SPAs provide a faster user experience with instant feedback and improved UX.
- Server resource consumption is reduced as the focus shifts to efficient API development.
- Ideal for building mobile apps on top of the API, promoting code reuse.
- Easily transformable into Progressive Web Apps (PWAs) for local caching and offline support.

**Cons:**
- Not suitable for SEO-dependent applications, as search engines may struggle to index SPAs.
- Requires careful management of JavaScript, as SPAs can remain open for extended periods, leading to potential memory issues.
- Great for team collaboration, allowing backend developers to focus on the API while frontend developers enhance the user experience.

**Considerations:**
- SPAs heavily rely on JavaScript, potentially causing poor experiences on low-power devices.
- Accessibility and user experience need to be considered, especially for visitors with JavaScript disabled.

### Overriding the Navigation

In Single Page Applications (SPAs), default browser navigation is replaced, requiring manual URL management through a router.
Frameworks like Ember handle this automatically, while React may use libraries like React Router.

**The Problem:**
Initially, managing URLs in SPAs was an afterthought, leading to the "broken back button" issue. Since the browser navigation was overridden, the URL didn't change when navigating within the application. Pressing the back button could unexpectedly take users to a previously visited website.

**Solution:**
This problem can be addressed using the History API provided by browsers, or through libraries like React Router that internally leverage the History API.

### Declarative

React is often described as a declarative approach to building UIs. This declarative nature is not a new concept but has been popularized by React, influencing the frontend development world.

**Key Aspects:**
- **Building Without Direct DOM Interaction:**
  React allows building web interfaces without directly manipulating the DOM.

- **Event System Abstraction:**
  React provides an event system without requiring direct interaction with DOM events.

**Declarative vs. Imperative:**
The declarative approach contrasts with the imperative approach, where actions are explicitly specified. For example, jQuery or direct DOM event handling is imperative, instructing the browser on exactly what to do. React's declarative approach abstracts these complexities, letting developers specify how they want components to be rendered without direct DOM interaction.
 


**Higher order components**
  - When a component receives a component as a prop and returns a component, it’s called higher order component.

**Why is the Virtual DOM helpful: batching**

The key thing is that React batches much of the changes and performs a unique update to the real DOM, by changing all the elements that need to be changed at the same time, so the repaint and reflow the browser must perform to render the changes are executed just once.

### Unidirectional Data Flow in React

- Unidirectional Data Flow is a fundamental concept not exclusive to React but crucial for JavaScript developers working with the framework.

- **In React:**
  - Data has only one path for transfer within the application.
  - State is passed to the view and child components.
  - Actions are triggered by the view, and they can update the state.
  - The updated state is then propagated to the view and child components.

- **Key Characteristics:**
  - View is a reflection of the application state.
  - Changes in state occur only through triggered actions.
  - One-way bindings prevent data flow in the opposite direction, ensuring:
    - Reduced error proneness.
    - Simplified debugging with clear data origin tracking.
    - Improved efficiency, as the library can delineate system boundaries.

- **Component Interaction:**
  - Each component owns its state, and data affected by this state can only impact its children.
  - Changing state on a component does not affect its parent, siblings, or any other component in the application.
  - States are often moved up the component tree for shared accessibility among components that require access.


**JSX**: is a technology that was introduced by React.
what you are really doing when using JSX syntax is writing a declarative syntax of what a component UI should be.
  - And you’re describing that UI not using strings, but instead using JavaScript, which allows you to do many nice things.


The render() function can only return a single node, so in case you want to return 2 siblings, just add a parent. It can be any tag, not just div.

**Transpiling JSX**
- JSX must be transpiled to regular JavaScript for browsers to execute it.
- Babel is a popular tool for JSX transpilation.
- JSX is optional; corresponding plain JavaScript alternatives exist for every JSX line.
- Key advantages of JSX include conciseness and readability compared to plain JS syntax.
- If you don’t use `create-react-app` you need to setup Babel yourself.

**Bind this in methods**
If you use class components, don’t forget to bind methods. The methods of ES6 classes by default are not bound. What this means is that this is not defined unless you define methods as arrow functions:

```
class Converter extends React.Component {
  handleClick = e => {
    /* ... */
  }
  //...
}
```
**Also when using the the property initializer syntax with Babel (enabled by default in create-react-app), otherwise you need to bind it manually in the constructor:**
```
class Converter extends React.Component {
  constructor(props) {
    super(props)
    this.handleClick = this.handleClick.bind(this)
  }
  handleClick(e) {}
}
```





**JSX Syntax**
- JSX resembles HTML but follows XML syntax.
- Differences include self-closing tags and camelCase attribute names.
- Class becomes className, and for becomes htmlFor in JSX.

**CSS in React**
- JSX provides a unique way to define CSS using inline styles.
- Styles are defined as objects, allowing for encapsulation within components.
- JSX CSS values differ from plain CSS, using camelCased property names.
`onchange => onChange`
`onclick => onClick`

**Forms in JSX**
- JSX introduces changes to HTML forms for developer convenience.
- Value attribute holds the current value; defaultValue holds the default value.
- Consistent onChange function subscription across various form fields.

**JSX Best Practices**
- JSX enforces automatic escaping to mitigate XSS exploits.
- White space rules include trimming horizontal white space to 1 and eliminating vertical white space.
- Adding comments in JSX uses standard JavaScript comment syntax.
- Spread attributes simplify assigning values to JSX attributes using the ES6 spread operator.
Ex: for spread: 
```
<div>
  <BlogPost title={data.title} date={data.date} />
</div>
    to 
<div>
  <BlogPost {...data} />
</div>
```

**Looping in JSX**
- Looping in JSX involves creating a loop and adding JSX elements to an array.
- Use map or for-of loops to directly render JSX elements in the component.

### Components
- In React, everything is a component, even plain HTML tags.
- Components can be built using function components, class components, or the older React.createClass syntax.
- Class components were traditionally used for state management, but React Hooks have made function components more powerful.

**State**:
- The object can contain a subset, or a superset, of the state. Only the properties you pass will be mutated, the ones omitted will be left in their current state.

- The reason is that using this method, React knows that the state has changed. It will then start the series of events that will lead to the Component being re-rendered, along with any DOM update.

- Because of the **Unidirectional Data Flow rule**, if two components need to share state, the state needs to be moved up to a common ancestor.

**Presentational vs container components**

Presentational components are mostly concerned with generating some markup to be outputted. They don’t manage any kind of state, except for state related the the presentation

Container components are mostly concerned with the “backend” operations.

As a way to simplify the distinction, we can say presentational components are concerned with the look, container components are concerned with making things work.

**React Fragment**
Notice how return values wrap in a div. This is because a component can only return one single element, and if you want more than one, you need to wrap it with another container tag.

This, however, causes an unnecessary div in the output. You can avoid this by using React.Fragment. which also has a very nice shorthand syntax <></> that is supported only in recent releases.
```js
import React, { Component } from 'react'

class BlogPostExcerpt extends Component {
  render() {
    return (
      <React.Fragment>
        <h1>{this.props.title}</h1>
        <p>{this.props.description}</p>
      </React.Fragment>
    )
  }
}
or 
    return (
      <>
        <h1>{this.props.title}</h1>
        <p>{this.props.description}</p>
      </>
    )


```
## React Component Lifecycle

There are 3 phases in a React component lifecycle:

- Mounting
- Updating
- Unmounting

### Mounting Phase
When mounting a component in React, there are four key lifecycle methods that are executed before the component is mounted in the DOM.

**1. Constructor:**
- The constructor is the first method called during component mounting.
- It is used to set up the initial state using `this.state = ...`.

**2. getDerivedStateFromProps():**
- Introduced in React 16.3 to replace the deprecated `componentWillReceiveProps` method.
- Used when the state depends on props, allowing updates to the state based on prop values.
- A static method without access to `this`.
- Should be a pure method without side effects, returning an object with updated state elements (or null if the state doesn't change).

**3. render():**
- This method returns JSX that builds the component interface.
- A pure method that should not cause side effects and consistently return the same output with the same input.

**4. componentDidMount():**
- This method is utilized for API calls or operations on the DOM after the component has been successfully mounted.
- Ideal for performing tasks that require access to the DOM or initiating asynchronous operations.

*Purpose*: Executed after a component is successfully mounted. \
*Tasks:* Perform DOM-related operations, initiate API calls, set up subscriptions. \
*State Update:* Can be used for immediate state updates but be cautious due to potential performance issues. \
*Best Practices:* Prefer assigning initial state in constructor(), use componentDidMount() for tasks requiring access to the DOM or asynchronous operations.


### Updating: 
When updating you have 5 lifecycle methods before the component is mounted in the DOM: the getDerivedStateFromProps, shouldComponentUpdate, render, getSnapshotBeforeUpdate and componentDidUpdate.

1. getDerivedStateFromProps():
    - Invoked before rendering during the update phase.
    - Used to update state based on props.
    - A pure method with no access to this.
    - Returns an object with updated state elements or null.

2. shouldComponentUpdate():
    - Returns a boolean (true or false) to inform React whether to proceed with rerendering.
    - Defaults to true. and Primarily used as a performance optimization.
    - Invoked before rendering with new props or state.
    Often replaced with PureComponent for shallow comparisons of props and state.
    - Avoid deep equality checks or using JSON.stringify() in shouldComponentUpdate().
    - Returning false may skip subsequent lifecycle methods.
3. render():

    - Renders the JSX that builds the updated component interface.
    - A pure method that should not cause side effects.
    - Called after getDerivedStateFromProps() and shouldComponentUpdate().
4. getSnapshotBeforeUpdate():

    - Invoked right before the most recently rendered output is committed to the DOM.
    - Access to props and state from the previous and current render.
    - Niche use case, often less utilized.
    - Allows capturing information from the DOM before potential changes.
    - Returned value passed as a parameter to componentDidUpdate().
5. componentDidUpdate():

    - Called immediately after updating occurs in the DOM.
    - Good for operating on the DOM, handling network requests, or calling APIs.
    - Receives prevProps, prevState, and an optional snapshot parameter.
    - setState() can be called but must be wrapped in a conditional to avoid infinite loops.
    - Not invoked if shouldComponentUpdate() returns false.

### Unmounting
  In this phase we only have one method, componentWillUnmount.

1. componentWillUnmount()
The method is called when the component is removed from the DOM. Use this to do any sort of cleanup you need to perform.

*componentWillMount, componentWillReceiveProps or componentWillUpdate are deprecated*


### **Forms in React:**

- React enhances form interactivity and dynamism, offering two main approaches: controlled components and uncontrolled components.

- Controlled Components:
    - The component state is the single source of truth.
      Data is managed by React components, and form fields are controlled using the value and onChange attributes.
    - Textareas and select tags follow the same controlled component pattern.

- Uncontrolled Components:
    - Some form fields, like `<input type="file">`, are inherently uncontrolled.
    - In uncontrolled components, the state is stored in the DOM, and data is accessed using React refs.
``` js
class FileInput extends React.Component {
  constructor(props) {
    super(props)
    this.curriculum = React.createRef()
    this.handleSubmit = this.handleSubmit.bind(this)
  }

  handleSubmit(event) {
    alert(this.curriculum.current.files[0].name)
    event.preventDefault()
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <input type="file" ref={this.curriculum} />
        <input type="submit" value="Submit" />
      </form>
    )
  }
}
```
### Referencing a DOM Element in React
- In certain scenarios, you may need to directly access the DOM element represented by a React component, for tasks like integrating with external libraries or performing specific DOM manipulations.

**How to Reference a DOM Element:**
- In JSX, use the `ref` attribute to assign the reference of the DOM element to a component property.
  ```jsx
  <button ref={el => this.button = el} />
  ```
- For class components, use `this` to access the component's property.
  ```jsx
  class SomeComponent extends Component {
    render() {
      return <button ref={el => this.button = el} />;
    }
  }
  ```
- For function components, use a local variable.
  ```jsx
  function SomeComponent() {
    let button;
    return <button ref={el => button = el} />;
  }
  ```

**Usage:**
- The referenced DOM element can be utilized within the component's lifecycle methods or other methods for direct interaction with the DOM.
- Example: Accessing the button element in a class component.
  ```jsx
  class SomeComponent extends Component {
    componentDidMount() {
      // Access the button element
      console.log(this.button);
    }

    render() {
      return <button ref={el => this.button = el} />;
    }
  }
  ```

- Directly accessing the DOM should be a last resort. Whenever possible, leverage React's virtual DOM abstraction.
- Ensure that accessing the DOM directly is necessary and cannot be achieved through React state or props.

### Server Side Rendering (SSR) in React

**Benefits of SSR:**
1. *Faster Initial Load:*  SSR improves the first page load time, enhancing the user experience.
2. *SEO Enhancement:* Enables better SEO as search engines can efficiently index server-rendered content.
3. *Social Media Sharing:* Facilitates sharing on social media platforms by providing necessary metadata for link previews.

**Drawbacks of SSR:**
1. *Increased Complexity:* Complexity grows with application complexity.
2. *Resource-Intensive:* Rendering large applications server-side can be resource-intensive and may become a bottleneck.

**SSR Implementation Basics:**
1. **Dependencies:**
   - Utilizes Express for basic SSR implementation.
   - Dependencies include Express, React, ReactDOMServer.

2. **Implementation Steps:**
   - Create an Express server.
   - Use `ReactDOMServer.renderToString()` to render React components server-side.
   - Replace the root div in the HTML template with the server-rendered content.
   - Serve static files using Express.

3. **Code Example (Server-Side):**
   ```jsx
   // Server-Side Rendering with Express and React
   import express from 'express';
   import React from 'react';
   import ReactDOMServer from 'react-dom/server';
   import App from '../src/App';

   const serverRenderer = (req, res, next) => {
     // Read HTML template
     fs.readFile(path.resolve('./build/index.html'), 'utf8', (err, data) => {
       if (err) return res.status(500).send('An error occurred');
       return res.send(
         data.replace(
           '<div id="root"></div>',
           `<div id="root">${ReactDOMServer.renderToString(<App />)}</div>`
         )
       );
     });
   };

   // Express setup, routing, and static file serving
   const app = express();
   const router = express.Router();
   router.use('^/$', serverRenderer);
   router.use(express.static(path.resolve(__dirname, '..', 'build'), { maxAge: '30d' }));
   app.use(router);
   ```

4. **Client-Side Adjustments:**
   - Replace `ReactDOM.render()` with `ReactDOM.hydrate()` in the client application.
   ```jsx
   // Client-Side Rendering Adjustment
   ReactDOM.hydrate(<App />, document.getElementById('root'))
   ```

5. **Babel and Node Transpilation:**
   - Transpile Node.js code using Babel for JSX and ES Modules.
   - Install Babel packages: `@babel/register`, `@babel/preset-env`, `@babel/preset-react`, `ignore-styles`.

*Limitations of Basic Approach:*
1. *Handling Images:* Basic approach doesn't handle rendering images correctly when using imports.
2. *Page Metadata:* Does not handle page header metadata crucial for SEO and social sharing.

### The Context API in React**
- The Context API is designed for efficiently passing state across an app without relying extensively on props.
- Recommended for scenarios where numerous levels of children need to access the shared state.

**How It Works:**
1. **Create Context:**
   - Use `React.createContext()` to create a Context object.
   ```jsx
   const { Provider, Consumer } = React.createContext();
   ```

2. **Wrapper Component (Provider):**
   - Build a wrapper component that returns a `Provider` component, encapsulating the components requiring access to the context.
   ```jsx
   class Container extends React.Component {
     constructor(props) {
       super(props)
       this.state = {
         something: 'hey'
       }
     }
   
     render() {
       return (
         <Provider value={{ state: this.state }}>{this.props.children}</Provider>
       )
     }
   }
   ```

3. **Consumer Usage:**
   - Inside a component wrapped in a `Provider`, utilize a `Consumer` component to access and use the context.
   ```jsx
   class Button extends React.Component {
     render() {
       return (
         <Consumer>
           {context => <button>{context.state.something}</button>}
         </Consumer>
       )
     }
   }
   ```

4. **Updating Context State:**
   - Functions can be passed into the `Provider` value to update the context state.
   ```jsx
   <Provider value={{
     state: this.state,
     updateSomething: () => this.setState({ something: 'ho!' })
   }}>
     {this.props.children}
   </Provider>

   <Consumer>
     {(context) => (
       <button onClick={context.updateSomething}>{context.state.something}</button>
     )}
   </Consumer>
   ```

5. **Multiple Contexts:**
   - Create multiple contexts to distribute state across components while ensuring accessibility.
   ```jsx
   // context.js
   import React from 'react'
   export default React.createContext()

   // component1.js
   import Context from './context'
   // ... use Context.Provider

   // component2.js
   import Context from './context'
   // ... use Context.Consumer
   ```

**Considerations:**
- The React team suggests using props for simple scenarios and reserving Context API for more complex state-sharing requirements.
- Context API can potentially replace Redux in certain scenarios, simplifying the app structure.

### Higher Order Components (HOCs) in React**
- Higher Order Components (HOCs) are a concept borrowed from Higher Order Functions in JavaScript, adapted for React components.
- HOCs in React take a component as input and return a component as output, allowing for composability, reusability, and encapsulation.

*Purpose of HOCs:*
   - Enhance existing components, operate on state or props, or modify rendered markup.
   - Useful for code that needs to be composable, reusable, and encapsulated.

*Naming Convention:*
   - HOCs typically follow the convention of being prepended with the word "with," such as `withButton` for a `Button` component.

**Examples HOC:**
1. **Simplest HOC:**  Basic HOC that returns the component unaltered.
   ```jsx
   const withElement = Element => () => <Element />
   ```

2. **HOC with Additional Property:**  A more useful HOC that adds a property (e.g., color) to the component.
   ```jsx
   const withColor = Element => props => <Element {...props} color="red" />
   ```

**Implementation Example:**
   ```jsx
   const Button = () => <button>test</button>
   const ColoredButton = withColor(Button)

   function App() {
     return (
       <div className="App">
         <h1>Hello</h1>
         <ColoredButton />
       </div>
     )
   }
   ```
### Render Props in React**

- Render Props is a design pattern in React used for sharing state between components.
- It addresses the limitation of accessing the state of the parent component from its children when using the traditional children prop.

**Using Children Prop:**
   - The children prop automatically injects JSX passed in the parent component into the children's position.
 ```jsx
   class Parent extends React.Component {
     render() {
       return <div>{this.props.children}</div>
     }
   }

   const Children1 = () => {}
   const Children2 = () => {}

   const App = () => (
     <Parent>
       <Children1 />
       <Children2 />
     </Parent>
   )
   ```

**Limitation:** The state of the parent component cannot be accessed from the children components using the children prop.

**Implementing Render Props:**
1. **Render Prop Component:**
   - Use a render prop component by passing a function as a prop, which is then executed inside the parent component to share its state.
   ```jsx
   class Parent extends React.Component {
     constructor(props) {
       super(props)
       this.state = { name: 'Flavio' }
     }

     render() {
       return <div>{this.props.children(this.state.name)}</div>
     }
   }
   ```

2. **Using Render Props:**
   - Children components can now access the parent's state by providing a function as a child of the Parent component.
   ```jsx
   const Children1 = props => {
     return <p>{props.name}</p>
   }

   const App = () => <Parent>{name => <Children1 name={name} />}</Parent>
   ```

3. **Multiple Render Props:**
   - The pattern can be used multiple times on the same component, providing different render functions.
   ```jsx
   class Parent extends React.Component {
     constructor(props) {
       super(props)
       this.state = { name: 'Flavio', age: 35 }
     }

     render() {
       return (
         <div>
           <p>Test</p>
           {this.props.someprop1(this.state.name)}
           {this.props.someprop2(this.state.age)}
         </div>
       )
     }
   }

   const Children1 = props => {
     return <p>{props.name}</p>
   }

   const Children2 = props => {
     return <p>{props.age}</p>
   }

   const App = () => (
     <Parent
       someprop1={name => <Children1 name={name} />}
       someprop2={age => <Children2 age={age} />}
     />
   )
   ```

**Conclusion:**
- Render Props is a powerful pattern for sharing state between components in a more flexible and controlled manner.
- It overcomes the limitation of the children prop, allowing components to access and interact with the state of the parent component.
- The pattern enhances component composability and reusability.

### React Hooks Overview
- React Hooks were introduced in React 16.7 to enhance the functionality of functional components.
- They provide a way for functional components to manage state, handle lifecycle events, and perform side effects, making them more powerful and feature-rich.

**Accessing State with useState:**
Using the useState() API, you can create a new state variable, and have a way to alter it. useState() accepts the initial value of the state item and returns an array containing the state variable, and the function you call to alter the state. Since it returns an array we use array destructuring to access each individual item, like this: `const [count, setCount] = useState(0)`

  ```jsx
  import { useState } from 'react';

  const Counter = () => {
    const [count, setCount] = useState(0);

    return (
      <div>
        <p>You clicked {count} times</p>
        <button onClick={() => setCount(count + 1)}>Click me</button>
      </div>
    );
  };
  ```

**Managing Multiple State Variables:**
- Multiple `useState` calls can be made to manage different state variables.
- Each state variable is independent and has its own updater function.
- Example:
  ```jsx
  const ExampleComponent = () => {
    const [value1, setValue1] = useState(initialValue1);
    const [value2, setValue2] = useState(initialValue2);
    // ...
  };
  ```
- Hooks should be called at the top level of functional components, not inside loops, conditions, or nested functions.
- Hooks should be called in the same order in every render of the component.

- The `useState` hook enables functional components to have their own state.
- Hooks provide a simpler and more concise way to manage state compared to class components.
- The introduction of hooks has made functional components a preferred choice for writing React applications.

**Accessing Lifecycle Hooks with `useEffect`**
- React Hooks provide a way for functional components to access lifecycle events.
- The `useEffect` hook is used to perform side effects in functional components, similar to lifecycle methods in class components.

- The following example demonstrates the basic usage of `useEffect` to log a message on every render/update:
  ```jsx
  import React, { useEffect, useState } from 'react';

  const CounterWithNameAndSideEffect = () => {
    const [count, setCount] = useState(0);
    const [name, setName] = useState('Flavio');
    
    useEffect(() => {
      console.log(`Hi ${name} you clicked ${count} times`);
    });

    return (
      <div>
        <p>
          Hi {name} you clicked {count} times
        </p>
        <button onClick={() => setCount(count + 1)}>Click me</button>
        <button onClick={() => setName(name === 'Flavio' ? 'Roger' : 'Flavio')}>
          Change name
        </button>
      </div>
    );
  };
  ```

**Cleanup with `useEffect`:**
- To mimic the `componentWillUnmount` behavior, you can return a cleanup function from `useEffect`:
  ```jsx
  useEffect(() => {
    console.log(`Hi ${name} you clicked ${count} times`);
    return () => {
      console.log(`Unmounted`);
    };
  });
  ```

**Conditional Run with Dependency Array:**

useEffect() can be called multiple times, which is nice to separate unrelated 
logic (something that plagues the class component lifecycle events).

Since the useEffect() functions are run on every subsequent re-render/update, we can tell React to skip a run, for performance purposes, by adding a second parameter which is an array that contains a list of state variables to watch for. React will only re-run the side effect if one of the items in this array changes

- You can specify a dependency array to control when `useEffect` runs.
- If the dependencies change, the effect is re-run:
  ```jsx
  useEffect(() => {
    console.log(`Hi ${name} you clicked ${count} times`);
  }, [name, count]);
  ```

**Run Once with Empty Dependency Array:**
- An empty dependency array ensures that the effect runs only once (during mount):
  ```jsx
  useEffect(() => {
    console.log(`Component mounted`);
  }, []);
  ```

**Benefits of `useEffect`:**
- `useEffect` simplifies the handling of side effects and replaces traditional lifecycle methods in functional components.
- It improves the performance of components by running asynchronously after the render.

- `useEffect` is a powerful hook for managing side effects and accessing lifecycle events in functional components.
- It provides cleaner and more concise code compared to class component lifecycle methods.

**Handling Events in Function Components**
- In React function components, event handling was traditionally done using class components or by passing event handlers via props.
- With the introduction of hooks, particularly `useCallback`, event handling in function components has become more concise and efficient.

**Using `useCallback` for Event Handling:**
- The `useCallback` hook is used to memoize functions, particularly useful for preventing unnecessary re-renders of child components.
- Example of using `useCallback` for handling a button click event:
  ```jsx
  import React, { useCallback } from 'react';

  const Button = () => {
    const handleClick = useCallback(() => {
      //...do something
    }, []); // Empty dependency array means the function does not depend on any variable
    return <button onClick={handleClick}>Click me</button>;
  };
  ```

**Passing Parameters with `useCallback`:**
- If the event handler function uses variables, those variables must be included in the dependency array:
  ```jsx
  const Button = () => {
    let name = ''; //... add logic
    const handleClick = useCallback(
      () => {
        //...do something with name
      },
      [name] // Include name in the dependency array
    );
    return <button onClick={handleClick}>Click me</button>;
  };
  ```

**Custom Hooks for Cross-Component Communication:**
- Custom hooks provide a way to share state and logic between components.
- Example custom hooks:
  ```jsx
  // Example 1: Custom hook to fetch data
  const useGetData = () => {
    //... logic to fetch data
    return data;
  };

  // Example 2: Custom hook to fetch user data
  const useGetUser = (username) => {
    //... logic to fetch user data
    const user = fetch(...);
    const userData = ...;
    return [user, userData];
  };
  ```

**Using Custom Hooks in Components:**
- Components can use custom hooks to access shared logic or state:
  ```jsx
  const MyComponent = () => {
    const data = useGetData();
    const [user, userData] = useGetUser('flavio');
    //... use data and user in the component
  };
  ```

**When to Use Hooks vs Regular Functions:**
- The decision to use hooks instead of regular functions depends on the specific use case.
- Hooks are advantageous for managing state and side effects in functional components, making them a preferred choice in modern React development.

**Takeaway:**
- `useCallback` is a valuable hook for optimizing event handling functions in function components.
- Custom hooks offer a powerful way to share state and logic between components, reducing the reliance on patterns like render props and higher-order components.

### Code Splitting with React.lazy and Suspense

Modern JavaScript applications often have large bundle sizes, causing longer load times and increased memory usage. Code splitting is a technique to address this issue by loading only the necessary JavaScript code when it is needed. React 16.6.0 introduced React.lazy and Suspense, providing an efficient way to lazily load dependencies.

1. **Goals:**
   - Reduce the initial bundle size.
   - Improve app performance by loading code only when required.
   - Minimize the impact on memory and battery usage, particularly on mobile devices.

2. **React.lazy Usage:**
   - Dynamically import components using React.lazy.
   - Components are loaded only when they are needed.
   - Example:
     ```jsx
     const TodoList = React.lazy(() => import('./TodoList'));
     ```

3. **React.lazy Component Rendering:**
   - Lazily loaded components are dynamically added to the output when available.
   - Webpack creates separate bundles for lazily loaded components.
   - Example:
     ```jsx
     export default () => (
       <div>
         <TodoList />
       </div>
     );
     ```
4. **Suspense Component Usage:**
   - Suspense is a component used to wrap lazily loaded components.
   - Manages the loading state while fetching and rendering the lazy-loaded component.
   - Example:
     ```jsx
     export default () => (
       <div>
         <React.Suspense fallback={<p>Please wait</p>}>
           <TodoList />
         </React.Suspense>
       </div>
     );
     ```
5. **Handling Loading with Fallback:**
   - Use the `fallback` prop of Suspense to specify JSX or a component to render during the loading process.

6. **Integration with React Router:**
   - React.lazy and Suspense seamlessly integrate with React Router for efficient code splitting in route-based components.
   - Example:
     ```jsx
     const App = () => (
       <Router>
         <React.Suspense fallback={<p>Please wait</p>}>
           <Switch>
             <Route exact path="/" component={TodoList} />
             <Route path="/new" component={NewTodo} />
           </Switch>
         </React.Suspense>
       </Router>
     );
     ```
