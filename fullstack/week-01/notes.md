# HTML + CSS + JavaScript Fundamentals

**Track:** FullStack — Week 1

## What I Learned
- HTML is the skeleton of the web — tags like `<div>`, `<span>`, `<nav>`,
  `<head>`, `<body>` each have a specific structural role; `<div>` is block-level,
  `<span>` is inline
- CSS can be applied three ways: inline styles, internal `<style>` tag, or an
  external `.css` file linked via `<link rel="stylesheet">`
- Flexbox makes layout manageable — `justify-content` values like `flex-start`,
  `center`, `space-between`, and `space-evenly` control horizontal distribution
- JS is interpreted, dynamically typed, single-threaded, and garbage collected —
  these four properties define how it behaves differently from C++
- Functions are first-class in JS — you can pass them as arguments (callbacks),
  which is the foundation of async code
- The JS async architecture has four parts: call stack, web APIs, callback queue,
  and the event loop that connects them

## Code / Commands
```javascript
// Variables
let firstName = "John";       // reassignable
const age = 30;               // constant
var isStudent = true;         // function-scoped (avoid)

// Objects
const user = {
  name: "Nishi",
  age: 20,
  address: {
    city: "Delhi",
    country: "India"
  }
};
const city = user.address.city;

// Functions + callbacks
function sum(a, b) {
  return a + b;
}
console.log(sum(2, 3)); // 5

// For loop
const users = ["Harkirat", "Nishi", "Diljeet", "Lucky"];
const totalUsers = users.length;
for (let i = 0; i < totalUsers; i++) {
  console.log(users[i]);
}

// Async with callback
const fs = require("fs");
fs.readFile("a.txt", "utf-8", function(err, contents) {
  console.log(contents);
});

// setTimeout (async)
setTimeout(function run() {
  console.log("I will run after 1 sec");
}, 1000);
console.log("I will run immediately");
