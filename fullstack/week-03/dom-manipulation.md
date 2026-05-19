# DOM Manipulation

## What is DOM?

The DOM (Document Object Model) is a programming interface for web documents. It represents the structure of a webpage as a tree of objects.

```
html
├── head
│   ├── title
│   └── meta
└── body
    └── h1
```

```html
<html>
  <head>
    <title>Simple App</title>
    <meta name="description">
  </head>
  <body>
    <h1>Hi there</h1>
  </body>
</html>
```

---

## Why DOM?

- HTML alone creates only static web pages
- The DOM allows JavaScript to interact with the webpage dynamically
- It acts as a bridge between HTML structure and JS functionality
- The DOM abstracts the structure of documents into a tree of objects, allowing script to manipulate content and structure dynamically

---

## Static HTML

Static HTML refers to web pages whose content remains fixed unless the source code is manually changed.

- The browser only displays the content written in the HTML file
- No dynamic behaviour happens automatically
- User interactions (like clicking buttons) do not change the page unless JavaScript is added

---

## Dynamic HTML

Dynamic HTML refers to web pages whose contents can be changed dynamically without reloading the page.

It is achieved using:
- HTML → structure
- CSS → styling
- JavaScript + DOM → dynamic behaviour

---

## Fetching Elements

Fetching elements means selecting or accessing HTML elements using JavaScript.

- JavaScript uses DOM methods to find elements inside a webpage
- Once an element is fetched, we can:
  - Read content
  - Change text
  - Modify style
  - Add events
  - Remove elements

**Why fetch elements?**
To interact with a webpage dynamically, JavaScript first needs access to HTML elements — e.g. change heading text, handle button clicks. This is done by fetching elements from the DOM.

---

## Popular DOM Fetching Methods

There are 5 commonly used methods.

---

### 1. querySelector()

Selects the first matching element from the webpage. Uses CSS selectors.

```
Syntax: document.querySelector("selector")
```

```html
<!-- HTML -->
<h1>Todo List</h1>
```
```js
const title = document.querySelector('h1');
console.log(title.innerHTML);
// op: Todo List
```

- `.innerHTML` — for any HTML content
- `.value` — for input tag content

---

### 2. querySelectorAll()

Selects all matching elements. Returns a collection called a NodeList.

```
Syntax: document.querySelectorAll("selector")
```

```html
<!-- HTML -->
<h4>1. Take class</h4>
<h4>2. Go out to eat</h4>
```
```js
const secondTodo = document.querySelectorAll("h4")[1];
console.log(secondTodo.innerHTML);
// op: 2. Go out to eat
```

---

### 3. getElementById()

Fetches an element using its unique ID.

```
Syntax: document.getElementById("id")
```

```html
<!-- HTML -->
<h1 id="title">Todo App</h1>
```
```js
const element = document.getElementById("title");
console.log(element.innerHTML);
// op: Todo App
```

---

### 4. getElementsByClassName()

Fetches all elements with the same class name. Returns an HTMLCollection.

```
Syntax: document.getElementsByClassName("className")
```

```html
<!-- HTML -->
<h4 class="todo">Study</h4>
<h4 class="todo">Eat</h4>
```
```js
const todos = document.getElementsByClassName("todo");
console.log(todos[0].innerHTML);
// op: Study
```

---

### 5. getElementsByTagName()

Fetches elements using HTML tag names.

```
Syntax: document.getElementsByTagName("tagName")
```

```html
<!-- HTML -->
<p>Hello</p>
<p>World</p>
```
```js
const paragraphs = document.getElementsByTagName("p");
console.log(paragraphs[1].textContent);
// op: World
```

---

## Updating Elements

Updating elements means changing the content of HTML elements dynamically using JavaScript. DOM allows JavaScript to modify webpage content without reloading the page.

### Popular properties used for updating

---

#### 1. .innerHTML

Used to get or update HTML content inside an element. It can add text, HTML tags, and nested elements.

```
Syntax: element.innerHTML
```

```html
<h4>Take class</h4>
```
```js
const firstTodo = document.querySelector("h4");
firstTodo.innerHTML = "Don't take class";
```

---

#### 2. .textContent

Updates only plain text. HTML tags are treated as normal text, not rendered as HTML.

```js
firstTodo.textContent = "<b>Important Task</b>";
// op: <b>Important Task</b>  ← tag is not rendered as HTML
```

---

## Deleting Elements

Deleting an element means removing it from the webpage dynamically.

### Popular DOM removing methods

---

#### 1. remove()

Removes the element itself / a node from the document.

```
Syntax: element.remove()
```

---

#### 2. removeChild()

Removes a specific child node of a parent.

```
Syntax: parentElement.removeChild(childElement)
```

Note: we can't directly call removeChild() on the element itself. We must access the parent element first.

---

#### 3. onclick event

onclick is an event that triggers when a user clicks on an element such as a button, div, image, or link.

```html
<button onclick="sayHello()">Click</button>
```
```js
function sayHello() {
  alert("Hello");
}
```

---

## Adding Elements

Adding elements means creating new HTML elements using JavaScript and inserting them into the webpage dynamically. It allows content to appear on the page without refreshing the website.

### Adding methods

---

#### 1. createElement()

Used to create a new HTML element dynamically using JavaScript.

```
Syntax: document.createElement("tagName")
```

```js
const div = document.createElement("div");
```

---

#### 2. appendChild()

Used to add a child element inside a parent element.

```
Syntax: parentElement.appendChild(childElement)
```

```js
const parent = document.getElementById("todos");
const div = document.createElement("div");
div.textContent = "New Todo";
parent.appendChild(div);
```

---
