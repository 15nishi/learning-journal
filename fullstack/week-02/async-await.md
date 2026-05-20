# Callback Hell, Promises Rejects & Async-Await


## Callback Hell

Write code that:

1. logs **hi** after 1 second → 1 sec
2. logs **hello** 3 second after step 1 → 4 sec
3. logs **hello there** 5 second after step 2 → 9 sec

---

### Solution (has callback hell)

```js
setTimeout(function() {
  console.log("hi");
  setTimeout(function() {
    console.log("hello");
    setTimeout(function() {
      console.log("hello there");
    }, 5000);
  }, 3000);
}, 1000);
```

---

### Alt Solution (doesn't really have callback hell)

```js
function step3Done() {
  console.log("hello there");
}

function step2Done() {
  console.log("hello");
  setTimeout(step3Done, 5000);
}

function step1Done() {
  console.log("hi");
  setTimeout(step2Done, 3000);
}

setTimeout(step1Done, 1000);
```

---

## Promisified Version

Now we use the **promisified** version we saw in the last slide.

```js
function setTimeoutPromisified(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}
```

---

### Solution #1 (has callback hell)

```js
setTimeoutPromisified(1000).then(function() {
  console.log("hi");
  setTimeoutPromisified(3000).then(function() {
    console.log("hello");
    setTimeoutPromisified(5000).then(function() {
      console.log("hello there");
    });
  });
});
```

---

### Alt Solution

```js
setTimeoutPromisified(1000)
  .then(function() {
    console.log("hi");
    return setTimeoutPromisified(3000);
  })
  .then(function() {
    console.log("hello");
    return setTimeoutPromisified(5000);
  })
  .then(function() {
    console.log("hello there");
  });
```

---

## Async Await Syntax

- The **async** and **await** syntax in JavaScript provides a way to write asynchronous code that looks and behaves like synchronous code, making it easier to read and maintain.

- It builds on top of **Promises** and allows you to avoid chaining **.then()** and **.catch()** method while still working with asynchronous operations.

- **async/await** is essentially syntactic sugar on top of Promises.

  ### Things to Keep in Mind

  - We can only call **await** inside a function if that function is **async**
  - We can't have a **top level await**

---

### Code Example: Assignment

Write a code that:

1. logs **hi** after 1 second → 1 sec
2. logs **hello** after step 1 (3 sec) → 4 sec
3. logs **hello there** 5 sec after step 2 → 9 sec

```js
function setTimeoutPromisified(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}

async function solve() {
  await setTimeoutPromisified(1000);
  console.log("hi");
  await setTimeoutPromisified(3000);
  console.log("hello");
  await setTimeoutPromisified(5000);
  console.log("hello there");
}

solve();
```

---

## Defining Your Own Async Function

**Q.** Write a function that:
1. To Read the contents of a file
2. Trims the extra space from the left and right
3. writes it back to the file.

---

### 1. Callback Approach

In the callback approach, the function signature should look something like this:

```js
function onDone() {
  console.log("file has been cleaned");
}

cleanFile("a.txt", onDone);
```

**#cleanFile** — function that removes extra spaces from both left and right using **trim()**

---

#### Solution → Callback

**File structure:**
```
project/
├── index.js
└── a.txt
```

```js
const fs = require("fs");

function cleanFile(filePath, cb) {
  fs.readFile(filePath, "utf-8", function(err, data) {
    data = data.trim();
    fs.writeFile(filePath, data, function() {
      cb();
    });
  });
}

function onDone() {
  console.log("file has been cleaned");
}

cleanFile("a.txt", onDone);
```

---

### 2. Promisified Approach

In the promisified approach, the function signature should look something like this:

```js
async function main() {
  await cleanFile("a.txt");
  console.log("Done cleaning file");
}

main();
```

---

#### Solution 2 → Promisified

**File structure:**
```
project/
├── index.js
└── a.txt
```

```js
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

---

## Error Handling: Callbacks vs Promises

### ☆ Callback

**fs.readFile** function used on **err first callback** approach to propagate back errors.

**File structure:**
```
project/
├── index.js
└── a.txt
```

```js
const fs = require("fs");

function afterDone(err, data) {
  if (err) {
    console.log("Error while reading file");
  } else {
    console.log(data);
  }
}

fs.readFile("a.txt", "utf-8", afterDone);
```

---

### ☆ Promises

**Promises** use the **reject** argument to propagate errors.

**File structure:**
```
project/
├── index.js
└── a.txt
```

```js
const fs = require("fs");

function readTheFilePromisified(filePath) {
  return new Promise(function(resolve, reject) {
    fs.readFile(filePath, "utf-8", function(err, data) {
      if (err) {
        reject("Error while reading file");
      } else {
        resolve(data);
      }
    });
  });
}

function onDone(data) {
  console.log(data);
}

function onError(err) {
  console.log("Error: " + err);
}

readFilePromisified("a.txt").then(onDone).catch(onError);
```

