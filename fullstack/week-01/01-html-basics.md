# HTML

HTML stands for Hyper Text Markup Language. It is the foundation of building unstyled websites.

---

## Tags in HTML


### 1. `<title>`

- Defines the title of the document
- It should be in text only
- It is shown in the browser's title bar or in the page's tab

```html
<title>My App</title>
```

```
output (browser tab):
┌────────────────┐
│  My App   ×    │
└────────────────┘
```

---

### 2. `<div>`

- Used as a container
- By default, browsers always place line breaks before and after the `<div>` element (block-level)

```html
<div>Box One</div>
<div>Box Two</div>
```

```
output:
┌─────────────┐
│   Box One   │
└─────────────┘
┌─────────────┐
│   Box Two   │
└─────────────┘
```

### `<span>`

- Used as an inline container
- Behaves similar to `<div>` but `<div>` is a block-level element and `<span>` is an inline element

```html
<div>
  Hello <span>World</span> how are you
</div>
```

```
output:
┌──────────────────────────┐
│  Hello World how are you │
└──────────────────────────┘
        ↑
   span sits inline, no line break
```

---

### 3. `<head>`

- `<head>` element is a container for metadata (anything that comes on pagetabs)
- Metadata is data about the HTML document
- Metadata is not displayed — it includes title, character set, styles, scripts, and other meta information

```html
<head>
  <title>Simple App</title>
  <meta name="description" content="My site">
  <link rel="stylesheet" href="index.css">
</head>
```

```
output: nothing visible on page
(affects tab title, SEO, and styles only)
```

---

### 4. `<body>`

- `<body>` tag defines the document's body
- `<body>` contains all contents of HTML documents such as headings, paragraphs, images, hyperlinks, tables, lists, etc.
- There can only be one `<body>` element in an HTML document

```html
<body>
  <h1>Hello</h1>
  <p>Welcome to my page</p>
</body>
```

```
output:
Hello
Welcome to my page
```

---

### 5. h1, h2, h3, h4, h5, h6

- `<h1>` to `<h6>` tags are used to define HTML headings
- `<h1>` defines the most important heading
- `<h6>` defines the least important heading

```html
<h1>Heading 1</h1>
<h2>Heading 2</h2>
<h3>Heading 3</h3>
```

```
output:
Heading 1   ← biggest
Heading 2
Heading 3   ← gets smaller as number increases
```

---

### 6. b, i, u

- `<b>` — bold text
- `<i>` — italic text
- `<u>` — underline text

```html
<b>Bold</b>
<i>Italic</i>
<u>Underline</u>
```

```
output:
**Bold**
_Italic_
Underline
─────────
```

---

### 7. `<a>`

- `<a>` tag defines a hyperlink, which is used to link from one page to another

```html
<a href="link">word</a>

<a target="_blank" href="link">word</a>
```

```
output:
word   ← clickable, opens in same tab
word   ← clickable, opens in new tab
```

`target="_blank"` — opens the link in a new tab

---

### 8. `<img>`

- `<img>` tag is used to embed an image in a web page
- `<img>` tag has two required attributes:
  - `src` — specifies the path to the image
  - `alt` — specifies the alternate text if image is not found at src

```html
<img src="URL/path" alt="alternate text">
```

```
output (image found):        output (image not found):
┌──────────────┐             [ alternate text ]
│   🖼 image   │
└──────────────┘
```

---

### 9. `<input>`

- `<input>` tag specifies an input field where the user can enter data
- `type` is default `text` but it can be many things like password, hidden, image, etc.

```html
<input type="text" placeholder="Search...">
<input type="password" placeholder="Password">
```

```
output:
┌──────────────────────┐
│  Search...           │   ← type="text"
└──────────────────────┘

┌──────────────────────┐
│  ••••••              │   ← type="password"
└──────────────────────┘
```

---

### 10. `<button>`

- `<button>` tag defines a clickable button

```html
<button>Download</button>
```

```
output:
┌────────────┐
│  Download  │
└────────────┘
```

---

### 11. `<br>`

- `<br>` tag inserts a single line break
- `<br/>` — auto closing tag

```html
<p>Line one<br/>Line two<br/>Line three</p>
```

```
output:
Line one
Line two
Line three
```

---

### 12. `<nav>`

- The `<nav>` tag defines a set of navigation links
- Not all links of a document should be inside a `<nav>` element — it is intended only for major blocks of navigation links

```html
<nav>
  <a href="/home">Home</a>
  <a href="/about">About</a>
  <a href="/contact">Contact</a>
</nav>
```

```
output:
Home   About   Contact
```

---

### 13. `<ul>` and `<li>`

- The `<ul>` tag defines an unordered (bulleted) list
- Use the `<ul>` tag together with the `<li>` tag to create an unordered list

```html
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ul>
```

```
output:
• HTML
• CSS
• JavaScript
```
