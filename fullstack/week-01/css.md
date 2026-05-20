# CSS

CSS stands for Cascading Style Sheets. It is used to style our applications.

We can add CSS to your HTML app by using:

1. The style attribute (inline styles) — inline CSS
2. In an external CSS file — external CSS
3. Internal CSS — using `<style>` tag — internal CSS

---

## Approach 1: Inline CSS

Directly on the HTML tag using the `style` attribute.

```html
<body style="background-color: black;">
```

```
output:
┌──────────────────────────┐
│                          │
│   (black background)     │
│                          │
└──────────────────────────┘
```

---

## Approach 2: External CSS

- First create a new file in some folder — `index.css`
- Add code in it:

```css
body {
  background-color: black;
}
```

- Link CSS file to HTML inside the `<head>` tag:

```html
<link rel="stylesheet" href="index.css">
```

```
output: nothing visible — but styles from index.css now apply to the page
```

---

## Approach 3: Internal CSS

Add a new `<style>` tag inside the `<head>` tag.

```html
<head>
  <style>
    body {
      background-color: black;
    }
  </style>
</head>
```

---

## Common Style Attributes

---

### color

Sets the text color.

```css
p {
  color: red;
}
```

```
output:
Hello World   ← text appears in red
```

---

### background-color

Sets the background color.

```css
body {
  background-color: black;
}
```

```
output:
┌──────────────────────────┐
│                          │  ← black background
└──────────────────────────┘
```

---

### font-size

Sets the size of text.

```css
h1 {
  font-size: 32px;
}
```

```
output:
Big Heading    ← 32px text
```

---

### margin

Sets the outer space around an element. Gives space outside the div.

```css
div {
  margin: 20px;
}
```

```
output:
        ↑ margin
  ┌──────────────┐
  │     div      │
  └──────────────┘
        ↓ margin
```

---

### border

Sets the border around an element.

```css
div {
  border: 2px solid black;
}
```

```
output:
┌──────────────┐
│     div      │  ← border around it
└──────────────┘
```

---

### class

Selects the element with a specific class attribute. Used in CSS with `.` prefix.

```html
<!-- HTML -->
<h1 class="title">Hello</h1>
```

```css
/* CSS */
.title {
  color: blue;
  padding: 10px;
}
```

```
output:
Hello   ← blue text with 10px padding
```

---

### padding

Sets the inner space between the content and the border of an element.

```css
/* all four sides = 10px */
padding: 10px;

/* top | right | bottom | left */
padding: 5px 10px 15px 20px;
```

```
output:

padding: 10px
┌────────────────────┐
│                    │  ← 10px space on all sides
│      content       │
│                    │
└────────────────────┘

padding: 5px 10px 15px 20px
  5px  → top
  10px → right
  15px → bottom
  20px → left
```

> Note: if we have to give padding to multiple sides, use shorthand — same goes for margin.

---

## Flexbox

Flexbox is a CSS layout model designed to help with the arrangement of items within a container.

`justify-content` is used to define flexbox alignment.

```css
div {
  display: flex;
  justify-content: flex-start;
}
```

---

### justify-content values

```
flex-start — items align to the left
┌──────────────────────────────┐
│ [1] [2] [3]                  │
└──────────────────────────────┘

flex-end — items align to the right
┌──────────────────────────────┐
│                  [1] [2] [3] │
└──────────────────────────────┘

center — items align to the center
┌──────────────────────────────┐
│         [1] [2] [3]          │
└──────────────────────────────┘

space-between — equal space between items, no space on edges
┌──────────────────────────────┐
│ [1]          [2]         [3] │
└──────────────────────────────┘

space-around — equal space around each item
┌──────────────────────────────┐
│  [1]        [2]        [3]   │
└──────────────────────────────┘

space-evenly — exactly equal space between all items and edges
┌──────────────────────────────┐
│    [1]      [2]      [3]     │
└──────────────────────────────┘
```

---

## Classes and IDs

In CSS, classes and IDs are used as selectors to apply styles to HTML elements. They help in targeting specific elements for styling and can be used to enhance the modularity and reusability of CSS code.

```html
<!-- class — can be used on multiple elements -->
<h1 class="title">Hello</h1>
<p class="title">World</p>

<!-- id — should be unique to one element -->
<h1 id="main-heading">Hello</h1>
```

```css
/* class selector — dot prefix */
.title {
  color: blue;
}

/* id selector — hash prefix */
#main-heading {
  font-size: 40px;
}
```

```
output:
Hello   ← blue (class applied)
World   ← blue (same class)

Hello   ← 40px (id applied)
```

---

## Colors in CSS

Colors can be written in three ways:

```css
color: red;                 /* color name */
color: rgb(200, 100, 50);  /* r, g, b — each value 0 to 255 */
color: #ff5733;            /* hex code */
```

```
output:
Hello   ← red       (color name)
Hello   ← orange    (rgb)
Hello   ← orange-red (hex)
```
