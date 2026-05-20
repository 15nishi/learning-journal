# CLASS in JS
 
| Primitive Data Types | Complex Data Types |
| -------------------- | ------------------ |
| number               | objects ←          |
| string               | arrays             |
| boolean              | function           |
 
---
 
## Classes
 
In JavaScript, classes are a way to define blueprints for creating objects (these objects are different from the objects defined in last section)
 
`new` - is a keyword that help to create new instance or object  
`this` - is a keyword that helps you access object variable data
 
 
```js
class Rectangle {
  constructor(width, height, color) {
    this.width = width;
    this.height = height;
    this.color = color;
  }
 
  area() {
    const area = this.width * this.height;
    return area;
  }
 
  paint() {
    console.log(`Painting with color ${this.color}`);
  }
}
 
const rect = new Rectangle(2, 4, 'Blue');
const area = rect.area();
console.log(area);
rect.paint();
```
 
---
 
## Key Concepts
 
**1. Class Declaration**
- you declare a class using the `class` keyword
- inside a class, you define properties (variables) and methods (functions) that will belong to the objects created from this class
  
**2. Constructor**
- a special method inside the class that is called when you create an instance (object) of the class
- it's used to initialize the properties of the object
  
**3. Methods**
- functions that are defined inside the class and can be used by all instances of the class
  
**4. Inheritance**
- classes can inherit properties and methods from other classes, allowing you to create a new class based on an existing one
  
**5. Static Methods**
- methods that belong to the class itself, not to instances of the class. You call them directly on the class
  
**6. Getters and Setters**
- special methods that allow you to define how properties are accessed and modified
---
 
## Some more classes — in-built classes in JS
 
**Date**
```js
const now = new Date()               // current date & time
console.log(now.toISOString());      // output the date in ISO format
```
 
**Map**
```js
const map = new Map()
map.set('name', 'Alice');            // → use to create key-value pairs
map.set('age', 30);
console.log(map.get('name'));        // → Alice
 
// let user = { name: "Alice", age: 30 }
```
 
---
 
## Promise class
 
💡 calling a promise is easy, defining your own promise is where things get hard.
 
A promise in JavaScript is an object that represents the eventual completion (or failure) of an asynchronous operation and its resulting value.
 
Promises are used to handle asynchronous operations more effectively than traditional callback functions, providing a cleaner and more manageable way to deal with code that executes asynchronously, such as API calls, file I/O, or timers.
 
using a function that returns a promise
 
> ignore the function definition of `setTimeoutPromisified` for now
 
```js
function setTimeoutPromisified(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}
 
function callback() {
  console.log("3 seconds have passed");
}
 
setTimeoutPromisified(3000).then(callback)    // promisified version
setTimeout(callback, 3000);                   // callback version
```
 
---
 
## Visual structure of Promise
 
```
Promise
|
|-- constructor
|     new Promise()
|
|-- static methods
|     |-- resolve()      by default-resolve, we call .then
|     |-- reject()       by default-reject, we call .catch
|     |-- all()          all promises run, if either any get rejected, all get rejected
|     |-- allSettled()   all promises run and return their state (resolve / reject)
|     |-- race()         fastest promise to resolve get return
|     └── any()          first promise to resolve get return
|
└── instance method
      |-- then()         run if resolved
      |-- catch()        run if reject
      └── finally()      run at the end either case resolve - reject
```
 
---
 
## Program which shows control flow of Promises
 
```js
const fs = require("fs");    // ①
 
console.log("----- Top of the file -----");
 
function readTheFile(resolve) {    // ③
  console.log("readTheFile called");
 
  setTimeout(function() {          // after 3 sec
    console.log("setTimeout completed");    // ⑤
    resolve();
  }, 3000);
}
 
function setTimeoutPromisified() {    // ②
  console.log("setTimeoutPromisified called");
  // returns a promise
  return new Promise(readTheFile);
}
 
const p = setTimeoutPromisified();
 
function callback() {    // ⑥
  console.log("Promise is done");
}
 
p.then(callback);    // ④
 
console.log("----- End of the file -----");

```
**Execution order:** ① → ② → ③ → ④ → ⑤ → ⑥ → ⑦ → ⑧
 
Output:
```
----- Top of the file -----
setTimeoutPromisified called
readTheFile called
----- End of the file -----
// after 3 sec
setTimeout completed
Promise is done
```


---
 
## Eg: Promise — Defining Own
 
```js
class Promise2 {
  constructor(fn) {
    function afterDone() {
      this.resolve();
    }
    fn(afterDone)
  }
 
  then(callback) {
    this.resolve = callback;
    // this.width = 2;
  }
}
 
function readTheFile(resolve) {
  setTimeout(function() {
    console.log("callback based setTimeout completed");
    resolve();
  }, 3000);
}
 
function setTimeoutPromisified() {
  return new Promise2(readTheFile)
}
 
let p = setTimeoutPromisified();
 
function callback2() {
  console.log("callback has been called");
}
 
p.then(callback2);
```
