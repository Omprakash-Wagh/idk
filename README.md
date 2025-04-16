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
