# 🧠 Frontend Interview Notes (v2: Interview-Ready)
### HTML → CSS → JavaScript → React (Basic → Advanced)

> **Sources:** 300 Frontend Interview Q&A (Ajeet Yadav PDF) · 50 React Qs (GreatFrontEnd) · 75+ JavaScript Qs (GreatFrontEnd, 2026)
> **How to use:** Read the bold answer, then say it out loud in your own words. Each answer is written to be spoken in about 20–30 seconds.

## 🎨 Legend

| Badge | Meaning |
|---|---|
| 🟢 **Basic** | Must know, warm-up |
| 🟡 **Medium** | Core interview level |
| 🟠 **Moderate** | Asked to test depth |
| 🔴 **Advanced** | Senior / tricky |
| 🔥 **Very important** | Code example included |
| 🔁 **Merged** | Same question in 2 sources, kept once |
| ⚠️ **Not legible** | Cut off in the scan, placeholder only |

---

# 📘 PART 1: HTML

## 🟢 Basic

**1. What is HTML?**
**HTML is the markup language that defines the structure and content of a web page.** It uses elements (tags) such as headings, paragraphs, and links. The browser parses the HTML into the DOM and renders it on screen.

**2. HTML vs XHTML?**
**HTML is lenient, case-insensitive, and some tags can be left unclosed.** **XHTML is a stricter, XML-based version where every tag must be closed and written in lowercase.** Modern projects use HTML5.

**3. 🔁 What are semantic elements?**
**Semantic elements describe the meaning of their content:** `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`. They help screen readers, search engines, and other developers understand the page, and they make code easier to read.

**4. `<div>` vs `<span>`?**
**`<div>` is a block-level container used to group larger sections.** **`<span>` is an inline element used to style small pieces of text.** Use `div` for layout structure and `span` for text-level styling.

**5. 🔁 Block vs inline elements?**
**Block elements take the full width and start on a new line** (`div`, `p`, `h1`, `section`). **Inline elements take only the width they need and stay on the same line** (`span`, `a`, `strong`, `img`). Block elements accept width and height; inline elements mostly ignore them.

**6. What is DOCTYPE?**
**`<!DOCTYPE html>` tells the browser which HTML version to use and turns on standards mode.** Without it, the browser may use quirks mode, which renders the page in an older, inconsistent way.

**7. What are meta tags?** *(Medium)*
**Meta tags are metadata placed in `<head>`:** charset, description, viewport, and so on. They are not displayed on the page, but browsers, search engines, and social platforms read them.

**8. What is the viewport meta tag?**
**It controls how the page scales on mobile screens.** Without it, phones show a zoomed-out desktop layout. It is required for responsive design.
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**9. `id` vs `class`?**
**An `id` is unique per page and selected with `#`.** **A `class` can be reused on many elements and selected with `.`.** Both are used for CSS styling and JavaScript selection.

**10. Absolute vs relative URLs?**
**An absolute URL includes the full domain** (`https://example.com/about`). **A relative URL is a path relative to the current page** (`/about`). Use relative URLs inside your own project so it works across environments.

**11. What are HTML entities?**
**Entities are codes for reserved or hard-to-type characters.** `&lt;` is `<`, `&gt;` is `>`, `&amp;` is `&`, `&quot;` is `"`, and `&#39;` is `'`. They let you display characters that would otherwise be read as markup.

**12. What are forms in HTML?**
**Forms collect user input and send it to a server.** They contain `input`, `textarea`, `select`, and `button` elements, and they are used for login, sign-up, and feedback.

**13. GET vs POST?**
**GET sends data in the URL, is cacheable, and has a size limit. It is used for retrieving data.** **POST sends data in the request body, has no practical size limit, and is used for submitting or changing data.** Neither is inherently secure without HTTPS.

**14. What are the HTML5 input types?**
**HTML5 added input types such as `email`, `number`, `date`, `range`, `color`, `tel`, and `url`.** They give built-in validation and show the right mobile keyboard, so you write less JavaScript.

## 🟡 Medium

**15.** ⚠️ *Not legible in the scan. Please send a clearer page.*

**16. 🔁 HTML5 new features?** *(Moderate)*
**HTML5 added semantic tags, native audio and video, canvas for drawing, `localStorage` and `sessionStorage`, geolocation, new input types, and WebSocket and Web Worker support.** It moved many features that used plugins into the browser.

**17. `<label>` vs placeholder?**
**A `label` is a permanent description of the field and is read by screen readers.** **A placeholder is a temporary hint that disappears when the user types.** Never use a placeholder as the only label.

**18. What is the `alt` attribute?**
**`alt` gives alternative text for an image.** It is shown if the image fails to load and is read by screen readers. It also helps SEO. Write meaningful text, and use an empty `alt=""` for purely decorative images.
```html
<img src="profile.jpg" alt="User profile photo">
```

**19. `tabindex` values?**
**`tabindex="0"` puts an element in the natural tab order.** **`tabindex="-1"` makes it focusable by script but not by the Tab key.** **Positive values break the natural order and should be avoided.**

**20. What are screen readers?**
**Screen readers are assistive tools that read page content aloud** (NVDA, JAWS, VoiceOver, TalkBack). They depend on semantic HTML and ARIA to understand the structure of the page.

**21. `<section>` vs `<article>`?**
**A `section` is a thematic group of related content on the page.** **An `article` is self-contained content that could be shared or reused on its own**, such as a blog post or a news story.

**22. What is the `<nav>` element?**
**`nav` wraps the main navigation links.** It tells screen readers and search engines that these links are navigation, so users can skip to them quickly.

**23. `<header>` vs `<head>`?**
**`head` holds metadata such as the title, meta tags, and linked CSS and scripts. It is not visible.** **`header` is a visible intro section at the top of a page or section**, often containing a logo and navigation.

**24. What is the `<main>` element?**
**`main` holds the main content of the page, and there should be only one per page.** Screen readers can jump straight to it, which saves users from tabbing through the header and navigation.

## 🟠 Moderate

**25. 🔁 Why is accessibility important?**
**Accessibility makes the web usable for people with visual, hearing, or motor disabilities.** It improves the experience for everyone, is required by many laws (for example WCAG), and helps SEO.

**26. How do you make a webpage keyboard accessible?** ⚠️ *(Answer partly reconstructed)*
**Use real interactive elements such as `button` and `a`, not clickable `div`s.** Keep a visible focus style, follow a logical tab order, and add a skip link for long navigation. Every feature should work without a mouse.

**27. How do you create an accessible form?**
**Give every input a `label`, show clear error messages, and use the correct input types.** Group related fields with `fieldset` and `legend`, and make sure the whole form works with the keyboard.
```html
<fieldset>
  <legend>Personal Details</legend>
  <label for="name">Name</label>
  <input id="name" type="text" required />
</fieldset>
```

## 🔴 Advanced

**28. 🔥 What are ARIA attributes?**
**ARIA (Accessible Rich Internet Applications) adds attributes such as `aria-label` and `role` to describe custom or dynamic widgets** that native HTML cannot express. **The first rule of ARIA is to use native HTML elements whenever they are enough.** Wrong ARIA is worse than none.
```html
<button aria-label="Close menu"><span class="icon">✕</span></button>
```

---

# 📗 PART 2: CSS

## 🟢 Basic

**31. What is CSS?**
**CSS (Cascading Style Sheets) controls the look and layout of HTML:** colors, fonts, spacing, and positioning. **It separates presentation from content.** It can be inline, internal, or external, and external is preferred.

**32. 🔥 What is the CSS box model?**
**Every element is a box made of content, padding, border, and margin.** **Total width is content + padding + border + margin.** By default, `width` applies only to the content, so `box-sizing: border-box` is often used to include padding and border.
```css
.box {
  width: 200px;
  padding: 10px;
  border: 2px solid black;
  margin: 20px;
  box-sizing: border-box;
}
```

**33. Margin vs padding?**
**Margin is the space outside the border and creates distance between elements.** **Padding is the space inside the border, between the content and the border.** Padding takes on the element's background color; margin does not.

**34. Values of `display`?**
**`display` controls how an element participates in layout.** `block` takes a full line, `inline` takes only its content width, `inline-block` lets you set width and height inline, `none` hides the element, `flex` and `grid` create layout containers, and `table` behaves like a table.

**35. What is the `position` property?**
**`position` controls how an element is placed.** `static` is the default in the normal flow. `relative` offsets from its normal place. `absolute` is placed relative to its nearest positioned ancestor. `fixed` is placed relative to the viewport. `sticky` switches between relative and fixed based on scroll.

**36. Relative vs absolute positioning?**
**`relative` shifts the element but keeps its original space in the layout.** **`absolute` removes the element from the flow and positions it relative to the nearest positioned ancestor.** Set `position: relative` on the parent to anchor an absolute child.

**37. Fixed vs sticky?**
**`fixed` stays in the same spot on screen, even while scrolling.** **`sticky` behaves normally until it reaches a scroll threshold, then sticks there within its parent.** A fixed navbar is always visible; a sticky header sticks only after you scroll past it.

**38. 🔥 What is CSS specificity?**
**Specificity decides which rule applies when several rules target the same element.** Inline styles score 1000, IDs 100, classes, attributes, and pseudo-classes 10, and element names 1. **If scores tie, the rule written later wins.** Avoid using IDs for styling to keep specificity low.

**39. What is the cascade?**
**The cascade is the process that resolves conflicts between rules.** It checks importance (`!important` first), then specificity, then source order. Inheritance fills in values when no rule applies.

**40. What is inheritance in CSS?**
**Some properties pass from parent to child automatically:** `color`, `font-family`, `font-size`, `line-height`, and `text-align`. **Layout properties such as `margin`, `padding`, and `border` are not inherited.** Use `inherit` to force it.

**41. What are pseudo-classes?**
**Pseudo-classes style an element based on its state, written with one colon.** Examples are `:hover`, `:focus`, `:active`, `:disabled`, `:checked`, `:first-child`, and `:nth-child()`.

**42. What are pseudo-elements?**
**Pseudo-elements style a part of an element, written with two colons.** Examples are `::before` and `::after` (for decorative content), `::first-line`, `::first-letter`, and `::placeholder`.

**43. 🔁 CSS units?**
**Absolute units (`px`, `pt`, `cm`) are fixed in size.** **Relative units (`%`, `em`, `rem`, `vw`, `vh`) scale with the context**, which is better for responsive design. `px` is precise, but `rem` and `%` adapt to user settings.

**44. `em` vs `rem`?**
**`em` is relative to the font size of its parent, so nested elements compound.** **`rem` is relative to the root `html` font size, so it stays predictable everywhere.** Use `rem` for most sizing and `em` when you want a size to scale with its own text.

## 🟡 Medium

**45.** ⚠️ *Not legible in the scan.*

**46. What is Flexbox?**
**Flexbox is a one-dimensional layout model for arranging items in a row or column.** It is great for navbars, toolbars, and centering. You set `display: flex` on the parent, then control alignment with `justify-content`, `align-items`, and `gap`.
```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
}
```

**47. 🔥 `justify-content` vs `align-items`?**
**`justify-content` aligns items along the main axis**, which is horizontal in a row. **`align-items` aligns items along the cross axis**, which is vertical in a row. Remember: justify is main, align is cross.

**48. What is the `gap` property?**
**`gap` sets the space between items in a flex or grid container.** It replaces margin hacks, and it does not add space at the outer edges. It is a shorthand for `row-gap` and `column-gap`.

**49. What are media queries?**
**Media queries apply CSS only when a condition is met,** such as screen width or orientation. They are the basis of responsive design.
```css
@media (max-width: 768px) {
  .container { flex-direction: column; }
}
```

**50. What are common breakpoints?**
**Common breakpoints are roughly: mobile below 768px, tablet 768 to 1024px, laptop 1024 to 1440px, and desktop above 1440px.** These are guidelines. Choose breakpoints based on where your content breaks.

## 🟠 Moderate

**51. 🔥 What is CSS Grid?**
**CSS Grid is a two-dimensional layout system that controls rows and columns at the same time.** It is best for full page layouts and complex grids. Use `repeat()` and `fr` units to build flexible columns.
```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
}
```

**52. Flexbox vs Grid?**
**Flexbox works in one dimension, while Grid works in two.** Use Flexbox for alignment within a single row or column, such as nav items. Use Grid when you need to control both rows and columns, such as a page layout.

**53. How do you define grid columns and rows?**
**Use `grid-template-columns` and `grid-template-rows` to set the number and size of tracks.** The `fr` unit splits the available space proportionally. For example, `1fr 2fr` gives the second column twice the space.

**54. 🔥 How do you make a design responsive?**
**Combine flexible units (`%`, `rem`, `vw`), flexible layouts (Flexbox and Grid), and media queries.** Images should use `max-width: 100%` so they scale down. The goal is one layout that adapts, not separate sites.

**55. 🔥 What is mobile-first design?**
**Mobile-first means you write the base styles for small screens, then add styles for larger screens with `min-width` media queries.** It is better for performance because small devices get the simplest CSS by default.
```css
.container { width: 100%; }

@media (min-width: 768px) {
  .container { width: 750px; }
}
```

## 🔴 Advanced

**56. What are CSS transitions?**
**Transitions animate a change between two states over a set duration.** You set the property to animate, the duration, and the timing function. They are usually triggered by a state change such as `:hover`.
```css
.button {
  background-color: blue;
  transition: background-color 0.3s ease;
}
.button:hover { background-color: darkblue; }
```

**57. What are CSS animations?**
**Animations use `@keyframes` to define multiple steps in an animation.** Unlike transitions, they can run automatically and loop. Prefer animating `transform` and `opacity`, because they are cheaper for the browser.
```css
@keyframes slideIn {
  from { transform: translateX(-100%); }
  to   { transform: translateX(0); }
}
.box { animation: slideIn 1s ease-out; }
```

**58–60.** ⚠️ *Not legible in the scan.*

---

# 📙 PART 3: JAVASCRIPT

## 🟢 Basic

**1. 🔁 `var`, `let`, and `const`?**
**`var` is function-scoped and can be redeclared.** **`let` is block-scoped and can be reassigned.** **`const` is block-scoped and cannot be reassigned**, though objects it holds can still change. Use `const` by default, `let` when you need to reassign, and avoid `var`.

**2. 🔁 `==` vs `===`?**
**`==` converts types before comparing, so `0 == false` is true.** **`===` compares both value and type without conversion, so `0 === false` is false.** Always use `===` unless you specifically want coercion. `Object.is()` is the strictest comparison and handles `NaN` and `-0`.

**3. 🔁 `null` vs `undefined`?**
**`undefined` means a value was declared but never assigned.** **`null` is an intentional "no value" that a developer sets on purpose.** Both are falsy. `typeof null` returns `'object'`, which is a long-standing quirk of the language.

**4. Truthy and falsy values?**
**Falsy values are `false`, `0`, `''`, `null`, `undefined`, `NaN`, and `0n`.** **Every other value is truthy,** including the string `'0'`, the string `'false'`, and empty arrays and objects. Conditions in `if` statements use this rule.

**5. 🔁 Primitive vs reference types?**
**Primitives are `string`, `number`, `boolean`, `null`, `undefined`, `symbol`, and `bigint`.** They are copied by value and immutable. **Reference types are objects, arrays, functions, and others.** Variables store a reference to them, so copying a variable does not copy the data.

**6. What is type coercion?**
**Type coercion is JavaScript converting one type to another automatically.** For example, `'5' - 2` is `3`, but `'5' + 2` is `'52'`. Coercion is why `===` is recommended.

**7. 🔁 Function declaration vs expression?**
**A function declaration is fully hoisted, so you can call it before the line where it is defined.** **A function expression assigned to a `var` is not usable before assignment**, which causes a `TypeError`. Declarations are hoisted; expressions are not.
```js
foo();                 // works
function foo() {}

bar();                 // TypeError
var bar = function () {};
```

**8. 🔁 Arrow functions?**
**Arrow functions are a shorter function syntax that does not have its own `this`.** **They inherit `this` from the surrounding scope**, so they are great for callbacks. They cannot be used as constructors and have no `arguments` object.
```js
const square = (n) => n * n;
```

**9. 🔁 Hoisting?**
**Hoisting moves declarations to the top of their scope during compilation.** `var` is set to `undefined` immediately. `let` and `const` stay in the Temporal Dead Zone (TDZ) until their line runs, so using them early throws a `ReferenceError`.

**10. 🔁 Scope and lexical scoping?**
**Scope decides where a variable can be accessed:** global, function, or block. **Lexical scoping means a function's scope is determined by where it is written, not where it is called.** That is what makes closures possible.

**11. 🔥 Destructuring?**
**Destructuring extracts values from arrays or objects into variables in one line.** It also supports default values and renaming. It is used heavily in React props and in function parameters.
```js
const [a, b] = [1, 2];
const { name, age = 18 } = { name: 'John' };
```

**12. 🔁 Spread vs rest?**
**Spread (`...`) expands an iterable into individual values.** **Rest (`...`) collects remaining values into an array or object.** Spread is used for copying and merging; rest is used for variable-length function arguments.
```js
const copy = [...arr];
function sum(...nums) { return nums.reduce((a, b) => a + b, 0); }
```

**13. Ways to create objects?**
**You can create objects with an object literal `{}`, `new Object()`, `Object.create(proto)`, a constructor function with `new`, or a `class`.** Literals are the most common. `Object.create` lets you set the prototype directly.

**14. Iterating objects and arrays?**
**For objects, use `Object.keys`, `Object.values`, or `Object.entries`.** **For arrays, use `for...of` for values and `forEach` for callbacks.** Avoid plain `for...in` on objects because it also includes inherited keys.

**15. 🔁 Array methods: map, filter, reduce, forEach, find, findIndex?**
**`map` transforms each item into a new array.** **`filter` keeps items that pass a test.** **`reduce` combines all items into one value.** **`forEach` loops but returns nothing.** **`find` returns the first matching item; `findIndex` returns its index.** ⚠️ *Q90 partly cut in the scan.*
```js
const nums = [1, 2, 3, 4];
nums.map(n => n * 2);                  // [2, 4, 6, 8]
nums.filter(n => n % 2 === 0);         // [2, 4]
nums.reduce((acc, n) => acc + n, 0);   // 10
```

**16. Flatten arrays?**
**`flat()` flattens nested arrays up to a given depth.** `flat(Infinity)` flattens completely. Before ES2019, people used `reduce` with recursion.
```js
[1, [2, [3]]].flat(Infinity); // [1, 2, 3]
```

**17. Merge objects and arrays?**
**Use spread to merge: `{ ...obj1, ...obj2 }` or `[...a1, ...a2]`.** When keys clash, the later one wins. The merge is shallow, so nested objects need a deep merge or Lodash `_.merge`.
```js
const merged = { ...obj1, ...obj2 };
```

**18. 🔁 Shallow vs deep copy?**
**A shallow copy copies only the top level, so nested objects are still shared.** **A deep copy duplicates everything.** Use `structuredClone(obj)` for deep copies. Avoid `JSON.parse(JSON.stringify())` because it drops `undefined`, functions, and `Date` objects.

**19. 🔁 Map vs object? Map/Set vs WeakMap/WeakSet?**
**A `Map` accepts any key type, keeps insertion order, and has a `.size` property.** **`WeakMap` and `WeakSet` accept only object keys, are not iterable, and let garbage collection remove entries** when the key object is no longer used.

## 🟡 Medium

**20. 🔥 What is `this`?** 🔁
**`this` is determined by how a function is called, not where it is defined.** With `new`, it is the new object. With `call`, `apply`, or `bind`, it is the object you pass. As a method, it is the object before the dot. Arrow functions inherit it from the surrounding scope.
```js
const obj = {
  name: 'Alice',
  greet() { console.log(this.name); },   // 'Alice'
  arrow: () => console.log(this.name),   // undefined
};
```

**21. `call` vs `apply`?**
**Both call a function with a chosen `this`.** **`call` takes arguments one by one, while `apply` takes an array.** Memory aid: **C** for call and comma, **A** for apply and array.

**22. What is `bind`?**
**`bind` returns a new function with `this` permanently set.** You can also preset some arguments. It is useful for passing methods as callbacks without losing context.
```js
const getAge = john.getAge.bind(john);
```

**23. Why use arrow functions in constructors?**
**Arrow functions defined in a constructor capture `this` from the instance,** so passing them around does not lose context. This was a common fix before hooks in React class components.

**24. 🔥 What is a closure?**
**A closure is a function that remembers variables from its outer scope even after the outer function has returned.** This allows data privacy and factory functions. A typical use is a counter whose `count` cannot be changed from outside.
```js
function makeCounter() {
  let count = 0;
  return () => ++count;
}
const counter = makeCounter();
counter(); // 1
counter(); // 2
```

**25. What is the execution context?**
**An execution context is the environment in which JavaScript code runs.** There are three types: global, function, and eval. Each one has its own variable environment and `this` binding, and they are stacked on the call stack.

**26. What is a higher-order function?**
**A higher-order function takes a function as an argument, returns one, or both.** `map`, `filter`, and `setTimeout` are examples. They allow reusable behavior.
```js
const double = (factor) => (num) => num * factor;
```

**27. What are callbacks?**
**A callback is a function passed to another function and called later,** usually when an asynchronous task completes or an event fires. Too many nested callbacks led to "callback hell," which Promises and async/await solved.

**28. 🔥 Debouncing and throttling?** 🔁
**Debouncing runs a function only after events stop for a set delay,** such as a search box waiting for typing to stop. **Throttling runs the function at most once per interval,** such as scroll or resize handlers.
```js
function debounce(fn, delay) {
  let id;
  return (...args) => {
    clearTimeout(id);
    id = setTimeout(() => fn.apply(this, args), delay);
  };
}

function throttle(fn, limit) {
  let inThrottle = false;
  return (...args) => {
    if (inThrottle) return;
    fn.apply(this, args);
    inThrottle = true;
    setTimeout(() => (inThrottle = false), limit);
  };
}
```

**29. What is memoization?**
**Memoization caches the result of a function for given inputs so repeated calls are fast.** It trades memory for speed. It only works well for pure functions.
```js
function memoize(fn) {
  const cache = {};
  return (n) => (cache[n] ??= fn(n));
}
```

**30. 🔥 Event bubbling and capturing?** 🔁
**Bubbling sends an event from the target up through its ancestors, which is the default.** **Capturing goes from the root down to the target** and is enabled with `{ capture: true }`. Use `stopPropagation()` to stop the event from going further.
```js
child.addEventListener('click', e => e.stopPropagation());
```

**31. 🔥 Event delegation?** 🔁
**Event delegation attaches one listener to a parent and uses `event.target` to find the child that was clicked.** It uses less memory and works for elements added later, because the parent listener catches their events.
```js
list.addEventListener('click', (e) => {
  if (e.target.tagName === 'LI') console.log(e.target.textContent);
});
```

**32. `mouseenter` vs `mouseover`?**
**`mouseenter` fires once when the pointer enters the element and does not bubble.** **`mouseover` bubbles and fires again each time the pointer moves onto a child element.** Use `mouseenter` for hover effects.

**33. 🔁 Synchronous vs asynchronous?**
**Synchronous code runs one step at a time and blocks until each step finishes.** **Asynchronous code starts a task such as a timer or network call and continues immediately,** then handles the result later through callbacks or Promises.

**34. 🔥 The event loop, call stack, and queues?** 🔁
**The call stack runs synchronous code one function at a time.** Browser APIs handle timers and network calls outside the stack. **When a task finishes, its callback goes to a queue.** **Microtasks such as Promise callbacks run before the next macrotask such as `setTimeout`.**
```js
console.log('Start');
setTimeout(() => console.log('Timeout'), 0);
Promise.resolve().then(() => console.log('Promise'));
console.log('End');
// Start, End, Promise, Timeout
```

**35. 🔁 DOM selection and manipulation?**
**Use `getElementById` for one element by id and `querySelector` for the first match of any CSS selector.** `querySelectorAll` returns a static NodeList. Change content with `textContent` and classes with `classList`, which is cleaner than editing `className`.
```js
document.getElementById('id');
document.querySelector('.class');
el.textContent = 'Hello';
el.classList.add('active');
```

**36. `preventDefault` vs `stopPropagation`?**
**`preventDefault()` stops the browser's default action, such as a form submitting or a link navigating.** **`stopPropagation()` stops the event from bubbling to parent elements.** They solve different problems and are often used together.

**37. 🔥 `localStorage`, `sessionStorage`, and cookies?** 🔁
**`localStorage` stores about 5 MB, persists until cleared, and is not sent to the server.** **`sessionStorage` is similar but clears when the tab closes.** **Cookies are small (about 4 KB), can expire, and are sent with every HTTP request,** which is why they are used for auth sessions.
```js
localStorage.setItem('user', 'john');
localStorage.getItem('user');
```

**38. IndexedDB?**
**IndexedDB is a built-in browser database for large amounts of structured data.** It supports transactions and indexes, so it works offline. Use it for PWAs and data-heavy apps where localStorage is too small or too simple.

**39. History API?**
**The History API changes the URL and browser history without reloading the page.** `pushState` adds an entry, `replaceState` swaps the current one, and `back` goes back. Single-page app routers use it to make navigation feel native.

**40. `<script>`, `async`, and `defer`?** 🔁
**A plain `<script>` pauses HTML parsing while it downloads and runs.** **`async` downloads in parallel and runs as soon as it is ready,** so the order is not guaranteed. **`defer` downloads in parallel and runs after the HTML is parsed, in order.** Use `defer` for app code.

**41. Encapsulation and abstraction?**
**Encapsulation hides internal state and exposes only controlled methods,** using closures or `#private` fields. **Abstraction shows only the interface a user needs and hides the implementation.** Both make code easier to change safely.

## 🟠 Moderate

**42. 🔥 Promises?**
**A Promise represents a value that will be available later.** **It is in one of three states: pending, fulfilled, or rejected, and it can settle only once.** You chain `.then` for success and `.catch` for errors, and each `.then` returns a new Promise.
```js
fetch('/api/user')
  .then(res => res.json())
  .then(user => console.log(user))
  .catch(err => console.error(err));
```

**43. 🔥 `async` / `await`?** 🔁
**`async/await` is syntax over Promises that makes async code read top to bottom.** **An `async` function always returns a Promise, and `await` pauses that function until the Promise settles.** Wrap awaits in `try/catch` for error handling.
```js
async function getData() {
  try {
    const res = await fetch('/api/data');
    return await res.json();
  } catch (err) {
    console.error(err);
  }
}
```

**44. 🔥 `Promise.all`?** 🔁
**`Promise.all` runs several Promises in parallel and waits for all of them.** **It resolves with an array of results in the same order, but rejects as soon as any one fails.** Use it when all results are required.
```js
const [a, b] = await Promise.all([fetch('/a'), fetch('/b')]);
```

**45. `Promise.allSettled`?** 🔁
**`Promise.allSettled` waits for every Promise, whether it succeeds or fails.** **Each result is reported as `{ status, value }` or `{ status, reason }`.** Use it when you want partial results, such as loading independent widgets.

**46. `Promise.race`?**
**`Promise.race` settles with whichever Promise finishes first, success or failure.** It is commonly used to add a timeout to a request.

**47. `Promise.any`?** 🔁
**`Promise.any` resolves with the first Promise that succeeds.** **It rejects only if every Promise fails,** with an `AggregateError` holding all the errors. Use it for "first successful mirror wins" patterns.

**48. 🔥 AJAX, XHR, and `fetch`?** 🔁
**AJAX means fetching data without reloading the page.** **`XMLHttpRequest` is the older, event-driven API, and it supports upload progress.** **`fetch` is the modern Promise-based API,** cleaner to use and paired with `AbortController` for cancellation. It rejects only on network errors, so check `res.ok` for HTTP errors.
```js
fetch('/api/todos/1')
  .then(res => res.json())
  .then(console.log);
```

**49. `AbortController`?**
**`AbortController` cancels an in-flight request or other async operation.** You pass its `signal` to `fetch` and call `abort()` when you no longer need the result, such as when a component unmounts.
```js
const controller = new AbortController();
fetch('/api/slow', { signal: controller.signal });
controller.abort();
```

**50. Event Emitter?**
**An Event Emitter lets objects subscribe to named events and publish them.** It follows the observer pattern: `on(event, fn)` subscribes and `emit(event, data)` notifies every subscriber. It is the basis of Node's event system.

**51. 🔥 Prototypes and the prototype chain?** 🔁
**Every object has a hidden link to a prototype object.** **When a property is missing, JavaScript looks it up the chain until it reaches `null`.** Methods are shared through the prototype instead of being copied into each object.
```js
function Animal(name) { this.name = name; }
Animal.prototype.speak = function () { console.log(this.name); };
const dog = new Animal('Rex');
dog.speak(); // Rex
```

**52. 🔁 Classes and inheritance?**
**`class` is syntactic sugar over prototypes.** **`extends` sets up inheritance, and `super()` calls the parent constructor.** Under the hood, the same prototype chain is used.
```js
class Animal {
  constructor(name) { this.name = name; }
  speak() { return `${this.name} makes a sound`; }
}
class Dog extends Animal {
  speak() { return `${this.name} barks`; }
}
```

**53. `new` vs a plain call vs a declaration?**
**`new` creates a new object, links it to the constructor's prototype, and returns it.** **A plain call runs the function normally and returns whatever it returns.** **A declaration only defines the function; nothing runs until it is called.**

**54. Generators?**
**Generators are functions that can pause with `yield` and resume with `next()`.** They produce values lazily. `async/await` is built on the same pause-and-resume idea.
```js
function* counter() { yield 1; yield 2; }
```

**55. Iterators and `Symbol.iterator`?**
**An object is iterable if it has a `[Symbol.iterator]()` method.** That makes it work with `for...of` and spread. The easiest way to implement it is with a generator method.

**56. Iterator helpers and `Array.fromAsync`?**
**Iterator helpers such as `.map`, `.filter`, and `.take` process values lazily,** one at a time, without creating intermediate arrays. **`Array.fromAsync` collects an async iterable into an array.**

**57. Dynamic `import()`?**
**Dynamic `import()` loads a module at runtime and returns a Promise.** It is used for code splitting and loading features only when needed, which reduces the initial bundle size.

**58. ES Modules vs CommonJS?**
**ES Modules (`import`/`export`) are static, asynchronous, and support tree-shaking, so unused code can be removed.** **CommonJS (`require`) is the older Node format and loads synchronously.** New code should use ES Modules.

**59. Tagged template literals?**
**A tag function receives the parts of a template string and the interpolated values.** This lets you escape HTML safely or process GraphQL or CSS-in-JS templates.

**60. `replaceAll()`?**
**`replaceAll()` replaces every occurrence of a string or a global regex.** Before it existed, you needed a regex with the `g` flag to replace all matches.

**61. 🔥 Optional chaining and nullish coalescing?** 🔁
**`?.` returns `undefined` instead of throwing when a value is `null` or `undefined`.** **`??` returns the right side only for `null` or `undefined`, while `||` also replaces `0`, `''`, and `false`.**
```js
user.profile?.name;
const port = config.port ?? 3000;  // 0 is kept
const port2 = config.port || 3000; // 0 is replaced
```

**62. Logical assignment (`||=`, `&&=`, `??=`)?**
**These assign only when a condition holds.** For example, `config.retries ??= 3` sets retries only if it is `null` or `undefined`.

## 🔴 Advanced

**63. 🔁 Deep equality?**
**Deep equality compares the contents of two values, not their references.** The function checks types first, then compares keys and values recursively. Handle `null` and arrays carefully.
```js
function deepEqual(a, b) {
  if (a === b) return true;
  if (typeof a !== 'object' || typeof b !== 'object' || !a || !b) return false;
  const ka = Object.keys(a), kb = Object.keys(b);
  if (ka.length !== kb.length) return false;
  return ka.every(k => deepEqual(a[k], b[k]));
}
```

**64. `var` vs `let` in a `setTimeout` loop?**
**With `var`, every callback shares one `i`, which ends at 3, so all three print 3.** **With `let`, each loop iteration gets its own `i`,** so the output is 0, 1, 2. This is the classic closure-in-loop question.
```js
for (var i = 0; i < 3; i++) setTimeout(() => console.log(i)); // 3 3 3
for (let i = 0; i < 3; i++) setTimeout(() => console.log(i)); // 0 1 2
```

**65. Private class fields (`#field`)?**
**`#field` is a true private field enforced by the language.** It cannot be read from outside the class, from subclasses, or through `Object.keys`. It is stronger than the old `_field` naming convention.

**66. `error.cause`?**
**`error.cause` lets you attach the original error when you rethrow a new one.** The stack and details of the original error are kept, which helps debugging.
```js
throw new Error('Failed to load user', { cause: originalError });
```

**67. Immutable array methods (`toSorted`, `toReversed`, `toSpliced`, `with`)?**
**These return a new array instead of changing the original.** They are safe for React state and frozen data. `findLast` and `findLastIndex` search from the end.

**68. `Object.groupBy` and `Map.groupBy`?**
**They group an iterable's items by the result of a callback.** `Object.groupBy` uses string keys, while `Map.groupBy` allows any value as a key. They replace the manual `reduce` grouping pattern.

**69. Set methods (`union`, `intersection`, `difference`)?**
**These are built-in set operations in ES2025.** They return a new `Set` and accept any iterable, so you no longer need to write filter-based code by hand.

**70. `structuredClone` and BigInt?**
**`structuredClone` deep-copies data, including `Date`, `Map`, `Set`, and cycles.** **BigInt (`123n`) handles integers beyond `Number.MAX_SAFE_INTEGER`,** which is 2⁵³ − 1. Use it for large IDs and precise money in minor units.

**71. ⚠️ Q75 and Q82 are missing from the scan.**

---

# 📕 PART 4: REACT

## 🟢 Basic

**1. 🔁 What is React?**
**React is a JavaScript library for building user interfaces out of reusable components.** It uses a virtual DOM for efficient updates and a declarative style, where you describe what the UI should look like for a given state. It was created by Meta.

**2. React Node vs Element vs Component?**
**A Node is anything React can render, such as an element, string, number, or `null`.** **An Element is a plain, immutable description of what to render, created by JSX.** **A Component is a function or class that returns elements.**

**3. 🔥 What is JSX?** 🔁
**JSX is a syntax extension that lets you write HTML-like markup inside JavaScript.** Babel compiles it into `React.createElement` calls. Use `className` instead of `class`, and return a single root element or a Fragment.
```jsx
const el = <h1 className="title">Hello</h1>;
// compiles to React.createElement('h1', { className: 'title' }, 'Hello')
```

**4. JSX vs JavaScript?**
**JSX is not a separate language. It is syntax that compiles to JavaScript.** It uses camelCase attributes such as `className` and `onClick`, and expressions go inside `{}`.

**5. Functional vs class components?**
**Functional components are plain functions that use hooks, and they are the modern standard.** **Class components use `this.state` and lifecycle methods and are rarely written in new code.**

**6. 🔥 State vs props?** 🔁
**Props are read-only inputs passed from a parent to a child.** **State is data owned by a component that changes over time.** When state changes, the component re-renders. When props change, the child re-renders with the new values.

**7. 🔥 `useState`?**
**`useState` adds state to a function component.** It returns the current value and a setter. Calling the setter schedules a re-render with the new value.
```jsx
function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(c => c + 1)}>{count}</button>;
}
```

**8. 🔥 Virtual DOM and reconciliation?** 🔁
**The virtual DOM is a lightweight JavaScript copy of the UI tree.** **When state changes, React builds a new tree, diffs it against the previous one, and updates only the changed parts of the real DOM.** This process is called reconciliation.

**9. What does re-rendering mean?**
**Re-rendering means React calls a component function again** because its state, props, or context changed. Re-rendering is not the same as updating the DOM; React updates the DOM only where the output differs.

**10. 🔥 Lists and `key`?** 🔁
**Keys help React identify which list item is which across renders.** **Use a stable, unique ID, not the array index, especially if items can be reordered, added, or removed.** Bad keys cause wrong state and slow updates.
```jsx
{items.map(item => <Item key={item.id} value={item.value} />)}
```

**11. 🔥 Controlled vs uncontrolled components?** 🔁
**In a controlled component, React state is the single source of truth for the input's value.** **In an uncontrolled component, the DOM holds the value, and you read it with a ref.** Controlled inputs are easier to validate; uncontrolled inputs are simpler for basic forms.
```jsx
// Controlled
const [name, setName] = useState('');
<input value={name} onChange={e => setName(e.target.value)} />

// Uncontrolled
const ref = useRef();
<input ref={ref} />  // read with ref.current.value
```

**12. Fragments?**
**Fragments group multiple elements without adding an extra DOM node.** Use the shorthand `<>...</>`, or `<React.Fragment key={...}>` when you need a key.

**13. Rules of hooks?**
**Call hooks only at the top level of a component or custom hook,** never inside loops, conditions, or nested functions. **React relies on the call order of hooks to match state to them,** so breaking the order breaks state.

## 🟡 Medium

**14. 🔥 `useEffect`?** 🔁
**`useEffect` runs side effects after render, such as fetching data, subscriptions, or timers.** **The dependency array controls when it runs:** `[]` means once after mount, `[a, b]` means when `a` or `b` change, and no array means after every render. **Return a cleanup function to undo the effect.**
```jsx
useEffect(() => {
  const id = setInterval(tick, 1000);
  return () => clearInterval(id);   // cleanup
}, []);
```

**15. `useEffect` vs `useLayoutEffect`?** 🔁
**`useEffect` runs after the browser paints, so it does not block the screen.** **`useLayoutEffect` runs after DOM changes but before paint,** so it is used when you must measure or adjust the DOM before the user sees it. Prefer `useEffect` unless you have a visual reason.

**16. 🔁 `useRef`?**
**`useRef` returns a mutable object whose `.current` value persists across renders.** **Changing `.current` does not cause a re-render.** Use it for DOM access, such as focusing an input, or for storing values that should not trigger updates.
```jsx
const inputEl = useRef(null);
useEffect(() => inputEl.current.focus(), []);
```

**17. setState callback form and batching?** 🔁
**Use the function form `setCount(c => c + 1)` when the new value depends on the previous one.** **React 18 batches multiple state updates into one render,** including inside promises and timeouts, which reduces unnecessary re-renders.

**18. Resetting state?**
**Set the state back to its initial value, or change the component's `key` so React remounts it with fresh state.** Changing the key is often the cleanest way to reset a whole form.

**19. Why not mutate state?**
**React detects changes by comparing references.** **If you mutate an object or array in place, the reference stays the same, so React may skip the re-render.** Always create a new object or array when you update state.

**20. Data fetching in React?**
**Fetch inside `useEffect`, track `loading` and `error` states, and clean up to avoid stale updates.** Without cleanup, a slow response for an old request can overwrite the newer data.
```jsx
useEffect(() => {
  let cancelled = false;
  fetch('/api/data').then(r => r.json()).then(d => !cancelled && setData(d));
  return () => { cancelled = true; };
}, []);
```

**21. Benefits of hooks?**
**Hooks let function components use state and effects,** which removes class boilerplate, groups related logic together, and makes logic easy to reuse through custom hooks.

**22. 🔥 Context API?** 🔁
**Context shares data across the component tree without passing props at every level.** It is ideal for slow-changing global data such as theme, auth, or locale. **Every component that reads the context re-renders when its value changes,** so keep the value stable and split contexts when needed.
```jsx
const ThemeContext = createContext('light');

<ThemeContext.Provider value="dark">
  <Navbar />
</ThemeContext.Provider>

const theme = useContext(ThemeContext);
```

**23. Prop drilling and how to avoid it?** 🔁
**Prop drilling is passing props through several layers that do not use them.** **Avoid it with Context for shared data, a state library such as Redux or Zustand, or component composition** where you pass the component itself as children.

**24. 🔥 `useReducer`?** 🔁
**`useReducer` manages complex state with a reducer function and actions.** **Use it when state has several related fields or many transitions.** The reducer is a pure function that returns the next state for each action.
```jsx
function reducer(state, action) {
  switch (action.type) {
    case 'INC': return { count: state.count + 1 };
    case 'DEC': return { count: state.count - 1 };
    default: return state;
  }
}
const [state, dispatch] = useReducer(reducer, { count: 0 });
```

**25. `useId`?**
**`useId` generates a unique, stable ID for each component instance.** It is used to link a label to its input for accessibility, and it works correctly during server rendering.

**26. Error boundaries?**
**An error boundary is a class component that catches render errors in its children and shows a fallback UI.** It does not catch errors in event handlers or async code, and it is used in addition to try/catch.

**27. Portals?**
**`createPortal` renders children into a different DOM node,** such as `document.body`, while keeping them in the React tree. It is used for modals, tooltips, and anything that must escape overflow or z-index limits.

**28. Testing and debugging?**
**Test components with Jest and React Testing Library, focusing on what the user sees and does.** Debug with React DevTools to inspect the component tree and props, and use `console.log` for quick checks.

**29. React Strict Mode?**
**Strict Mode runs extra development-only checks.** It warns about unsafe patterns and runs effects and renders twice to expose side-effect bugs. It has no effect on production builds.

**30. Localization?**
**Use a library such as `react-i18next` or `react-intl`, store translation files per language, and read text through a hook such as `useTranslation()`.** This keeps text out of components.

**31. 🔥 Lazy loading and Suspense?** 🔁
**`React.lazy` loads a component only when it is first rendered,** and `Suspense` shows a fallback while it loads. Together they split the bundle and reduce the initial load time.
```jsx
const About = lazy(() => import('./About'));

<Suspense fallback={<div>Loading...</div>}>
  <About />
</Suspense>
```

**32. Routing and protected routes?** 🔁
**React Router maps URLs to components with `Routes` and `Route`, and navigation happens without reloading the page.** **A protected route checks authentication and redirects to `/login` if the user is not signed in.**
```jsx
function Protected({ children }) {
  const { isAuthenticated } = useAuth();
  return isAuthenticated ? children : <Navigate to="/login" />;
}
```
Route types: static (`/about`), dynamic (`/user/:id`), nested, protected, and wildcard (`*`).

**33. Forms and validation?**
**Handle forms with controlled inputs and state, or use Formik with Yup for validation schemas.** Formik manages form state, submission, and errors, so you write less boilerplate.

**34. Hydration?**
**Hydration is when React attaches event handlers and state to HTML that the server already rendered.** Until hydration finishes, the page looks ready but is not yet interactive.

**35. 🔁 CSR vs SSR?**
**Client-side rendering sends a mostly empty HTML page, and the browser builds the UI with JavaScript.** **Server-side rendering sends complete HTML from the server,** which gives a faster first paint and better SEO, then hydrates on the client.

**36. Higher-order components (HOC)?**
**A HOC is a function that takes a component and returns an enhanced one.** It is used for shared behavior such as authentication or logging. Hooks have mostly replaced HOCs for new code.

**37. Render props?**
**A render prop is a component that takes a function prop and calls it to decide what to render.** It shares logic such as mouse tracking between components without needing a HOC.

**38. Presentational vs container components?**
**Presentational components only display data through props.** **Container components handle data fetching and logic, and pass the results to presentational components.** Hooks now make this split optional, but the idea of separating concerns still helps.

**39. Composition pattern?**
**Composition builds complex UIs by combining components through `children` and props,** instead of extending base classes. React favors composition over inheritance.
```jsx
<Dialog><h1>Welcome</h1></Dialog>
```

**40. Custom hooks?**
**A custom hook is a function whose name starts with `use` and that calls other hooks.** It extracts reusable stateful logic, such as data fetching, so components stay small and the logic is easy to test.
```jsx
function useFetch(url) {
  const [data, setData] = useState(null);
  useEffect(() => { fetch(url).then(r => r.json()).then(setData); }, [url]);
  return data;
}
```

## 🟠 Moderate

**41. 🔥 `React.memo`, `useMemo`, and `useCallback`?** 🔁
**`React.memo` skips re-rendering a component when its props have not changed.** **`useMemo` caches an expensive computed value.** **`useCallback` caches a function reference, so memoized children do not see a new prop each time.** Measure first, because memoization has its own cost.
```jsx
const Child = React.memo(({ onClick }) => <button onClick={onClick}>Go</button>);

function Parent() {
  const handleClick = useCallback(() => console.log('clicked'), []);
  return <Child onClick={handleClick} />;
}
```

**42. Optimizing re-renders?**
**Use `React.memo`, `useMemo`, and `useCallback` where profiling shows a problem.** Avoid creating new objects and functions inline in props, split large components, lazy-load routes, virtualize long lists, and use stable keys.

**43. React anti-patterns?**
**Common anti-patterns are mutating state, creating components inside other components, using array indices as keys, heavy inline functions, and deeply nested state.** Each one causes bugs or slow re-renders.

**44. `forwardRef` and `useImperativeHandle`?**
**`forwardRef` passes a ref from a parent through a component to a DOM node.** **`useImperativeHandle` exposes a limited set of methods, such as `focus` or `clear`, to the parent** instead of the whole DOM node.

**45. Context vs Redux vs Zustand vs Recoil?**
**Context is built in and fine for small or medium global data.** **Redux is a predictable store with actions, reducers, and strong devtools, but more boilerplate.** **Zustand is a small store with a minimal API.** **Recoil uses atoms and selectors for fine-grained derived state.**

**46. `startTransition` and `useTransition`?**
**They mark a state update as non-urgent,** so React keeps the UI responsive while it renders a heavy update, such as filtering a large list. Urgent updates such as typing still happen immediately.

**47. Side effects with `useEffect`?**
**Side effects are anything outside rendering, such as fetching, subscriptions, timers, and DOM changes.** Put them in `useEffect`, and return a cleanup function when you start something that must be stopped.

**48. CSR, SSR, and SSG?**
**CSR renders in the browser, SSR renders on the server for each request, and SSG renders at build time.** Choose SSG for mostly static content, SSR for personalized data that needs SEO, and CSR for app-like dashboards.

## 🔴 Advanced

**49. 🔥 React Fiber?** 🔁
**Fiber is the reconciler rewrite introduced in React 16.** **It breaks rendering into small units of work that can pause, resume, or be dropped.** This enables time slicing, Suspense, and concurrent features that the old synchronous reconciler could not support.

**50. Concurrent rendering and React 18?**
**Concurrent rendering lets React prepare several versions of the UI and interrupt work when something more urgent happens.** **React 18 introduced `createRoot`, automatic batching, `startTransition`, `useId`, and `useSyncExternalStore`.**
```jsx
import { createRoot } from 'react-dom/client';
createRoot(document.getElementById('root')).render(<App />);
```

**51. React 17 vs 18 vs 19?**
**React 17 was an upgrade release with no new features.** **React 18 added concurrent rendering and the new root API.** **React 19 focused on Actions, new hooks, and server component improvements.**

**52. Automatic batching?**
**React 18 batches state updates from promises, timeouts, and native events into one render.** Before React 18, batching only happened inside React event handlers.

**53. `useLayoutEffect` (blocking)?**
**`useLayoutEffect` blocks the browser from painting until it finishes.** Use it only when you must measure or synchronize the DOM before the user sees the frame, because it can slow the page.

**54. Flux and one-way data flow?** 🔁
**One-way data flow means data moves from parent to child, and changes go back up through events.** **Flux formalizes this with actions, a dispatcher, stores, and views,** so state changes are predictable and easy to trace.

**55. Shallow compare in `React.memo`?**
**`React.memo` compares each prop with `===` against the previous render.** **Inline objects and functions create new references every render, so they defeat memoization,** which is why `useMemo` and `useCallback` exist.

**56. Server Components and Suspense?**
**Server Components render on the server and send only their output to the client,** so they add no JavaScript to the bundle. **Suspense shows a fallback while data or code is loading** and works with both server and client rendering.

**57. Pitfalls of data fetching?**
**Common mistakes are skipping loading and error states, not cleaning up, race conditions when inputs change quickly, and wrong dependency arrays.** Fix them with cleanup flags or `AbortController`.

**58. Context or Redux at scale?**
**Keep state as local as possible.** **Use Context for rarely changing global data and a dedicated store for frequent or complex updates,** so unrelated components do not re-render.

**59. Code splitting in React?**
**Code splitting divides the bundle into chunks loaded on demand,** using `React.lazy`, dynamic `import()`, and route-based splits. It reduces the initial download.

**60. Performance checklist?**
**Profile first, then memoize the hot spots, virtualize long lists with `react-window`, lazy-load routes, ship production builds, and optimize images.** Measure after each change to confirm it helped.

---

## ⚠️ Items not legible in the source PDF

| Topic | Question numbers |
|---|---|
| HTML | Q15 and Q30 |
| CSS | Q45, Q58, Q59, Q60 |
| JavaScript | Q75, Q82 (+ Q90 and Q105 partly cut) |
| React | Q122, Q127, Q135, Q231 (cut), Q239 (cut), Q255, Q270, Q285 |

---

## 🚫 Skipped (not in your 4 topics)
- **Browser rendering and performance** (PDF Q136–Q139, Q141, Q145–Q149)
- **HTTP, WebSocket, Service Workers, PWA** (PDF Q151–Q165)
- **Next.js and TypeScript** (PDF Q181–Q225, Q286–Q300)

*Duplicates inside those sections (block/inline, CSS units, media queries, responsive design) are merged into the HTML and CSS sections above.*
