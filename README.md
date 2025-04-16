# HTML, CSS & JS Comprehensive Guide

## 1. `<picture>` Element vs. `<img>` with `srcset`

### Theory
The `<picture>` Element:
- Allows specifying multiple image sources based on media conditions
- Uses `<source>` elements for different media queries and image types
- Useful for art direction - providing different images or croppings for different viewport sizes

The `<img>` with `srcset`:
- Provides responsive images by offering image candidates with descriptors (width or pixel density)
- Browser picks the best-fit image based on inherent image conditions
- Cannot change the "art" or composition of the image

**When to Use Each:**
- Use `<picture>` when you need to change the image completely (different cropping or composition) based on viewport size
- Use `<img>` with `srcset` when you only need multiple resolutions of the same image

### Code Examples

Using `<picture>` for art direction:
```html
<picture>
  <!-- For wide screens -->
  <source media="(min-width: 800px)" srcset="images/landscape-large.jpg">
  <!-- For smaller screens -->
  <source media="(max-width: 799px)" srcset="images/landscape-small.jpg">
  <!-- Fallback image -->
  <img src="images/landscape-small.jpg" alt="A beautiful landscape">
</picture>
```

Using `<img>` with `srcset` for resolution switching:
```html
<img src="images/photo-1x.jpg"
     srcset="images/photo-1x.jpg 1x, images/photo-2x.jpg 2x"
     alt="A descriptive photo">
```

## 2. `defer` vs. `async` Attributes in `<script>`

### Theory
**defer:**
- Downloads script while continuing to parse HTML
- Executes script only after parsing is complete
- Scripts marked with `defer` preserve their execution order
- Ideal for scripts that depend on the full DOM

**async:**
- Downloads script while parsing HTML
- Executes script as soon as it's available, regardless of HTML parsing progress
- Order of execution is not guaranteed with multiple `async` scripts
- Best for independent scripts (tracking, analytics) that don't rely on the DOM

### Code Examples
```html
<!-- Deferred scripts execute in order after HTML parsing -->
<script src="script1.js" defer></script>
<script src="script2.js" defer></script>

<!-- Async script loads and executes as soon as ready -->
<script src="analytics.js" async></script>
```

## 3. Web Components: Shadow DOM, Custom Elements, and HTML Templates

### Theory
Web Components are a set of standards for creating reusable custom elements with encapsulated functionality and styling:

**Custom Elements:**
- Define new HTML tags with custom behavior

**Shadow DOM:**
- Provides encapsulated DOM and style scoping
- Prevents component styles from leaking out or being affected by global styles

**HTML Templates:**
- Define markup that isn't rendered until explicitly instantiated
- Ideal for repeating structures and reusable content

### Code Example
```html
<!-- Define a template -->
<template id="my-component-template">
  <style>
    .container {
      border: 2px solid #333;
      padding: 1rem;
      background-color: #f9f9f9;
    }
  </style>
  <div class="container">
    <h2>Custom Component</h2>
    <p>This is a reusable web component.</p>
  </div>
</template>

<script>
  // Define a custom element class
  class MyComponent extends HTMLElement {
    constructor() {
      super();
      // Attach a shadow DOM tree to this element.
      const shadow = this.attachShadow({mode: 'open'});
      // Find the template and clone its content.
      const template = document.getElementById('my-component-template');
      const templateContent = template.content.cloneNode(true);
      // Append the cloned template to the shadow root.
      shadow.appendChild(templateContent);
    }
  }
  // Register the custom element.
  customElements.define('my-component', MyComponent);
</script>

<!-- Use the custom element -->
<my-component></my-component>
```

## 4. `<datalist>` vs. `<select>` Dropdown

### Theory
**`<datalist>`:**
- Works as an autocomplete feature for `<input>` elements
- Provides suggestions while allowing any value to be entered
- More flexible but with less control

**`<select>` Dropdown:**
- Displays a closed list of predefined options
- User must choose from the provided options
- More structured and controlled

**Limitations of `<datalist>`:**
- Limited styling options (browser-dependent appearance)
- No guarantee of enforcing selection from the list
- Inconsistent support for features like grouping

### Code Examples

Using `<datalist>`:
```html
<input list="browsers" name="browser">
<datalist id="browsers">
  <option value="Chrome">
  <option value="Firefox">
  <option value="Safari">
  <option value="Edge">
</datalist>
```

Using `<select>`:
```html
<select name="browser">
  <option value="Chrome">Chrome</option>
  <option value="Firefox">Firefox</option>
  <option value="Safari">Safari</option>
  <option value="Edge">Edge</option>
</select>
```

## 5. Resource Hints: `rel="preload"`, `rel="preconnect"`, and `rel="prefetch"`

### Theory
**preload:**
- Instructs browser to load resources as soon as possible
- Used for critical assets like fonts, scripts, or stylesheets
- Prioritizes resources regardless of where they appear in the document

**preconnect:**
- Establishes early connections (DNS, TCP, TLS) to specified domains
- Reduces latency when resources are later fetched from those domains

**prefetch:**
- Provides hints about resources that might be needed in the future
- Browser fetches these resources during idle time
- Useful for resources needed for subsequent navigation

### Code Examples
```html
<!-- Preload critical stylesheet -->
<link rel="preload" href="styles/critical.css" as="style">
<link rel="stylesheet" href="styles/critical.css">

<!-- Preconnect to a third-party domain -->
<link rel="preconnect" href="https://api.example.com">

<!-- Prefetch resources for next page -->
<link rel="prefetch" href="next-page-content.html">
```

## 6. The `contenteditable` Attribute and Creating a Rich-Text Editor

### Theory
**contenteditable:**
- Makes an element editable in the browser
- Users can modify content directly on the page

**Rich-text editor creation:**
- Combine `contenteditable` with JavaScript toolbars for formatting
- Use `document.execCommand()` or modern libraries for editing functions

### Code Example
```html
<!-- Editable div for rich text -->
<div id="editor" contenteditable="true" style="border: 1px solid #ccc; padding: 10px;">
  <p>Edit this content...</p>
</div>

<!-- Simple toolbar using buttons -->
<button onclick="document.execCommand('bold')">Bold</button>
<button onclick="document.execCommand('italic')">Italic</button>
<button onclick="document.execCommand('underline')">Underline</button>
```

## 7. `<details>` and `<summary>` Elements

### Theory
**Usage:**
- `<details>` creates an interactive widget users can open and close
- `<summary>` provides a visible heading for the details section

**Accessibility Considerations:**
- Ensure `<summary>` text is descriptive
- Keyboard accessibility is built-in (Enter/Space to toggle)
- Screen readers announce when a section is expandable

### Code Example
```html
<details>
  <summary>More Information</summary>
  <p>Here is the additional content that can be toggled by the user.</p>
</details>
```

## 8. ARIA Attributes: `aria-label`, `aria-labelledby`, and `aria-describedby`

### Theory
**aria-label:**
- Provides an invisible label where a visible text label isn't present
- Useful for icons or complex controls

**aria-labelledby:**
- References the ID of another element that provides a label
- Used when the label is visible elsewhere in the DOM

**aria-describedby:**
- Identifies elements that describe the object
- Helpful for extra context, instructions, or error messages

**Usage Guidelines:**
- Use `aria-label` for simple, standalone labels
- Use `aria-labelledby` when you already have an associated element acting as a label
- Use `aria-describedby` for additional explanatory text

### Code Example
```html
<!-- Using aria-label -->
<button aria-label="Close" onclick="closeModal()">X</button>

<!-- Using aria-labelledby -->
<label id="usernameLabel" for="username">Username:</label>
<input id="username" type="text" aria-labelledby="usernameLabel">

<!-- Using aria-describedby -->
<input id="email" type="email" aria-describedby="emailHint">
<small id="emailHint">We will not share your email.</small>
```

## 9. The `sandbox` Attribute in `<iframe>`

### Theory
**Purpose:**
- Adds security restrictions on content rendered inside an `<iframe>`
- Disables features like form submission, script execution, and same-origin access unless explicitly allowed

**Secure Embedding of Third-Party Content:**
- Apply the `sandbox` attribute with appropriate flags to limit what third-party content can do
- Reduces risk of malicious behavior

### Code Example
```html
<iframe src="https://trusted-thirdparty.com"
        sandbox="allow-scripts allow-same-origin"
        width="600"
        height="400"
        title="Embedded Third Party Content">
</iframe>
```

## 10. Animated Portfolio Website

### Code Examples

**HTML (index.html):**
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Animated Portfolio</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <header>
    <h1>My Portfolio</h1>
    <nav>
      <a href="#about">About</a>
      <a href="#projects">Projects</a>
      <a href="#contact">Contact</a>
    </nav>
  </header>

  <section id="about" class="fade-in">
    <h2>About Me</h2>
    <p>I am a creative web developer passionate about animations and modern design.</p>
  </section>

  <section id="projects" class="slide-in">
    <h2>Projects</h2>
    <div class="project-cards">
      <div class="card">Project 1</div>
      <div class="card">Project 2</div>
      <div class="card">Project 3</div>
    </div>
  </section>

  <section id="contact" class="fade-in">
    <h2>Contact</h2>
    <p>Email me at <a href="mailto:me@example.com">me@example.com</a></p>
  </section>

  <footer>
    <p>© 2025 My Portfolio</p>
  </footer>
  <script src="scripts.js"></script>
</body>
</html>
```

**CSS (styles.css):**
```css
body {
  font-family: sans-serif;
  margin: 0;
  padding: 0;
  background: #f0f0f0;
  overflow-x: hidden;
}

header {
  background: #333;
  color: #fff;
  padding: 1rem;
  text-align: center;
}
header nav a {
  color: #fff;
  margin: 0 10px;
  text-decoration: none;
}

/* Animation keyframes */
@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}
@keyframes slideIn {
  from { transform: translateX(-100%); }
  to { transform: translateX(0); }
}

/* Apply animations */
.fade-in {
  animation: fadeIn 1s ease-in forwards;
}

.slide-in {
  animation: slideIn 1s ease-out forwards;
}

.project-cards {
  display: flex;
  justify-content: center;
  gap: 20px;
  padding: 2rem;
}
.card {
  background: #fff;
  padding: 1rem;
  border: 1px solid #ccc;
  width: 150px;
  text-align: center;
  box-shadow: 2px 2px 8px rgba(0,0,0,0.1);
}

/* Additional styling */
section {
  padding: 3rem 1rem;
  text-align: center;
}
footer {
  background: #333;
  color: #fff;
  text-align: center;
  padding: 1rem;
}
```

**JavaScript (scripts.js):**
```javascript
// Simple JS to enhance interactivity (e.g., smooth scrolling)
document.querySelectorAll('nav a').forEach(link => {
  link.addEventListener('click', function(event) {
    event.preventDefault();
    const targetId = this.getAttribute('href').substring(1);
    document.getElementById(targetId).scrollIntoView({ behavior: 'smooth' });
  });
});
```

## 11. CSS `contain` Property

### Theory
The `contain` property tells the browser that an element's subtree is isolated and doesn't affect the rest of the layout. This enables performance optimizations by limiting the scope of layout, style, and paint calculations.

### Code Example
```css
.card {
  contain: layout style;
  border: 1px solid #ccc;
  padding: 1rem;
}
```

## 12. Margin Collapse vs. Padding Collapse

### Theory
**Margin Collapse:**
- Vertical margins between block-level elements may combine (collapse) to form a single margin
- Occurs when there is no border, padding, or clearance between elements
- The resulting margin equals the larger of the two margins

**Padding:**
- Padding does not collapse
- Each element's internal padding remains intact

## 13. CSS Stacking Context

### Theory
A stacking context is a three-dimensional conceptualization that determines the rendering order of elements. Factors that create a new stacking context include:
- Elements with `position` (relative, absolute, fixed) and a `z-index` value other than `auto`
- Elements with CSS `opacity` less than 1
- Elements with `transform`, `filter`, or properties like `mix-blend-mode`

### Code Example
```css
.parent {
  position: relative;
  z-index: 1; /* creates a stacking context */
}
.child {
  position: relative;
  z-index: 2; /* within the parent's stacking context */
}
```

## 14. The `:has()` Pseudo-class

### Theory
**Overview:**
- The `:has()` pseudo-class allows selecting an element based on its children or related elements
- Powerful for "parent selection" scenarios previously difficult in CSS

**Limitations:**
- Browser support is still evolving (supported in modern Chrome, Edge, and Safari)
- Can be less performant if overused in large DOM trees

### Code Example
```css
/* Select any <div> that contains an <img> */
div:has(> img) {
  border: 2px solid #00f;
}
```

## 15. `transform` vs. `translate` vs. `position: absolute`

### Theory
**transform:**
- Applies transformations (rotate, scale, translate, etc.) to an element
- Often GPU-accelerated
- Doesn't force a reflow of the document, just repaint or composition

**translate:**
- Part of the CSS transform function
- Moves an element along X and Y axes
- Benefits from GPU acceleration

**position: absolute:**
- Removes the element from normal document flow
- Changing position might trigger reflow if surrounding elements depend on it
- Can be more performance-intensive in some cases

### Code Example
```css
.box {
  width: 100px;
  height: 100px;
  background: #f00;
  /* Using transform for smooth hardware-accelerated movement */
  transform: translate(50px, 50px);
}

/* Using absolute positioning */
.absolute-box {
  position: absolute;
  top: 50px;
  left: 50px;
  background: #0f0;
  width: 100px;
  height: 100px;
}
```

## 16. CSS Subgrid

### Theory
CSS Subgrid is an extension of CSS Grid that allows child elements to inherit grid line definitions from their parent. This solves layout problems where nested grid containers should align with the outer grid structure.

**Benefits over Regular Grid:**
- Enables consistent alignment of nested content
- Avoids redundancy by allowing child grid items to follow parent's grid lines

### Code Example
```html
<!-- Outer grid -->
<div class="grid-container">
  <div class="item">Header</div>
  <div class="subgrid">
    <!-- Child grid items follow the parent grid's columns -->
    <div>Sub-item 1</div>
    <div>Sub-item 2</div>
  </div>
</div>
```

```css
.grid-container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
}

.subgrid {
  display: grid;
  grid-column: span 3; /* spans across parent grid columns */
  grid-template-columns: subgrid;
}
```

**Note:** Browser support for subgrid is still emerging.

## 17. The `@layer` Rule in CSS Cascade Layers

### Theory
The `@layer` rule organizes CSS into distinct layers to manage specificity conflicts. By assigning rules into named layers, you ensure that styles from one layer don't inadvertently override others, simplifying maintenance in large projects.

### Code Example
```css
@layer reset, base, components, utilities;

@layer reset {
  html, body, div, span, applet, object, iframe {
    margin: 0;
    padding: 0;
  }
}

@layer base {
  body {
    font-family: sans-serif;
    line-height: 1.6;
  }
}

@layer components {
  .btn {
    background: #007bff;
    color: #fff;
    padding: 0.5rem 1rem;
  }
}

@layer utilities {
  .text-center {
    text-align: center;
  }
}
```

## 18. The `will-change` Property

### Theory
The `will-change` property hints to the browser that an element's property is likely to change, allowing the browser to make performance optimizations (like creating a new compositor layer) in anticipation.

**When to Use:**
- Use sparingly on elements that are animated or updated frequently

**When Not To:**
- Don't apply to too many elements
- Don't use for properties that rarely change

### Code Example
```css
.animate {
  will-change: transform, opacity;
}
```

## 19. `backface-visibility` and 3D Transforms

### Theory
The `backface-visibility` property determines whether the back face of an element is visible when rotated in 3D space.

**When set to hidden:**
- Back side will not be visible
- Prevents flickering or unwanted display when rotating

**Typical Use:**
- Used on elements being flipped or rotated in 3D space

### Code Example
```css
.flip-card {
  perspective: 1000px;
}
.flip-card-inner {
  transition: transform 0.8s;
  transform-style: preserve-3d;
  backface-visibility: hidden;
}
```

## 20. The `color-mix()` Function

### Theory
The `color-mix()` function allows blending of two colors in specified proportions. It can be used to derive new colors based on theme parameters, ideal for dynamic theming where you want to mix a base color with tints or shades.

### Code Example
```css
:root {
  --primary-color: #007bff;
  --secondary-color: #ff6347;
}

.button {
  /* Mix 70% primary and 30% secondary color */
  background-color: color-mix(in srgb, var(--primary-color) 70%, var(--secondary-color) 30%);
  color: #fff;
  padding: 0.5rem 1rem;
  border: none;
  cursor: pointer;
}
```




# UI Design Solutions

## Q1. Masonry grid

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Student Masonry Grid</title>
<style>
* {
box-sizing: border-box;
}
body {
font-family: Arial, sans-serif;
margin: 0;
padding: 10px;
background-color: #eaeaea;
}
h1 {
text-align: center;
margin-bottom: 20px;
}
.masonry {
column-count: 3;
column-width: 300px;
column-gap: 3rem;
}
.box {

background-color: white;
padding: 10px;
margin-bottom: 1rem;
border: 1px solid #ccc;
display: inline-block;
width: 100%;
border-radius: 15px;
}
.box img {
width: 100%;
height: auto;
display: block;
border-radius: 15px;
margin-bottom: 10px;
}
.box h3 {
margin-top: 0.5rem;
margin-bottom: 0.3rem;
}
.box p {
font-size: 14px;
}
</style>
</head>
<body>
<h1>My Masonry Grid</h1>
<div class="masonry">

<!-- Sample Posts -->
<div class="box">
<img src="https://picsum.photos/300/200?1" alt="image" />
<h3>Post 1</h3>
<p>This is a short description.</p>
</div>
<div class="box">
<img src="https://picsum.photos/300/250?2" alt="image" />
<h3>Post 2</h3>
<p>A slightly longer description with more text to show height.</p>
</div>
<div class="box">
<img src="https://picsum.photos/300/220?3" alt="image" />
<h3>Post 3</h3>
<p>Another post with a few lines of content. Looks decent, right?</p>
</div>
<div class="box">
<img src="https://picsum.photos/300/180?4" alt="image" />
<h3>Post 4</h3>
<p>Small one.</p>
</div>
<div class="box">
<img src="https://picsum.photos/300/240?5" alt="image" />
<h3>Post 5</h3>
<p>Trying to make the grid fill up nicely. Here's a bit more text to help.</p>
</div>
<div class="box">
<img src="https://picsum.photos/300/300?6" alt="image" />
<h3>Post 6</h3>
<p>This one has a taller image and a longer paragraph to show variety.</p>
</div>

<!-- Add more posts if needed -->
</div>
</body>
</html>
```

## Q2. Accessible modal dialog with focus trap

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Simple Accessible Modal</title>
<style>
body {
font-family: sans-serif;
padding: 2rem;
}
.modal-overlay {
position: fixed;
inset: 0;
background: rgba(0, 0, 0, 0.5);
display: flex;
align-items: center;
justify-content: center;
opacity: 0;
visibility: hidden;
transition: opacity 0.3s ease;
}

.modal-overlay.active {
opacity: 1;
visibility: visible;
}
.modal {
background: #fff;
padding: 1.5rem;
border-radius: 8px;
max-width: 400px;
width: 90%;
transform: translateY(-30px);
transition: transform 0.3s ease;
}
.modal-overlay.active .modal {
transform: translateY(0);
}
.modal button.close {
float: right;
font-size: 1.2rem;
background: none;
border: none;
cursor: pointer;
}
</style>
</head>
<body>

<button id="openBtn">Open Modal</button>
<div id="overlay" class="modal-overlay" role="dialog" aria-modal="true" aria-
labelledby="modalTitle">
<div class="modal">
<button class="close" id="closeBtn" aria-label="Close Modal">&times;</button>
<h2 id="modalTitle">Simple Modal</h2>
<p>This modal has animations and traps focus.</p>
<input type="text" placeholder="Try tabbing..." />
<button>Another Button</button>
</div>
</div>
<script>
const openBtn = document.getElementById('openBtn');
const overlay = document.getElementById('overlay');
const closeBtn = document.getElementById('closeBtn');
let focusableEls, firstEl, lastEl;
function openModal() {
overlay.classList.add('active');
setFocusableEls();
setTimeout(() => firstEl?.focus(), 100);
document.addEventListener('keydown', handleKeyDown);
}
function closeModal() {
overlay.classList.remove('active');
openBtn.focus();
document.removeEventListener('keydown', handleKeyDown);

}
function setFocusableEls() {
focusableEls = overlay.querySelectorAll('button, input, [href], [tabindex]:not([tabindex="-1"])');
firstEl = focusableEls[0];
lastEl = focusableEls[focusableEls.length - 1];
}
function handleKeyDown(e) {
if (e.key === 'Escape') closeModal();
if (e.key === 'Tab') {
if (e.shiftKey && document.activeElement === firstEl) {
e.preventDefault();
lastEl.focus();
} else if (!e.shiftKey && document.activeElement === lastEl) {
e.preventDefault();
firstEl.focus();
}
}
}
overlay.addEventListener('click', (e) => {
if (e.target === overlay) closeModal();
});
openBtn.addEventListener('click', openModal);
closeBtn.addEventListener('click', closeModal);
</script>
</body>
</html>
```

## Q3. Create a hamburger menu

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>CSS Hamburger Menu</title>
<style>
body {
margin: 0;
font-family: sans-serif;
overflow-x: hidden;
}
/* Hide the checkbox */
#menu-toggle {
display: none;
}
/* Hamburger icon */
.hamburger {
width: 30px;
height: 22px;
position: fixed;
top: 20px;
right: 20px;
z-index: 1001;
cursor: pointer;
display: flex;
flex-direction: column;

justify-content: space-between;
}
.hamburger span {
display: block;
height: 4px;
width: 100%;
background: #000;
border-radius: 2px;
transition: 0.4s ease;
}
/* Animate to X when checked */
#menu-toggle:checked + .hamburger span:nth-child(1) {
transform: rotate(45deg) translate(5px, 5px);
}
#menu-toggle:checked + .hamburger span:nth-child(2) {
opacity: 0;
}
#menu-toggle:checked + .hamburger span:nth-child(3) {
transform: rotate(-45deg) translate(6px, -6px);
}
/* Fullscreen Menu */
.menu {
position: fixed;
top: 0;
left: 100%;
width: 100%;

height: 100%;
background: #451f1f;
color: #fff;
display: flex;
flex-direction: column;
justify-content: center;
align-items: center;
transition: left 0.4s ease;
z-index: 1000;
}
#menu-toggle:checked ~ .menu {
left: 0;
}
.menu a {
text-decoration: none;
color: white;
font-size: 2rem;
margin: 1rem 0;
transition: color 0.3s;
}
.menu a:hover {
color: #f39c12;
}
</style>
</head>
<body>
<!-- Hidden Checkbox Toggle -->

<input type="checkbox" id="menu-toggle">
<!-- Hamburger Icon -->
<label for="menu-toggle" class="hamburger">
<span></span>
<span></span>
<span></span>
</label>
<!-- Fullscreen Menu -->
<nav class="menu">
<a href="#">Home</a>
<a href="#">About</a>
<a href="#">Services</a>
<a href="#">Contact</a>
</nav>
</body>
</html>
```

## Q4. Dynamic CSS variable theming with js

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Simple Theme Toggle</title>
<style>
:root {

--bg: #fff;
--text: #000;
--primary: #007bff;
}
[data-theme="dark"] {
--bg: #121212;
--text: #eee;
--primary: #ff9800;
}
body {
background: var(--bg);
color: var(--text);
font-family: sans-serif;
margin: 0;
padding: 2rem;
transition: background 0.3s, color 0.3s;
}
button {
background: var(--primary);
color: white;
border: none;
padding: 0.6rem 1rem;
font-size: 1rem;
border-radius: 4px;
cursor: pointer;
}
</style>
</head>

<body>
<h1>Simple Theme Toggle</h1>
<button id="toggle">Toggle Theme</button>
<script>
const btn = document.getElementById('toggle');
const savedTheme = localStorage.getItem('theme');
if (savedTheme === 'dark') {
document.documentElement.setAttribute('data-theme', 'dark');
} else {
document.documentElement.setAttribute('data-theme', 'light');
}
btn.addEventListener('click', function () {
const currentTheme = document.documentElement.getAttribute('data-theme');
if (currentTheme === 'dark') {
document.documentElement.setAttribute('data-theme', 'light');
localStorage.setItem('theme', 'light');
} else {
document.documentElement.setAttribute('data-theme', 'dark');
localStorage.setItem('theme', 'dark');
}
});
</script>
</body>
</html>
```

## Q5. Responsive multi-column form with flexbox

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Responsive Multi-Column Form</title>
<style>
* {
box-sizing: border-box;
}
body {
font-family: sans-serif;
padding: 2rem;
background: #f5f5f5;
}
.form-container {
background: #fff;
padding: 2rem;
border-radius: 12px;
max-width: 800px;
margin: auto;
}
.form-title {
font-size: 1.5rem;
margin-bottom: 1.5rem;
text-align: center;
}

.form-grid {
display: flex;
flex-wrap: wrap;
gap: 1rem;
}
.form-group {
flex: 1 1 45%; /* grow, shrink, basis */
display: flex;
flex-direction: column;
}
.form-group label {
margin-bottom: 0.5rem;
font-weight: bold;
}
.form-group input,
.form-group select,
.form-group textarea {
padding: 0.5rem;
border: 1px solid #ccc;
border-radius: 6px;
font-size: 1rem;
}
.full-width {
flex: 1 1 100%;
}
.submit-button {

margin-top: 1.5rem;
padding: 0.75rem 1.5rem;
font-size: 1rem;
background-color: #007bff;
color: white;
border: none;
border-radius: 6px;
cursor: pointer;
align-self: flex-end;
}
.submit-button:hover {
background-color: #0056b3;
}
@media (max-width: 600px) {
.form-group {
flex: 1 1 100%;
}
}
</style>
</head>
<body>
<form class="form-container">
<div class="form-title">Registration Form</div>
<div class="form-grid">
<div class="form-group">
<label for="fname">First Name</label>
<input type="text" id="fname" name="fname">
</div>

<div class="form-group">
<label for="lname">Last Name</label>
<input type="text" id="lname" name="lname">
</div>
<div class="form-group">
<label for="email">Email</label>
<input type="email" id="email" name="email">
</div>
<div class="form-group">
<label for="phone">Phone</label>
<input type="tel" id="phone" name="phone">
</div>
<div class="form-group full-width">
<label for="message">Message</label>
<textarea id="message" name="message" rows="4"></textarea>
</div>
</div>
<button type="submit" class="submit-button">Submit</button>
</form>
</body>
</html>
```

## Q6. CSS scroll snap – implement a horizontally scrolling section where each item snaps into place

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Horizontal Scroll Snap</title>
<style>

body {
margin: 0;
font-family: sans-serif;
background: #f0f0f0;
}
.scroll-container {
display: flex;
overflow-x: auto;
scroll-snap-type: x mandatory;
padding: 1rem;
gap: 1rem;
}
.scroll-item {
flex: 0 0 80%;
scroll-snap-align: center;
background-color: white;
border-radius: 10px;
padding: 2rem;
text-align: center;
font-size: 1.2rem;
min-height: 200px;
box-shadow: 0 4px 10px rgba(0,0,0,0.1);
}
@media (min-width: 768px) {
.scroll-item {
flex: 0 0 40%;
}
}

</style>
</head>
<body>
<div class="scroll-container">
<div class="scroll-item"> Project 1: Global Tracker</div>
<div class="scroll-item"> Project 2: Analytics Dashboard</div>
<div class="scroll-item"> Project 3: E-commerce Store</div>
<div class="scroll-item"> Project 4: Design System</div>
<div class="scroll-item"> Project 5: Mobile App</div>
</div>
</body>
</html>
```

## Q7. Glassmorphic card

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Glassmorphic Card</title>
<style>
body {
margin: 0;
padding: 0;
height: 100vh;
background: linear-gradient(135deg, #89f7fe, #66a6ff);
display: flex;
justify-content: center;
align-items: center;
font-family: sans-serif;

}
.glass-card {
width: 300px;
padding: 2rem;
border-radius: 20px;
background: rgba(255, 255, 255, 0.1);
backdrop-filter: blur(15px);
-webkit-backdrop-filter: blur(15px);
box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
border: 1px solid rgba(255, 255, 255, 0.3);
color: #fff;
text-align: center;
transition: transform 0.3s ease, box-shadow 0.3s ease;
}
.glass-card:hover {
transform: translateY(-10px) scale(1.03);
box-shadow: 0 12px 36px rgba(0, 0, 0, 0.3);
}
</style>
</head>
<body>
<div class="glass-card">
<h2>Glassmorphism</h2>
<p>This card has a frosted glass effect using CSS backdrop-filter.</p>
</div>
</body>
</html>
```

## Q8. Build a tabbed navigation system that switches content on click using css

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>CSS Tabs</title>
<style>
body {
font-family: sans-serif;
display: flex;
justify-content: center;
align-items: center;
height: 100vh;
margin: 0;
background: #f0f4f8;
}
.tabs {
width: 320px;
}
input[type="radio"] {
display: none;
}
.tab-labels {
display: flex;
}

label {
flex: 1;
padding: 1rem;
text-align: center;
cursor: pointer;
background: #ddd;
color: #333;
font-weight: bold;
transition: 0.3s;
}
label:hover {
background: #ccc;
}
input:checked + label {
background: #fff;
border-bottom: 2px solid #fff;
}
.content-container {
background: #fff;
padding: 1rem;
border: 1px solid #ccc;
border-top: none;
}
.content {
display: none;
}

#tab1:checked ~ .content-container #content1,
#tab2:checked ~ .content-container #content2,
#tab3:checked ~ .content-container #content3 {
display: block;
}
</style>
</head>
<body>
<div class="tabs">
<input type="radio" name="tabs" id="tab1" checked>
<input type="radio" name="tabs" id="tab2">
<input type="radio" name="tabs" id="tab3">
<div class="tab-labels">
<label for="tab1">Home</label>
<label for="tab2">Profile</label>
<label for="tab3">Settings</label>
</div>
<div class="content-container">
<div class="content" id="content1">
<p> Home tab content.</p>
</div>
<div class="content" id="content2">
<p> Profile tab content.</p>
</div>
<div class="content" id="content3">
<p> Settings tab content.</p>
</div>
</div>

</div>
</body>
</html>
```

## Q9. A real world scenario e-commerce dropdown menu

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Filter Dropdown</title>
<style>
body {
font-family: sans-serif;
background: #f5f5f5;
padding: 20px;
}
.filter-menu {
width: 250px;
background: #fff;
box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
}
.filter-category {
border-bottom: 1px solid #ddd;
}
.category-header {

display: block;
padding: 10px;
font-weight: bold;
cursor: pointer;
}
.category-toggle {
display: none;
}
.category-items {
display: none;
list-style: none;
margin: 0;
padding: 0;
}
.category-items li {
padding: 8px 15px;
cursor: pointer;
}
.category-items li:hover {
background: #eef3f8;
}
.category-toggle:checked + .category-items {
display: block;
}
</style>
</head>

<body>
<div class="filter-menu">
<div class="filter-category">
<label class="category-header" for="cat1">Department</label>
<input type="checkbox" id="cat1" class="category-toggle" />
<ul class="category-items">
<li>Electronics</li>
<li>Computers</li>
<li>Smart Home</li>
</ul>
</div>
<div class="filter-category">
<label class="category-header" for="cat2">Price</label>
<input type="checkbox" id="cat2" class="category-toggle" />
<ul class="category-items">
<li>Under $25</li>
<li>$25 to $50</li>
</ul>
</div>
<div class="filter-category">
<label class="category-header" for="cat3">Brands</label>
<input type="checkbox" id="cat3" class="category-toggle" />
<ul class="category-items">
<li>Apple</li>
<li>Samsung</li>
</ul>
</div>
</div>
</body>

</html>
```

## Q10. Complex table design - style a larger html table with alternating row colors, fixed headers and responsive behavior

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Simple Responsive Table</title>
<style>
body {
font-family: Arial, sans-serif;
padding: 20px;
}
.table-container {
overflow-x: auto;
border: 1px solid #ccc;
border-radius: 8px;
}
table {
width: 100%;
border-collapse: collapse;
min-width: 800px;
}
thead th {
      background-color: #333;
      color: white;
      padding: 12px;
      text-align: left;
      position: sticky;
      top: 0;
      z-index: 1;
    }
th {

padding: 12px;
text-align: left;
}
td {
padding: 12px;
border-top: 1px solid #ddd;
}
tr:nth-child(even) {
background-color: #73a77e;
}
tr:nth-child(odd) {
background-color: #4073ae;
}
tr:hover {
background-color: #e3f2fd;
}
@media (max-width: 600px) {
thead th, tbody td {
padding: 10px 8px;
font-size: 14px;
}
}
</style>

</head>
<body>
<h2>Simple Styled Table</h2>
<div class="table-container">
<table>
<tr><thead>
<th>#</th>
<th>Product</th>
<th>Category</th>
<th>Price</th>
<th>Stock</th>
<th>Rating</th></thead>
</tr>
<tr><td>1</td><td>Laptop</td><td>Electronics</td><td>$999</td><td>20</td><td>4.5</td></tr>
<tr><td>2</td><td>Headphones</td><td>Audio</td><td>$199</td><td>50</td><td>4.2</td></tr>
<tr><td>3</td><td>Smartphone</td><td>Electronics</td><td>$699</td><td>35</td><td>4.6</td></tr>
<tr><td>4</td><td>Keyboard</td><td>Accessories</td><td>$89</td><td>80</td><td>4.1</td></tr>
<tr><td>5</td><td>Mouse</td><td>Accessories</td><td>$49</td><td>120</td><td>4.3</td></tr>
</table>
</div>
</body>
</html>
```

## Q11. Traffic light

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Traffic Light</title>
<style>
body {
display: flex;
justify-content: center;
}
.traffic-light {
width: 100px;
background: #333;
border-radius: 20px;
padding: 20px;
box-shadow: 0 0 10px rgba(0,0,0,0.5);
}
.red {
background: red;
box-shadow: 0 0 15px red;
width: 60px;
height: 60px;
margin: 15px auto;
border-radius: 50%;
}
.yellow {
background: yellow;

box-shadow: 0 0 15px yellow;
width: 60px;
height: 60px;
margin: 15px auto;
border-radius: 50%;
}
.green {
background: limegreen;
box-shadow: 0 0 15px limegreen;
width: 60px;
height: 60px;
margin: 15px auto;
border-radius: 50%;
}
</style>
</head>
<body>
<div class="traffic-light">
<div class="red"></div>
<div class="yellow"></div>
<div class="green"></div>
</div>
</body>
</html>
```

## Q12. Make a web form that collects specific user input by restricting values using the min and max attribute

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Restricted Input Form</title>
</head>
<body>
<h2>User Info Form</h2>
<form>
<label for="age">Age (18 to 65):</label><br>
<input type="number" id="age" name="age" min="18" max="65" required><br><br>
<label for="rating">Service Rating (1 to 5):</label><br>
<input type="number" id="rating" name="rating" min="1" max="5" step="1" required><br><br>
<label for="dob">Date of Birth (1950 to 2005):</label><br>
<input type="date" id="dob" name="dob" min="1950-01-01" max="2005-12-31"
required><br><br>
<label for="quantity">Quantity (1 to 100):</label><br>
<input type="number" id="quantity" name="quantity" min="1" max="100"><br><br>
<button type="submit">Submit</button>
</form>
</body>
</html>
```

## Q13. Create accessible and responsive custom form elements (dropdown, check box, radio) using real world data like country list, skills, gender

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Accessible Responsive Form</title>
<style>
* {
box-sizing: border-box;
}
body {
font-family: Arial, sans-serif;
background: #f0f2f5;
padding: 2rem;
}
.form-container {
background: #fff;
padding: 2rem;
max-width: 700px;
margin: auto;
border-radius: 10px;
box-shadow: 0 0 10px rgba(0,0,0,0.1);
}
h2 {
text-align: center;
margin-bottom: 1.5rem;
}
.form-group {

margin-bottom: 1rem;
display: flex;
flex-direction: column;
}
label {
margin-bottom: 0.5rem;
font-weight: bold;
}
select, input[type="text"], textarea {
padding: 0.5rem;
font-size: 1rem;
border: 1px solid #ccc;
border-radius: 5px;
}
.options-group {
display: flex;
flex-wrap: wrap;
gap: 1rem;
}
.options-group label {
display: flex;
align-items: center;
gap: 0.5rem;
font-weight: normal;
cursor: pointer;
}

input[type="checkbox"], input[type="radio"] {
transform: scale(1.2);
}
.submit-btn {
margin-top: 1.5rem;
padding: 0.75rem 1.5rem;
font-size: 1rem;
background-color: #007bff;
color: white;
border: none;
border-radius: 6px;
cursor: pointer;
}
.submit-btn:hover {
background-color: #0056b3;
}
@media (max-width: 600px) {
.options-group {
flex-direction: column;
}
}
</style>
</head>
<body>
<form class="form-container">
<h2>User Info Form</h2>

<!-- Country Dropdown -->
<div class="form-group">
<label for="country">Country</label>
<select id="country" name="country" aria-label="Select your country">
<option value="">-- Select Country --</option>
<option value="us">United States</option>
<option value="in">India</option>
<option value="uk">United Kingdom</option>
<option value="ca">Canada</option>
<option value="au">Australia</option>
</select>
</div>
<!-- Skills Checkbox -->
<div class="form-group">
<label>Skills (select all that apply)</label>
<div class="options-group" role="group" aria-labelledby="skills">
<label><input type="checkbox" name="skills" value="html"> HTML</label>
<label><input type="checkbox" name="skills" value="css"> CSS</label>
<label><input type="checkbox" name="skills" value="js"> JavaScript</label>
<label><input type="checkbox" name="skills" value="python"> Python</label>
<label><input type="checkbox" name="skills" value="cpp"> C++</label>
</div>
</div>
<!-- Gender Radio Buttons -->
<div class="form-group">
<label>Gender</label>
<div class="options-group" role="radiogroup" aria-labelledby="gender">
<label><input type="radio" name="gender" value="male"> Male</label>
<label><input type="radio" name="gender" value="female"> Female</label>

<label><input type="radio" name="gender" value="other"> Other</label>
<label><input type="radio" name="gender" value="na"> Prefer not to say</label>
</div>
</div>
<button type="submit" class="submit-btn">Submit</button>
</form>
</body>
</html>
```
