# Asynchronous JavaScript

---

## Normal Function in JS

The code way to write function in JS is as follows:

### Find sum of two numbers

```js
// ① function declaration
function sum(a, b) {
  return a + b;  // ②
}

// ② function call
console.log(sum(2, 3));  // op: 5
```

---

### Find sum from 1 to 100 (a number)

```js
// ① function declaration
function sum(n) {
  let total = 0;  // ④ variable initialization
  
  // ⑤ loop runs from 1 to n
  for (let i = 1; i <= n; i++) {
    total = total + i;  // then here loop run for n time
  }
  
  return total;  // ⑥ then here returning
}

// ② function call
console.log(sum(100));  // then here returning
// op: 5050
```

---

## Synchronous Code

**Synchronous code** is executed line by line, in the order it's written. Each operation waits for the previous one to complete before moving on next one.

↑ eg: see the `sum(100)` code written above.

---

## I/O Heavy Operations

**I/O (input/output) heavy operations** refers to tasks in a computer program that involve a lot of data transfer between the program and external system or devices. These operations usually require waiting for data to be read from or written to sources like disk, networks, databases, or other external devices, which can be time consuming to in-memory computation.

### Examples of I/O heavy operations:

1. Reading a file
2. Starting a clock
3. HTTP Request

**Note:** `require` statement lets you import code/function, `export` from other file/module.

Let's try to write code to do an I/O heavy operation:

1. Open replit
2. Create a file in there (`a.txt`) with some text inside
3. Write the code to read a file synchronously

**File structure:**
```
project/
├── index.js
└── a.txt
```

```js
const fs = require("fs");
const contents = fs.readFileSync("a.txt", "utf-8");
console.log(contents);
```

---

## I/O Bound Tasks vs CPU Bound Tasks

### CPU BOUND TASK

CPU-bound tasks are operations that are limited by the speed and power of the CPU. These tasks require significant computation and processing power, meaning that the performance bottleneck is the CPU itself.

```js
let ans = 0;
for (let i = 1; i <= 1000; i++) {
  ans = ans + i;
}
console.log(ans);
```

💡 **Real world example:** Running for 3 miles — your legs/brain have to be constantly engaged for all 3 miles while you run.

---

### I/O BOUND TASK

**I/O-Bound task** are operations that are limited by the system's input/output capabilities, such as disk I/O, network I/O, or any other form of data transfer. These tasks spend most of their time waiting for I/O operations to complete.

💡 **Real world example:** Boiling water — I don't have to do much, I just put water in kettle, and my brain can be occupied elsewhere.

---

## Using I/O Bound Tasks in the Real World

**Example file structure we'll be using:**
```
project/
├── index.js
├── a.txt
├── b.txt
└── c.txt
```

What if you were tasked with doing 3 things:

1. Boil some water
2. Do some laundry
3. Send a package via mail

Would you do these:

1. One by one (synchronously)?
2. Context switch between them (concurrently)?
3. Start all 3 tasks together and wait for them to finish. The first one that finishes gets catered to first.

---

### Synchronously (one by one)

```js
const fs = require("fs");
const contents = fs.readFileSync("a.txt", "utf-8");
console.log(contents);

const contents2 = fs.readFileSync("b.txt", "utf-8");
console.log(contents2);

const contents3 = fs.readFileSync("c.txt", "utf-8");
console.log(contents3);
```

---

### Start all 3 tasks together, and wait for them to finish

```js
const fs = require("fs");

fs.readFile("a.txt", "utf-8", function (err, contents) {
  console.log(contents);
});

fs.readFile("b.txt", "utf-8", function (err, contents) {
  console.log(contents);
});

fs.readFile("c.txt", "utf-8", function (err, contents) {
  console.log(contents);
});
```

**→ function passed as argument**

---

## Functional Arguments

Write a calculator program that adds, subtracts, multiplies, divides two arguments.

### Approach — 1: Calling the respective function

```js
function sum(a, b) {  // functional argument
  return a + b;  
}

function multiply(a, b) {
  return a * b;  
}

function subtract(a, b) {
  return a - b;
}

function divide(a, b) {
  return a / b;
}

function doOperation(a, b, op) { // by passing a function to another function as an argument
  return op(a, b);
}
```

---

### Approach — 2: Passing in what needs to be done as an argument

```js
console.log(sum(1, 2));  // ① Approach

console.log(doOperation(1, 2, sum));  // ② Approach
```

---

## Asynchronous Code, Callbacks

Let's look at the code to read from a file **asynchronously**. Here, we pass in a **function as an argument**. This function is called a **callback** since the function gets **called back** when the file is read.

```js
const fs = require("fs");

function afterFileRead(err, contents) {
  console.log(contents);
}

fs.readFile("a.txt", "utf-8", afterFileRead);
```

---

### Another approach

```js
const fs = require("fs");

fs.readFile("a.txt", "utf-8", function (err, contents) {
  console.log(contents);
});
```

---

## setTimeout

**setTimeout** is another asynchronous function that executes a certain code after some time.

```js
function run() {
  console.log("I will run after 1 sec");
}

setTimeout(run, 1000);  // 1000 millisecond

console.log("I will run immediately");
```

---

### Another way of finding sum from 1 to n number

```js
function sum(n) {
  return total = n * (n + 1) / 2;
}

const ans = sum(10);
console.log(ans);

// op: 55
```

---

## JS Architecture for Async Code

### 1. Call Stack

The **call stack** is a data structure that keeps track of the function calls in your program. It operates in a "Last In, First Out" (LIFO) manner, meaning the last function that was called is the first one to be executed and removed from the stack.

- When a function is called, it gets **pushed onto** the call stack
- When the function completes, it's **popped off** the stack

```js
// ① function first() { ⑥
function first() {
  console.log("first");  // ⑦
}

// ② function second() { ④
function second() {
  first();  // ⑤
  console.log("second");  // ⑧
}

// ③ second();
second();
```

**Execution order:** ① → ② → ③ → ④ → ⑤ → ⑥ → ⑦ → ⑧

---

### 2. Web APIs

**Web APIs** are provided by the browser (or the Node.js runtime) and allow you to perform tasks that are outside the scope of the JavaScript language itself, such as making network requests, setting timers, or handling DOM events.

---

### 3. Callback Queue

The **callback queue** is a list of tasks (callbacks) that are waiting to be executed once the call stack is empty. These tasks are added to the queue by web APIs after they have completed their operation.

---

### 4. Event Loop

The **event loop** constantly checks if the call stack is empty; if it is and there are callbacks in the callback queue, it will push the first callback from the queue onto the call stack for execution.

---

## Visual Flow

```
┌─────────────────────────────────────────────┐
│           JavaScript Runtime                │
│                                             │
│  ┌──────────────┐      ┌────────────────┐   │
│  │  Call Stack  │      │   Web APIs     │   │
│  │              │      │  - setTimeout  │   │
│  │   main()     │◄─────│  - fetch       │   │
│  │   second()   │      │  - DOM events  │   │
│  │   first()    │      └────────────────┘   │
│  └──────────────┘               │           │
│         ▲                       ▼           │
│         │              ┌────────────────┐   │
│         │              │ Callback Queue │   │
│         │              │  [cb1, cb2]    │   │
│         │              └────────────────┘   │
│         │                       ▲           │
│         └───────Event Loop──────┘           │
│                                             │
└─────────────────────────────────────────────┘
```
