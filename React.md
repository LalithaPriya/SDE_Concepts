
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

