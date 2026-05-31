# JavaScript — The Basics


## Web Development

- Web development involves writing a lot of HTML, CSS and JS code
- Historically (and even today to some extent), browsers could only understand HTML, CSS and JS
- Any website that we see is a bunch of HTML, CSS and JS files along with some assets (images, video etc.)

---

## Facts / Callouts

1. React, NextJS are frameworks. They compile down to HTML, CSS, JS in the end. That is what your browser understands.

2. When you run your C++ code on Leetcode, it does not run on your browser / machine. It runs somewhere else. Your browser can't compile and run C++ code.

3. If someone asks — what all languages can your browser interpret, the answer is HTML, CSS, JS and Web Assembly. It can, technically, run C++ / Rust code that is compiled down to Web Assembly (WASM).

---

## Properties of JS

Every language comes with its unique set of features. JS has the following:

---

### 1. Interpreted

JS is an interpreted language, meaning it is executed line by line at runtime by the JS engine in the browser or server environment, rather than being compiled into machine code beforehand.

```
C++ code:
source code → [compiler] → Binary → Run on your machine
(good for production)

JS code:
source code → Run on your machine directly
(good for developers — one less step)
```

**Upside:**
- There is one less step to do before running your code

**Downside:**
- Performance overhead
- More prone to runtime errors

> TypeScript helps to reduce runtime errors at compilation. TypeScript works like C++ — TypeScript converts into JS → runs on machine.

---

### 2. Dynamically Typed

Variables in JS are not bound to a specific data type. Types are determined at runtime and can change as the program executes.

```
C++ code (won't compile):         JS code (will compile):
int main() {                      var a = 1;
  int a = 1;                      a = "nishi";
  a = "hello";   ← error          a = true;
  a = true;                       console.log(a)
}
// C++ doesn't let you            // JS lets you change
// change data type               // data type
```

---

### 3. Single Threaded

JS executes code in a single-threaded environment, meaning it processes one task at a time.

**Single Threaded (JavaScript)**
```
 ┌───────────┐
 │  ●  ○  ○  │
 │  ○  ○  ○  │
 │  ○  ○  ○  │
 └───────────┘
(only CPU 1 busy)
● = busy  ○ = idle
```

**Multi-Threaded (Rust/C++)**
```
 ┌───────────┐
 │  ●  ●  ●  │
 │  ●  ●  ●  │
 │  ●  ●  ●  │
 └───────────┘
(all CPUs busy)
● = busy  ○ = idle
```

---

### 4. Garbage Collected

JS automatically manages memory allocation and deallocation through garbage collection, which helps prevent memory leaks by automatically reclaiming memory used by objects no longer in use.

**Memory Management comparison:**

| Garbage Collector | Manual | Rust way |
|---|---|---|
| Written by smart people | You allocate & deallocate memory yourself | Rust has its own ownership model for memory management |
| Usually no dangling pointers / memory issues | Can lead to dangling pointers / memory issues | Makes it extremely safe from memory errors |
| You can't do manual memory management | Learning curve is high since you have to do manual MM | — |
| Example — Java, JS | Example — C | — |

---

### Conclusion — Is JS a good language?

Yes and no. It is beginner friendly, but has a lot of performance overhead. But is trying to solve for a lot of this; there's a long way to go before JS can compete with languages like C++ / Rust.

---

## Syntax of JavaScript

### 1. Variables

Variables are used to store data. In JS, you declare variables using `var`, `let` or `const`.

```js
let firstName = "John";       // variable that can be reassigned
const age = 30;               // constant variable that cannot be reassigned
var isStudent = true;         // older way to declare variable, function-scoped
```

---

### 2. Data Types

```js
let number = 42;                        // int
let string = "Hello World";            // string
let isActive = false;                  // boolean
let numbers = [1, 2, 3];              // array
let person = { name: "Nishi", age: 20 }; // object
```

---

### 3. Operators

```js
let sum = 10 + 5;              // arithmetic
let isEqual = (10 == 10);      // comparison
let isTrue = (true && false);  // logical
```

---

### 4. Functions

```js
// function declaration
function greet(name) {
  return "Hello, " + name;
}

let message = greet("John");   // function call
console.log(message);          // Hello, John
```

**Sum function — works with both numbers and strings:**

```js
// function sum is declared
function sum(a, b) {
  let totalSum = (a + b);
  return totalSum;
}

let ans = sum(1, 9);           // function call
console.log(ans);              // op: 10

let ans2 = sum("1", "9");     // giving string instead of int
console.log(ans2);             // op: 19
```

**Syntax error example:**

```js
function canVote(age) {
  if (age >= 18);    // syntax error — the return runs unconditionally
  return true;       //               despite age >= 18
}

let age = canVote(80);
console.log(age);   // correct ans on next page
```

---

### 5. if / else

```js
// check age
function canVote(age) {
  if (age >= 18) {
    console.log("You are an adult.");
  } else {
    console.log("You are a minor.");
  }
}

canVote(20);
```

**canVote function using if & else with return:**

```js
// declaration of canVote function
function canVote(age) {
  if (age >= 18) {
    return true;    // if else applied
  } else {
    return false;
  }
}

let age = canVote(1);    // function call
console.log(age);        // console.log(false) — op
```

**Odd / Even example:**

```js
function oddEven(no) {
  if (no % 2 == 0) {
    console.log("no. is even");
  } else {
    console.log("no. is odd");
  }
}

oddEven(11);   // op: no. is odd
```

---

### 6. Loops

```js
let users = ["Harkisat", "Nishi", "Diljeet", "Lucky"];
for (let i = 0; i < 4; i++) {
//   ▲          ▲      ▲
//   │          │      └─── increment
//   │          └────────── condition
//   └───────────────────── initialisation
  console.log(users[i]);
}
```


We can replace `4` with `users.length` by creating a length variable:

```js
let totalUsers = users.length;
// put it before the for loop code
for (let i = 0; i < totalUsers; i++) {
  console.log(users[i]);
}
```

**Sum from 1 to n using loop:**

```js
// function will take single input n
function sum(n) {
  let total = 0;       // initial value be 0
  for (let i = 1; i <= n; i++) {  // loop will sum from i to n adding each no. in total
    total += i;
  }
  return total;        // return total sum
}

let result = sum(5);
console.log(result);   // op: 15
```

---

## Complex Types


### 1. Objects

An object in JS is a collection of key-value pairs, where each key is a string and each value can be any valid JS data type, including another object.

```js
// key/value pairs
let user = {
  name: "Nishi",   // key: value
  age: 20
};

console.log("Nishi age is " + user.age);
```

**Function that takes a user as input and greets them with their name and age:**

```js
// 1st way
let user = {
  name: "Nishi",
  age: 20
};

function greet(user) {
  return "Hello " + user.name + ", you are " + user.age + " yr old";
}

console.log(greet(user));
```

```js
// 2nd way — function directly logs
function greet(user) {
  console.log("hi " + user.name + " you are " + user.age + " yr old");
}

let user = {
  name: "Nishi",
  age: 20
};

greet(user);
```

**Function with name, age and gender:**

```js
let user = {
  name: "nishi",
  age: 20,
  gender: "Male"
};

function greet(user) {
  return "Hi Mr. " + user.name + ", your age is " + user.age;
}

console.log(greet(user));
```

**Also tell the user if they are legal to vote or not:**

```js
function canVote(vote) {
  if (user.age >= 18) {
    return "you are eligible to vote";
  } else {
    return "you are not eligible to vote";
  }
}

let age1 = canVote(user.age);
console.log(age1);
```

---

### 2. Arrays

Arrays let you group data together.

```js
const users = ["Nishi", "Harkisat", "diljeet"];
const totalUsers = users.length;
const firstUser = users[0];
```

**Assignment — function that takes an array of numbers as input and returns a new array with only even values:**

```js
function evenNumbers(arr) {
  let newArray = [];
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] % 2 === 0) {
      newArray.push(arr[i]);
    }
  }
  return newArray;
}

let numbers = [1, 2, 3, 4, 5, 6];
console.log(evenNumbers(numbers));
// op: [2, 4, 6]
```

---

### 3. Array of Objects

We can have more complex objects, for example an array of objects.

```js
const users = [
  {
    name: "nishi",
    age: 20
  },
  {
    name: "Harkisat",
    age: 28
  }
];

const user1 = users[0];          // { name: "nishi", age: 20 }
const user1Age = users[0].age;   // 20
```

---

### 4. Object of Objects

We can have an even more complex object (obj of objs).

```js
const user1 = {
  name: "nishi",
  age: 20,
  address: {
    city: "Delhi",
    country: "India",
    pinCode: 110084
  }
};

const city = user1.address.city;   // Delhi
```
