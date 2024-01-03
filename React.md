
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



