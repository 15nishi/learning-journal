# JavaScript — Classes, Promises & Async/Await

**Date:** May 5, 2026
**Track:** FullStack — 100xDevs Week 2

## What I Learned
- JS has two type categories: primitive (number, string, boolean) and complex (objects, arrays). Classes produce complex types.
- A class is a blueprint for objects. The `constructor` runs automatically when you create an instance with `new`, and `this` refers to that specific instance.
- Promises represent the eventual success or failure of an async operation — calling one is easy, but defining your own is where it gets hard.
- Callback hell happens when you nest callbacks inside callbacks to sequence async tasks — it works but becomes unreadable fast.
- Promise chaining with `.then()` fixes the nesting problem, and `async/await` makes it look synchronous while still being async under the hood.
- Error handling differs by approach: callbacks use the "error-first" pattern (first argument is error), while Promises use `reject` and `.catch()`.

## Code / Commands
```javascript
// Class example
class Rectangle {
  constructor(width, height, color) {
    this.width = width;
    this.height = height;
    this.color = color;
  }
  area() {
    return this.width * this.height;
  }
  paint() {
    console.log(`Painting with color ${this.color}`);
  }
}
const rect = new Rectangle(2, 4);
console.log(rect.area()); // 8

// Promisified setTimeout
function setTimeoutPromisified(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

// Async/await version
async function solve() {
  await setTimeoutPromisified(1000);
  console.log("hi");
  await setTimeoutPromisified(3000);
  console.log("hello");
  await setTimeoutPromisified(5000);
  console.log("hello there");
}
solve();

// Promisified file cleaner with error handling
const fs = require("fs");
function cleanFile(filePath, cb) {
  return new Promise(function(resolve) {
    fs.readFile(filePath, "utf-8", function(err, data) {
      data = data.trim();
      fs.writeFile(filePath, data, function() {
        resolve();
      });
    });
  });
}
async function main() {
  await cleanFile("a.txt");
  console.log("Done cleaning file");
}
main();
```

## The One Thing That Clicked
> `async/await` is just syntactic sugar on top of Promises — we're not using something new, we're writing the same Promise logic in a way that reads like synchronous code. That reframe made everything make sense.

## What Still Confuses Me
- [ ] When exactly should I use `.then()` chaining vs `async/await`? Is one preferred in real projects?
- [ ] What happens if you `await` inside a non-async function — does it silently fail or throw?
- [ ] Static methods vs instance methods — when would I actually reach for static in a real project?

## Resource Used
- 100xDevs Full Stack Course by Harkirat Singh — Week 2 lectures
