# React Notes: Beginner to Advanced (Simple Language)

Easy notes for all 137 React topics. Every topic has:

- **Simple Definition**: what it is, in plain words
- **Code**: a small example (only where code makes sense)
- **Interview Notes**: how often it is asked, a short answer you can say, and the common confusion

**Interview frequency key:** 🔥 High = asked very often | ⭐ Medium = asked sometimes | 💤 Low = asked rarely

## Table of Contents

1. [Level 1: React Fundamentals](#level-1--react-fundamentals)
2. [Level 2: Props, Conditional Rendering and Lists](#level-2--props-conditional-rendering-and-lists)
3. [Level 3: State and Event Handling](#level-3--state-and-event-handling)
4. [Level 4: React Hooks](#level-4--react-hooks)
5. [Level 5: React Rendering and Internals](#level-5--react-rendering-and-internals)
6. [Level 6: Routing with React Router](#level-6--routing-with-react-router)

---

# Level 1 — React Fundamentals

### 1. What Is React?

**Simple Definition:** React is a tool (a JavaScript library) made by Facebook for building what users see on a screen. You build your page from small reusable pieces called components, and React keeps the screen updated when your data changes.

**Interview Notes:**
- 🔥 Frequency: High (first question in most interviews)
- Say: "React is a JavaScript library for building user interfaces using reusable components."
- Confusion: React is a **library**, not a **framework**. It only handles the screen part. Things like routing you add yourself.

---

### 2. Why React? Problems with Vanilla JavaScript

**Simple Definition:** "Vanilla JavaScript" means plain JavaScript with no extra tools. In big apps, plain JavaScript makes you update the page by hand (find the element, change its text, and so on). This gets messy and full of bugs. React fixes this: you just change your data, and React updates the page for you.

**Interview Notes:**
- 🔥 Frequency: High
- Say: "React saves us from manually touching the page. We describe what the screen should look like, and React does the updating."
- Confusion: React is not faster than plain JavaScript in every case. Its real benefit is that big apps stay organized and easy to maintain.

---

### 3. React Features and Use Cases

**Simple Definition:** Main features:
- **Components**: reusable building blocks
- **JSX**: write HTML-like code inside JavaScript
- **Virtual DOM**: a fast way to update the page
- **One-way data flow**: data moves from parent to child
- **Hooks**: add features like memory to simple functions

Used for dashboards, shopping sites, social media feeds, admin panels, and so on.

**Interview Notes:**
- 🔥 Frequency: High
- Say the 4 main ones: components, JSX, virtual DOM, one-way data flow.
- Confusion: Do not say React has "two-way binding". It does not.

---

### 4. Single-Page Applications (SPA)

**Simple Definition:** An SPA is a website that loads **one HTML page** only. When you click links, the page does not fully reload. JavaScript just swaps the content on the screen. This feels fast, like a mobile app.

**Interview Notes:**
- 🔥 Frequency: High
- Say: "An SPA loads one page once and updates parts of it without reloading."
- Confusion: Even though the URL changes, the browser is not asking the server for a new page. React Router handles that.
- Downside to mention: the first load can be slower, and search engines may find it harder to read.

---

### 5. React vs Vanilla JavaScript

**Simple Definition:** Both are JavaScript. In plain JavaScript you tell the browser *how* to change things step by step. In React you tell it *what* you want to see, and React works out the steps.

```jsx
// Vanilla JavaScript: change the page by hand
document.getElementById("count").innerText = count;

// React: just change the data, the screen updates itself
<p>{count}</p>
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "Vanilla JS is step-by-step (imperative). React is describe-the-result (declarative)."
- Confusion: React is not a different language. It is JavaScript.

---

### 6. Setting Up React with Vite

**Simple Definition:** Vite (say "veet") is a tool that creates a ready-made React project for you and runs it very fast on your computer.

```bash
npm create vite@latest my-app -- --template react
cd my-app
npm install
npm run dev
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "Vite is a fast build tool. It replaced Create React App, which is no longer recommended."
- Confusion: Vite is not React. Vite is the tool that runs and builds your React code.

---

### 7. React Project Structure

**Simple Definition:** The folders and files you get in a new project:

```
my-app/
├── node_modules/   -> downloaded packages (never edit)
├── public/         -> files used as they are (images, icons)
├── src/            -> YOUR code lives here
│   ├── main.jsx    -> starting point, connects React to the page
│   ├── App.jsx     -> main component
│   └── App.css     -> styles
├── index.html      -> the one HTML page
└── package.json    -> project details and package list
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "`index.html` has an empty `div` with id `root`. `main.jsx` puts our React app inside it."
- Confusion: People think there are many HTML pages. There is only one.

---

### 8. Understanding package.json

**Simple Definition:** A file that is like the project's ID card. It holds the project name, the list of packages it needs (dependencies), and shortcut commands (scripts).

```json
{
  "name": "my-app",
  "scripts": {
    "dev": "vite",
    "build": "vite build"
  },
  "dependencies": {
    "react": "^18.2.0"
  }
}
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "`dependencies` are packages the app needs to run. `devDependencies` are only needed while building."
- Confusion: `node_modules` is not saved on GitHub. Anyone can recreate it by running `npm install`, because `package.json` has the list.

---

### 9. Understanding npm run dev and Production Build

**Simple Definition:**
- `npm run dev`: starts a test server on your computer while you build. Changes show instantly.
- `npm run build`: makes a small, fast, final version of your app, ready to put on the internet.

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "Dev is for developing with helpful warnings. Build creates an optimized version for users."
- Confusion: Never upload the dev version to real users. It is slower and bigger.

---

### 10. JSX Fundamentals

**Simple Definition:** JSX lets you write HTML-looking code inside JavaScript. It is not real HTML. React turns it into normal JavaScript behind the scenes.

```jsx
const element = <h1>Hello World</h1>;
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "JSX is a syntax that looks like HTML but is converted into JavaScript function calls (`React.createElement`)."
- Confusion: Browsers cannot read JSX. A tool (Vite/Babel) converts it first. JSX is optional but everyone uses it.

---

### 11. JSX Rules and Syntax

**Simple Definition:** Rules to remember:
1. Return **one parent** element only.
2. Close every tag, even `<img />` and `<input />`.
3. Use `className` instead of `class`.
4. Write attributes in camelCase (`onClick`, `tabIndex`).

```jsx
// Wrong
return (
  <h1>Hi</h1>
  <p>Bye</p>
);

// Right
return (
  <div>
    <h1>Hi</h1>
    <p>Bye</p>
  </div>
);
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: "Why only one parent?" Because a function can return only one thing. Wrap in a `div` or a Fragment.

---

### 12. JavaScript Expressions Inside JSX

**Simple Definition:** Put `{ }` curly braces inside JSX to use JavaScript. You can show variables, do math, or call functions inside them.

```jsx
const name = "Ravi";
return <h1>Hello {name}, 2 + 2 = {2 + 2}</h1>;
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "Curly braces allow any JavaScript **expression** (something that gives a value)."
- Confusion: You cannot put `if` or `for` statements inside `{ }`. Use a ternary (`? :`) or `map()` instead. Also, objects cannot be shown directly.

---

### 13. JSX Attributes and className

**Simple Definition:** Attributes are written like HTML but with JavaScript names. `class` is already a word in JavaScript, so React uses `className`. Inline styles take an **object**.

```jsx
<div className="box" style={{ color: "red", fontSize: "20px" }}>
  Hello
</div>
<label htmlFor="name">Name</label>
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: Why `{{ }}` for style? The outer braces mean "JavaScript here", the inner braces are the style object. Style names are camelCase (`fontSize`, not `font-size`).

---

### 14. Fragments (<>...</>)

**Simple Definition:** A Fragment lets you group elements without adding an extra `div` to the page.

```jsx
return (
  <>
    <h1>Title</h1>
    <p>Text</p>
  </>
);
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "Fragments group elements without extra HTML nodes."
- Confusion: The short `<>` cannot take a `key`. For a key, write `<React.Fragment key={id}>`.

---

### 15. Functional Components

**Simple Definition:** A component is a normal JavaScript function that returns JSX. It is one reusable piece of the screen.

```jsx
function Welcome() {
  return <h1>Welcome!</h1>;
}
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "A functional component is a JavaScript function that returns JSX."
- Confusion: Older React used class components. Today, function components with Hooks are the standard.

---

### 16. Component Naming Rules

**Simple Definition:** A component name **must start with a capital letter**. Small letters are treated as normal HTML tags.

```jsx
function Button() { ... }   // correct
function button() { ... }   // wrong

<Button />   // React component
<button />   // normal HTML button
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Confusion: If you write `<button />` thinking it is your component, you will get the plain HTML button instead.

---

### 17. Importing and Exporting Components

**Simple Definition:** You put each component in its own file. `export` shares it; `import` brings it into another file.

```jsx
// Button.jsx
export default function Button() {
  return <button>Click</button>;
}

// App.jsx
import Button from "./Button";
```

Named export (many per file):

```jsx
export function A() {}
import { A } from "./file";
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "A file can have one default export and many named exports."
- Confusion: Default import: any name works, no braces. Named import: exact name, with braces.

---

### 18. Component Composition

**Simple Definition:** Building big components by putting small components inside them, like Lego blocks.

```jsx
function App() {
  return (
    <div>
      <Header />
      <Content />
      <Footer />
    </div>
  );
}
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "Composition means building complex UIs by combining simple components."
- Confusion: React prefers composition over inheritance.

---

### 19. Rendering Components

**Simple Definition:** "Rendering" means React showing your component on screen. You use a component like an HTML tag, and `main.jsx` starts the whole app.

```jsx
import { createRoot } from "react-dom/client";
import App from "./App";

createRoot(document.getElementById("root")).render(<App />);
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Confusion: Writing `App()` is wrong. Write `<App />`, so React can manage it.

---

### 20. Styling React Components with CSS

**Simple Definition:** Ways to style:
1. Normal CSS file with `className`
2. Inline style object
3. CSS Modules (styles only for that one component)

```jsx
import "./App.css";
<h1 className="title">Hello</h1>
```

```jsx
// CSS Module: Button.module.css
import styles from "./Button.module.css";
<button className={styles.btn}>Click</button>
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Confusion: A normal CSS file is **global**. Its styles can affect other components. CSS Modules avoid that clash.

---

# Level 2 — Props, Conditional Rendering and Lists

### 21. What Are Props?

**Simple Definition:** Props (short for properties) are values you send **into** a component, like giving inputs to a function. They let the same component show different things.

**Interview Notes:**
- 🔥 Frequency: High
- Say: "Props are read-only inputs passed from a parent to a child component."
- Confusion: A child **cannot change** its props.

---

### 22. Passing Props to Components

**Simple Definition:** Write them like HTML attributes. The child receives them as one object.

```jsx
function Greeting(props) {
  return <h1>Hello {props.name}</h1>;
}

<Greeting name="Ravi" />
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: Text goes in quotes (`name="Ravi"`). Numbers, variables and booleans go in braces (`age={25}`).

---

### 23. Props Destructuring

**Simple Definition:** A shortcut to pull values out of props so you don't write `props.` every time.

```jsx
function Greeting({ name, age }) {
  return <h1>{name} is {age}</h1>;
}
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "Destructuring takes values out of the props object directly in the function's brackets."

---

### 24. Default Prop Values

**Simple Definition:** A backup value used when the parent does not send that prop.

```jsx
function Button({ text = "Click Me" }) {
  return <button>{text}</button>;
}

<Button />            // shows "Click Me"
<Button text="Buy" /> // shows "Buy"
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Confusion: The default only works when the value is `undefined`. If someone passes `null`, the default is NOT used.

---

### 25. Passing Functions as Props

**Simple Definition:** You can send a function to a child. The child can run it later, for example on a button click.

```jsx
function Parent() {
  const sayHi = () => alert("Hi!");
  return <Child onGreet={sayHi} />;
}

function Child({ onGreet }) {
  return <button onClick={onGreet}>Say Hi</button>;
}
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: Write `onClick={sayHi}`, not `onClick={sayHi()}`. With `()` it runs immediately while rendering.

---

### 26. Passing JSX as Props

**Simple Definition:** A prop can hold a piece of JSX too, so the parent decides what appears in a certain spot.

```jsx
function Card({ title, icon }) {
  return <div>{icon} {title}</div>;
}

<Card title="Home" icon={<span>🏠</span>} />
```

**Interview Notes:**
- 💤 Frequency: Low
- Say: "Props can be any value: text, numbers, functions, or JSX."

---

### 27. The children Prop

**Simple Definition:** Whatever you write **between** a component's opening and closing tags is sent automatically as a prop called `children`.

```jsx
function Box({ children }) {
  return <div className="box">{children}</div>;
}

<Box>
  <h1>Hello</h1>
  <p>Anything can go here</p>
</Box>
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "`children` is a special prop that holds whatever is placed inside the component's tags. It makes wrapper components like cards and modals possible."

---

### 28. Props vs State

**Simple Definition:**
- **Props**: data coming **from outside** (from the parent). Read-only.
- **State**: data **owned by the component itself**. It can change.

| Props | State |
|---|---|
| Given by parent | Created inside the component |
| Cannot be changed by the child | Can be changed |
| Like function inputs | Like a function's own memory |

**Interview Notes:**
- 🔥 Frequency: High (very common)
- Confusion: When state changes, the component updates. A parent's state can become a child's props.

---

### 29. Conditional Rendering with if and Ternary Operators

**Simple Definition:** Showing different things depending on a condition.

```jsx
function Status({ isLoggedIn }) {
  if (isLoggedIn) {
    return <h1>Welcome back!</h1>;
  }
  return <h1>Please log in</h1>;
}

// Inside JSX use a ternary
<h1>{isLoggedIn ? "Welcome back!" : "Please log in"}</h1>
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: You cannot write `if` inside JSX braces. Use the ternary `condition ? A : B`.

---

### 30. Conditional Rendering with &&

**Simple Definition:** Show something only if a condition is true, and show nothing otherwise.

```jsx
{isLoggedIn && <button>Logout</button>}
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion (famous trap):

```jsx
{count && <p>Items</p>}   // if count is 0, it shows "0" on screen!
{count > 0 && <p>Items</p>}  // correct
```

`0` is a number React actually prints, so always make the condition a true/false value.

---

### 31. Rendering Lists with map()

**Simple Definition:** To show many items, loop over an array with `map()`. It turns each item into a piece of JSX.

```jsx
const fruits = ["Apple", "Mango", "Banana"];

<ul>
  {fruits.map((fruit) => (
    <li key={fruit}>{fruit}</li>
  ))}
</ul>
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: Use `map()`, not `forEach()`. `forEach` returns nothing, so nothing would show.

---

### 32. The key Prop

**Simple Definition:** A `key` is a special label you give each item in a list. It helps React know which item is which when the list changes.

```jsx
{users.map((user) => (
  <li key={user.id}>{user.name}</li>
))}
```

**Interview Notes:**
- 🔥 Frequency: High (one of the most asked)
- Say: "Keys help React identify which items were added, removed, or moved, so it updates only what changed."
- Confusion: `key` is not available inside the child as a prop. Put it on the element inside `map()`.

---

### 33. Why Keys Must Be Unique and Stable

**Simple Definition:**
- **Unique**: no two items in the same list share a key.
- **Stable**: an item's key should not change between renders. Do not use `Math.random()`.

**Interview Notes:**
- 🔥 Frequency: High
- Say: "If keys change every render, React thinks every item is new, deletes all of them, and rebuilds. That is slow and can lose what users typed."
- Best key: an id from your database.

---

### 34. Index as Key — Problems and Exceptions

**Simple Definition:** Using the array position as the key (`key={index}`) works, but is risky when the list can be reordered, added to, or deleted from.

```jsx
// Risky if list changes
{items.map((item, index) => <li key={index}>{item}</li>)}
```

**Why it is a problem:** If you delete the first item, every item shifts position, so their keys change. React may show wrong data or mix up input boxes.

**OK to use index when:** the list is fixed, never reordered, never filtered, and items have no ids.

**Interview Notes:**
- 🔥 Frequency: High
- Say: "Index as key is fine for static lists. For dynamic lists use a unique id."

---

### 35. Rendering Empty States

**Simple Definition:** What to show when a list has no items, like "No results found". Always handle this so the page doesn't look broken.

```jsx
{todos.length === 0 ? (
  <p>No todos yet!</p>
) : (
  <ul>{todos.map((t) => <li key={t.id}>{t.text}</li>)}</ul>
)}
```

**Interview Notes:**
- 💤 Frequency: Low (but shows good practice)
- Also handle "loading" and "error" states in real apps.

---

### 36. Component Reusability

**Simple Definition:** Writing a component once and using it in many places with different props.

```jsx
function Button({ label, color }) {
  return <button style={{ background: color }}>{label}</button>;
}

<Button label="Save" color="green" />
<Button label="Delete" color="red" />
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "Reusable components reduce repeated code and keep the design consistent."

---

### 37. Presentational vs Logic-Heavy Components

**Simple Definition:**
- **Presentational**: only shows things. Gets data through props. No data fetching.
- **Logic-heavy** (container): handles state, fetches data, makes decisions, then passes data down.

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "Splitting display from logic makes code easier to test and reuse."
- Today, custom hooks are often used to separate logic instead.

---

### 38. Parent-to-Child Communication

**Simple Definition:** The parent sends data down using props.

```jsx
function Parent() {
  return <Child message="Hello from parent" />;
}
function Child({ message }) {
  return <p>{message}</p>;
}
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "Data flows one way: down, from parent to child."

---

### 39. Child-to-Parent Communication

**Simple Definition:** A child cannot send data up directly. Instead, the parent gives the child a **function** as a prop. The child calls that function and passes the data.

```jsx
function Parent() {
  const [msg, setMsg] = useState("");
  return (
    <>
      <p>Child said: {msg}</p>
      <Child onSend={setMsg} />
    </>
  );
}

function Child({ onSend }) {
  return <button onClick={() => onSend("Hi parent!")}>Send</button>;
}
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: Data goes down as props. Information goes up through function calls.

---

### 40. Component Composition vs Prop Drilling

**Simple Definition:** **Prop drilling** is passing a prop through many layers of components just so a deep child can use it. The middle components don't need it but must carry it. It becomes messy.

**Fixes:**
- **Composition**: pass ready-made JSX using `children`, so the middle layers don't need the data.
- **Context**: share data to any depth without passing it step by step.

```jsx
// Composition fix: Page builds the deep part itself
<Layout>
  <Profile user={user} />
</Layout>
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "Prop drilling means passing props through components that do not use them. Solve it with composition or Context."
- Confusion: Not all prop passing is bad. 1-2 levels is fine.

---

# Level 3 — State and Event Handling

### 41. React Event Handling

**Simple Definition:** Events are things users do: click, type, submit. In React you attach a function to the element with camelCase names like `onClick` and `onChange`.

```jsx
function App() {
  function handleClick() {
    alert("Clicked!");
  }
  return <button onClick={handleClick}>Click</button>;
}
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: `onclick` (small letters) is HTML. React uses `onClick`, and you pass a function, not a string.

---

### 42. Event Handlers and Callback Functions

**Simple Definition:** An event handler is the function that runs when an event happens. A callback is a function you give to something else to call later. The handler is a callback.

```jsx
<button onClick={() => console.log("Hi")}>Click</button>
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Confusion: `onClick={handle()}` runs it right away. `onClick={handle}` runs it on click.

---

### 43. Passing Arguments to Event Handlers

**Simple Definition:** To give extra data to a handler, wrap it in an arrow function.

```jsx
function handleDelete(id) {
  console.log("Deleting", id);
}

<button onClick={() => handleDelete(5)}>Delete</button>
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: `onClick={handleDelete(5)}` is wrong, it runs immediately. Use the arrow function wrapper.

---

### 44. Synthetic Events

**Simple Definition:** React wraps the browser's normal event in its own event object, so events behave the same in all browsers. You use it the same way as a normal event.

```jsx
function handleChange(event) {
  console.log(event.target.value);
}
<input onChange={handleChange} />
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "A synthetic event is React's cross-browser wrapper around the native event."
- Common: `event.preventDefault()` stops the default behavior (like form refresh). `event.stopPropagation()` stops the event from reaching parents.

---

### 45. useState Hook

**Simple Definition:** `useState` gives a component a **memory**. It stores a value and gives you a function to change it. When the value changes, the screen updates.

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```

**Interview Notes:**
- 🔥 Frequency: High (guaranteed)
- Say: "`useState` returns an array: the current value and a function to update it."
- Confusion: A normal variable (`let count`) is forgotten on every render and does not update the screen. State does.

---

### 46. State Initialization

**Simple Definition:** The value you pass into `useState(...)` is the starting value. It is used only on the first render.

```jsx
const [name, setName] = useState("");
const [age, setAge] = useState(0);
const [items, setItems] = useState([]);
const [user, setUser] = useState(null);
```

For heavy starting work, pass a function so it runs only once:

```jsx
const [data, setData] = useState(() => loadFromStorage());
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Confusion: Changing the initial value later does nothing. Also `useState(loadFromStorage())` runs on every render; `useState(() => ...)` runs once.

---

### 47. Updating State

**Simple Definition:** Always use the setter function. Never change the state variable directly.

```jsx
setCount(5);       // correct
count = 5;         // wrong, screen will not update
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "We call the setter so React knows something changed and can re-render."

---

### 48. State Updates and Re-rendering

**Simple Definition:** When you call a setter with a **new value**, React runs your component function again (re-renders) to show the new screen.

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: If you set the same value as before, React skips the re-render.
- Re-render means the function runs again, not that the whole page reloads.

---

### 49. Updating State Based on Previous State

**Simple Definition:** When the new value depends on the old one, pass a **function** to the setter. React gives it the latest value.

```jsx
setCount((prev) => prev + 1);
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "Use the functional update form when the next state depends on the previous state."

```jsx
// Only adds 1, not 3
setCount(count + 1);
setCount(count + 1);
setCount(count + 1);

// Adds 3
setCount((p) => p + 1);
setCount((p) => p + 1);
setCount((p) => p + 1);
```

---

### 50. Why State Updates May Appear Asynchronous

**Simple Definition:** After calling `setCount`, the variable `count` does **not** change right away in that same function. The new value shows up on the next render.

```jsx
function handleClick() {
  setCount(count + 1);
  console.log(count); // still the OLD value
}
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "State updates are scheduled, not instant. The new value is available in the next render."
- Confusion: This is why people think `useState` is async. Technically it is "batched", not a Promise.

---

### 51. State Batching

**Simple Definition:** If you call several setters in one event, React groups them and re-renders **only once**, which is faster.

```jsx
function handleClick() {
  setName("Ravi");
  setAge(25);
  // only ONE re-render
}
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "React 18 batches updates everywhere, including inside timeouts and promises."

---

### 52. Immutable State Updates

**Simple Definition:** "Immutable" means do not change the existing object or array. Make a **new copy** with your change and give that to the setter.

```jsx
// Wrong: changing the old one
user.name = "Sam";
setUser(user);

// Right: a new copy
setUser({ ...user, name: "Sam" });
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "React compares old and new state by reference. If I change the same object, React sees no difference and may not re-render."

---

### 53. Updating Objects in State

**Simple Definition:** Copy the old object with the spread operator (`...`) and overwrite only what changed.

```jsx
const [user, setUser] = useState({ name: "Ravi", age: 25 });

setUser({ ...user, age: 26 });

// Nested object
setUser({ ...user, address: { ...user.address, city: "Pune" } });
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: Without `...user`, the other fields (like `name`) disappear. Also, spread makes a shallow copy, so nested objects need their own copy.

---

### 54. Updating Arrays in State

**Simple Definition:** Do not use `push`, `pop`, `splice`, or `sort` directly on state. Make a new array.

```jsx
// Add
setItems([...items, "new"]);
// Add at the start
setItems(["new", ...items]);
```

| Avoid (changes original) | Use (makes new array) |
|---|---|
| push, pop, shift | spread `[...arr]`, concat |
| splice | slice, filter |
| sort, reverse | copy first, then sort |

**Interview Notes:**
- 🔥 Frequency: High

---

### 55. Removing and Updating Array Items in State

**Simple Definition:** Use `filter` to remove and `map` to update.

```jsx
// Remove item with id 2
setTodos(todos.filter((t) => t.id !== 2));

// Update item with id 2
setTodos(
  todos.map((t) => (t.id === 2 ? { ...t, done: true } : t))
);
```

**Interview Notes:**
- 🔥 Frequency: High (often asked as a todo-app coding task)
- Confusion: Inside `map`, always return the other items unchanged.

---

### 56. Managing Multiple State Variables

**Simple Definition:** You can call `useState` many times. Use separate states for unrelated values, or one object when values always change together.

```jsx
const [name, setName] = useState("");
const [age, setAge] = useState(0);

// or together
const [form, setForm] = useState({ name: "", age: 0 });
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Confusion: Updating an object state replaces the whole object, so you must spread the old values.

---

### 57. Lifting State Up

**Simple Definition:** When two components need the same data, move the state to their **closest common parent**, and pass it down as props.

```jsx
function Parent() {
  const [text, setText] = useState("");
  return (
    <>
      <Input text={text} onChange={setText} />
      <Preview text={text} />
    </>
  );
}
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "If siblings need to share data, lift the state to their parent."

---

### 58. Sharing State Between Components

**Simple Definition:** Ways to share data:
- Lift state to a common parent (small apps)
- Context (many components, far apart)
- External tools like Redux (very large apps)

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "Start simple with lifting state, move to Context when passing props gets painful."
- Confusion: Two components using the same custom hook do **not** share state. Each gets its own copy.

---

### 59. Controlled Components

**Simple Definition:** An input whose value is controlled by React state. React is the "boss" of what the input shows.

```jsx
const [name, setName] = useState("");

<input value={name} onChange={(e) => setName(e.target.value)} />
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "In a controlled component, form data lives in React state. In an uncontrolled one, the browser keeps it and we read it using a ref."
- Confusion: If you give `value` but forget `onChange`, the input becomes stuck and you cannot type.

---

### 60. Handling Forms and Input Fields

**Simple Definition:** Connect each input to state, update on `onChange`, and handle submit.

```jsx
function Form() {
  const [name, setName] = useState("");

  function handleSubmit(e) {
    e.preventDefault(); // stop page reload
    console.log(name);
  }

  return (
    <form onSubmit={handleSubmit}>
      <input value={name} onChange={(e) => setName(e.target.value)} />
      <button type="submit">Send</button>
    </form>
  );
}
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: Forgetting `e.preventDefault()` makes the page reload on submit.

---

### 61. Checkbox, Radio and Select Inputs

**Simple Definition:** Checkbox uses `checked`. Radio uses `checked` compared to a value. Select uses `value`.

```jsx
// Checkbox
<input type="checkbox" checked={agree}
  onChange={(e) => setAgree(e.target.checked)} />

// Radio
<input type="radio" value="male" checked={gender === "male"}
  onChange={(e) => setGender(e.target.value)} />

// Select
<select value={city} onChange={(e) => setCity(e.target.value)}>
  <option value="pune">Pune</option>
  <option value="delhi">Delhi</option>
</select>
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Confusion: Checkbox uses `e.target.checked`, not `e.target.value`. In React, `<select>` takes `value`, not `selected` on the option.

---

### 62. Handling Multiple Inputs

**Simple Definition:** Use one state object and one handler. Give each input a `name`, and use that name as the key.

```jsx
const [form, setForm] = useState({ name: "", email: "" });

function handleChange(e) {
  setForm({ ...form, [e.target.name]: e.target.value });
}

<input name="name" value={form.name} onChange={handleChange} />
<input name="email" value={form.email} onChange={handleChange} />
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: `[e.target.name]` with square brackets is a "computed key": the key is taken from a variable.

---

### 63. Form Submission and Validation

**Simple Definition:** Validation means checking input before accepting it. Check on submit and show error messages.

```jsx
function handleSubmit(e) {
  e.preventDefault();
  if (!email.includes("@")) {
    setError("Enter a valid email");
    return;
  }
  setError("");
  // send data
}

{error && <p style={{ color: "red" }}>{error}</p>}
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "Validate on the client for good user experience, but always validate on the server too, for safety."

---

### 64. Derived State

**Simple Definition:** Values you can **calculate** from existing state or props. Do not store them in a separate state. Just calculate them while rendering.

```jsx
const [items, setItems] = useState([]);
const total = items.length;  // derived, no extra state needed
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "Don't store what you can calculate. Extra state can go out of sync."
- Confusion: Copying a prop into state (`useState(props.value)`) is a common mistake, because later prop changes won't update the state.

---

### 65. State Preservation and Resetting

**Simple Definition:** React keeps a component's state as long as it stays in the **same position** in the screen tree. State resets when the component is removed or its `key` changes.

```jsx
// Changing key forces a fresh start
<Profile key={userId} userId={userId} />
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "Changing the key tells React it is a different component, so it resets the state."
- Confusion: Two same components in the same spot keep the old state, which surprises people.

---

# Level 4 — React Hooks

### 66. What Are Hooks?

**Simple Definition:** Hooks are special functions that start with `use` (like `useState`, `useEffect`). They let a simple function component use features like memory and side jobs. Before Hooks, you needed class components for these.

**Interview Notes:**
- 🔥 Frequency: High
- Say: "Hooks let function components use state and other React features."
- Common built-in hooks: `useState`, `useEffect`, `useRef`, `useContext`, `useReducer`, `useMemo`, `useCallback`.

---

### 67. Rules of Hooks

**Simple Definition:** Two rules:
1. Call Hooks only at the **top level** of a component. Not inside `if`, loops, or nested functions.
2. Call Hooks only inside **function components or custom hooks**. Not in normal JavaScript functions.

```jsx
// Wrong
if (loggedIn) {
  const [name, setName] = useState("");
}

// Right
const [name, setName] = useState("");
```

**Interview Notes:**
- 🔥 Frequency: High
- Say both rules clearly. Interviewers love this one.

---

### 68. Why Hooks Must Be Called at the Top Level

**Simple Definition:** React remembers hooks **by their order** (first hook, second hook, third hook). If a hook is sometimes skipped because of an `if`, the order changes and React gets confused and gives wrong values.

**Interview Notes:**
- 🔥 Frequency: High
- Say: "React tracks hooks by call order, so the order must be the same on every render."
- Confusion: React does not track hooks by name. That is why order matters.

---

### 69. useState in Depth

**Simple Definition:** Points to remember about `useState`:
- It returns `[value, setter]`.
- Setting new state re-renders the component.
- Use the function form when depending on old state.
- Each component copy has its own state.
- State is remembered between renders.

```jsx
const [count, setCount] = useState(0);
setCount((c) => c + 1);
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: Two copies of `<Counter />` do not share state. Each one has its own count.

---

### 70. useEffect

**Simple Definition:** `useEffect` runs code **after** the screen is shown. Use it for side jobs: fetching data, timers, listening to events, or updating the page title.

```jsx
useEffect(() => {
  document.title = "Hello";
}, []);
```

**Interview Notes:**
- 🔥 Frequency: High (guaranteed)
- Say: "`useEffect` is for side effects, things that happen outside rendering, like API calls or timers."
- Confusion: It runs after the render, not during it.

---

### 71. Effect Setup and Cleanup

**Simple Definition:** The effect function is the **setup**. It can return another function, the **cleanup**, which runs before the next effect and when the component is removed. Use it to stop timers or remove listeners.

```jsx
useEffect(() => {
  const id = setInterval(() => console.log("tick"), 1000);

  return () => clearInterval(id); // cleanup
}, []);
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "Cleanup avoids memory leaks and duplicate timers or listeners."
- Confusion: Cleanup also runs **before each re-run** of the effect, not only when the component is removed.

---

### 72. Dependency Array in useEffect

**Simple Definition:** The second argument (a list) tells React **when** to run the effect again. React runs it only when a value in that list has changed.

```jsx
useEffect(() => {
  fetchUser(userId);
}, [userId]); // re-runs when userId changes
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "Put every value the effect uses (props, state) inside the dependency array."
- Confusion: Missing values cause old (stale) data bugs.

---

### 73. Empty Dependency Array vs No Dependency Array

**Simple Definition:**

| Code | When it runs |
|---|---|
| `useEffect(fn)` (no array) | After **every** render |
| `useEffect(fn, [])` (empty array) | **Once**, after the first render |
| `useEffect(fn, [a, b])` | First render, and when `a` or `b` change |

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: In development with Strict Mode, an empty-array effect runs twice on purpose to check for bugs. It will run once in production.

---

### 74. When useEffect Runs

**Simple Definition:** Order of events:
1. Component renders (function runs)
2. Screen is updated
3. Effect runs
4. On a re-render with changed dependencies: old cleanup runs, then the new effect runs
5. On removal: cleanup runs

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "Effects run after the browser paints the screen, so they don't block what the user sees."

---

### 75. Common useEffect Mistakes

**Simple Definition:** Mistakes beginners make:
1. Forgetting the dependency array (effect runs every render).
2. Missing dependencies (stale values).
3. Forgetting cleanup (timers pile up).
4. Using an effect for something that can be calculated while rendering.
5. Making the effect function itself `async`.

```jsx
// Wrong
useEffect(async () => { ... }, []);

// Right
useEffect(() => {
  async function load() {
    const res = await fetch(url);
    setData(await res.json());
  }
  load();
}, []);
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: An `async` function returns a Promise, but `useEffect` expects either nothing or a cleanup function.

---

### 76. Infinite Re-render and Effect Loops

**Simple Definition:** A loop where updating state causes a re-render, which causes the effect to run, which updates state again, forever.

```jsx
// Infinite loop!
useEffect(() => {
  setCount(count + 1);
}, [count]);

// Also an infinite loop: setting state during render
function App() {
  const [n, setN] = useState(0);
  setN(n + 1);
}
```

Another cause: an object or array in the dependency list that is created fresh on every render.

**Interview Notes:**
- 🔥 Frequency: High
- Say: "To fix, check the dependencies, use an empty array if it should run once, or avoid state updates that trigger themselves."

---

### 77. Effects vs Event Handlers

**Simple Definition:**
- **Event handler**: runs because the **user did something** (click, type).
- **Effect**: runs because the **component appeared or something changed on screen**.

If the code is a reaction to a click, put it in the click handler, not an effect.

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "If the work is caused by a user action, use an event handler. Use an effect only to keep something in sync with the screen."

---

### 78. useRef

**Simple Definition:** `useRef` gives you a box that holds a value. You can change the value inside the box (`ref.current`) and React will **not** re-render.

```jsx
const ref = useRef(0);
ref.current = ref.current + 1;
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "`useRef` returns an object with a `current` property that survives re-renders without causing them."

---

### 79. useRef vs useState

| useRef | useState |
|---|---|
| Changing it does **not** re-render | Changing it **does** re-render |
| Change `ref.current` directly | Use the setter function |
| For values not shown on screen | For values shown on screen |

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: If the screen should update when the value changes, use state, not ref.

---

### 80. Accessing DOM Elements with useRef

**Simple Definition:** Attach a ref to an element with the `ref` attribute, and you can reach the real HTML element.

```jsx
function Form() {
  const inputRef = useRef(null);

  return (
    <>
      <input ref={inputRef} />
      <button onClick={() => inputRef.current.focus()}>Focus</button>
    </>
  );
}
```

**Interview Notes:**
- 🔥 Frequency: High
- Uses: focusing inputs, scrolling, playing video, measuring size.
- Confusion: `inputRef.current` is `null` until the component has been shown.

---

### 81. Storing Mutable Values with useRef

**Simple Definition:** Use a ref to remember something between renders when it doesn't need to appear on screen, like a timer id or previous value.

```jsx
const timerId = useRef(null);

function start() {
  timerId.current = setInterval(() => console.log("hi"), 1000);
}
function stop() {
  clearInterval(timerId.current);
}
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "Refs are good for timer ids, previous values, and flags that should not cause re-renders."

---

### 82. useContext

**Simple Definition:** `useContext` lets any component read shared data directly, without passing props through every level.

```jsx
const theme = useContext(ThemeContext);
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "`useContext` reads the nearest Provider's value for that context."
- Confusion: When the context value changes, **all** components using it re-render.

---

### 83. Creating Context

**Simple Definition:** Step 1 is making the context with `createContext`.

```jsx
import { createContext } from "react";

export const ThemeContext = createContext("light"); // "light" is the default
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Confusion: The default value is used only when a component has **no Provider** above it.

---

### 84. Context Provider and Consumer

**Simple Definition:**
- **Provider**: wraps your components and supplies the value.
- **Consumer**: any component that reads the value (usually with `useContext`).

```jsx
function App() {
  const [theme, setTheme] = useState("dark");
  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      <Page />
    </ThemeContext.Provider>
  );
}

function Page() {
  const { theme } = useContext(ThemeContext);
  return <h1>Theme is {theme}</h1>;
}
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: Components outside the Provider cannot see the value.

---

### 85. Context API

**Simple Definition:** The full system: `createContext` makes it, `Provider` supplies it, `useContext` reads it. It is built into React and solves prop drilling.

**Interview Notes:**
- 🔥 Frequency: High
- Say: "Context shares data like theme, language, or logged-in user across the app without prop drilling."
- Confusion: Context is not a full replacement for Redux. It is not built for data that changes very often, because every consumer re-renders.

---

### 86. useReducer

**Simple Definition:** Like `useState`, but better when state has many parts or many ways to change. You send an **action** (a message like "add"), and a **reducer** function decides the new state.

```jsx
const [state, dispatch] = useReducer(reducer, { count: 0 });

dispatch({ type: "increment" });
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "`useReducer` gives state and a `dispatch` function to trigger changes."

---

### 87. Reducer Functions and Actions

**Simple Definition:** A reducer takes the **current state** and an **action**, and returns the **new state**. It must be a pure function: no API calls, no changing the old state.

```jsx
function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    case "reset":
      return { count: 0 };
    default:
      return state;
  }
}
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Confusion: Always **return** a new state. Never change `state` directly.

---

### 88. useReducer vs useState

| useState | useReducer |
|---|---|
| Simple values | Complex state with many updates |
| Easy and short | More code, but organized |
| Logic in components | Logic in one reducer function |

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "Use `useState` for simple state. Use `useReducer` when next state depends on actions or when many values change together."

---

### 89. Custom Hooks

**Simple Definition:** Your own hook: a function whose name starts with `use`, which uses other hooks inside it. It lets you reuse logic across components.

```jsx
function useCounter(start = 0) {
  const [count, setCount] = useState(start);
  const add = () => setCount((c) => c + 1);
  return { count, add };
}

function App() {
  const { count, add } = useCounter();
  return <button onClick={add}>{count}</button>;
}
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "A custom hook is a function starting with `use` that shares logic, not UI, between components."
- Confusion: Each component using it gets its **own separate state**.

---

### 90. Rules and Naming of Custom Hooks

**Simple Definition:**
- Name must start with `use` (like `useFetch`).
- Follow the Rules of Hooks inside it.
- It can call other hooks.
- It can return anything: values, arrays, objects, functions.

**Interview Notes:**
- ⭐ Frequency: Medium
- Confusion: The `use` name is not just style. Tools use it to check that you follow the Rules of Hooks.

---

### 91. Sharing Logic with Custom Hooks

**Simple Definition:** Move repeated logic (like fetching data) into a custom hook, so many components can use it.

```jsx
function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch(url)
      .then((res) => res.json())
      .then((json) => {
        setData(json);
        setLoading(false);
      });
  }, [url]);

  return { data, loading };
}

const { data, loading } = useFetch("/api/users");
```

**Interview Notes:**
- 🔥 Frequency: High (often a coding question: "write a useFetch")
- Confusion: This shares the **logic**, not the **data**.

---

### 92. useMemo

**Simple Definition:** `useMemo` remembers (caches) the result of a slow calculation. It recalculates only when its dependencies change.

```jsx
const total = useMemo(() => {
  return items.reduce((sum, i) => sum + i.price, 0);
}, [items]);
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "`useMemo` caches a calculated value between renders."
- Confusion: Don't use it everywhere. It has its own cost. Use it for really slow work or to keep an object's reference stable.

---

### 93. useCallback

**Simple Definition:** `useCallback` remembers a **function** so it is not re-created on every render.

```jsx
const handleClick = useCallback(() => {
  console.log("clicked");
}, []);
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "`useCallback` caches a function. It is useful when passing functions to memoized children."
- Confusion: `useCallback(fn, deps)` is the same as `useMemo(() => fn, deps)`.

---

### 94. React.memo

**Simple Definition:** `React.memo` wraps a component so it **skips re-rendering** if its props did not change.

```jsx
const Child = React.memo(function Child({ name }) {
  console.log("Child rendered");
  return <p>{name}</p>;
});
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: It compares props only by reference (shallow). If you pass a new function or object each time, the child still re-renders. That's where `useCallback` and `useMemo` help.

---

### 95. useMemo vs useCallback vs React.memo

| Tool | What it remembers | Used on |
|---|---|---|
| `useMemo` | A calculated **value** | Inside a component |
| `useCallback` | A **function** | Inside a component |
| `React.memo` | A whole **component's output** | Wraps a component |

**Interview Notes:**
- 🔥 Frequency: High (very common comparison)
- Say: "`React.memo` skips re-rendering a component. `useCallback` and `useMemo` keep function and value references steady so `React.memo` can work properly."

---

### 96. Hook Dependency Pitfalls

**Simple Definition:** Common problems with dependency arrays:
- Leaving out a value the code uses (stale data)
- Putting an object or array created in the component body in the list (it is new every render, so the effect runs every time)
- Ignoring the lint warning instead of fixing the cause

```jsx
// Bad: `options` is a new object every render
const options = { page: 1 };
useEffect(() => { load(options); }, [options]);

// Better: depend on the simple value
useEffect(() => { load({ page }); }, [page]);
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "Include everything the effect uses. Prefer simple values (numbers, strings) over objects in dependencies."

---

### 97. Stale Closures in Hooks

**Simple Definition:** A function "remembers" the values from the render it was created in. If it runs later (like in a timer), it may still use **old** values.

```jsx
// Always logs 0, never updates
useEffect(() => {
  const id = setInterval(() => {
    console.log(count); // stuck at the first value
  }, 1000);
  return () => clearInterval(id);
}, []);

// Fix 1: add count to dependencies
// Fix 2: use functional update
setCount((c) => c + 1);
```

**Interview Notes:**
- 🔥 Frequency: High (a favorite "tricky" question)
- Say: "A stale closure is when a function captured old state or props. Fix it with correct dependencies, functional updates, or a ref."

---

# Level 5 — React Rendering and Internals

### 98. How React Renders a Component

**Simple Definition:** "Rendering" means React calls your component function to find out what should be on screen. The function returns JSX, React compares it with the last result, and updates the real page where needed.

Steps:
1. Trigger (first load or state change)
2. React calls your component
3. React works out what changed
4. React updates only those parts of the real page

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: Rendering does not always mean the screen changes. React may render and find nothing changed.

---

### 99. Initial Render vs Re-render

**Simple Definition:**
- **Initial render**: the first time a component appears.
- **Re-render**: every time after that, when state or props change.

**Interview Notes:**
- ⭐ Frequency: Medium
- Confusion: On a re-render, `useState` keeps its old value. It does not reset to the starting value.

---

### 100. Render Phase vs Commit Phase

**Simple Definition:**
- **Render phase**: React calls your components and figures out what the screen should look like. Nothing changes on the page yet. Must be pure.
- **Commit phase**: React makes the real changes to the page. Then effects run.

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "Render phase is calculating. Commit phase is applying the changes to the real page."
- Confusion: `useEffect` runs after the commit, so it's safe to do side jobs there.

---

### 101. What Triggers a Re-render?

**Simple Definition:** A component re-renders when:
1. Its **state** changes
2. Its **parent** re-renders
3. A **context** it uses changes

Changing a plain variable or `useRef` does **not** trigger a re-render.

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: Changing props directly is not a trigger. Props change only because a parent re-rendered.

---

### 102. Parent and Child Re-rendering

**Simple Definition:** When a parent re-renders, **all its children re-render too**, even if their props are the same. Use `React.memo` to avoid that.

```jsx
function Parent() {
  const [n, setN] = useState(0);
  return (
    <>
      <button onClick={() => setN(n + 1)}>+</button>
      <Child /> {/* re-renders every click */}
    </>
  );
}
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: Children re-render because the parent re-rendered, not because their props changed.

---

### 103. Virtual DOM

**Simple Definition:** The DOM is the real page structure in the browser. Updating it is slow. The Virtual DOM is a **light copy** of it kept in memory by React. React updates the copy first, finds what changed, and updates only that part of the real DOM.

**Interview Notes:**
- 🔥 Frequency: High (guaranteed)
- Say: "The Virtual DOM is a lightweight JavaScript copy of the real DOM. React compares old and new copies and updates only the differences."
- Confusion: Virtual DOM is not magic fast. The benefit is doing fewer real page updates.

---

### 104. Reconciliation

**Simple Definition:** Reconciliation is the process of React comparing the **old** Virtual DOM with the **new** one to decide the smallest set of changes needed on the real page.

**Interview Notes:**
- 🔥 Frequency: High
- Say: "Reconciliation is how React finds the difference between two renders and updates only what changed."

---

### 105. Diffing Algorithm — Basic Concepts

**Simple Definition:** The "diffing" is how React compares two trees quickly using two simple rules:
1. If an element's **type** is different (`div` became `span`), remove the old one and build a new one.
2. For lists, use **keys** to match old and new items.

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "React assumes different types make different trees, and uses keys for lists. This keeps comparison fast."

---

### 106. Element Identity and Component Types

**Simple Definition:** React decides if something is "the same component" by its **type** and **position**. Same type in the same spot means keep it and update. Different type means throw away and rebuild (and lose its state).

```jsx
// Switching between these destroys the state
{isAdmin ? <AdminPanel /> : <UserPanel />}
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Confusion: Defining a component **inside** another component creates a new type each render, so it resets state every time. Always define components at the top level of the file.

---

### 107. How Keys Affect Reconciliation

**Simple Definition:** Keys tell React which list item is which. With stable keys, React moves items. With changing or index keys, React may update the wrong ones or rebuild everything.

**Interview Notes:**
- 🔥 Frequency: High
- Say: "Keys give list items identity. Good keys help React reorder cheaply and keep state with the right item."

---

### 108. Component Lifecycle Concepts

**Simple Definition:** A component's life has three stages:
1. **Mounting**: appears on screen for the first time
2. **Updating**: re-renders as state or props change
3. **Unmounting**: removed from screen

In function components, `useEffect` handles all three:

```jsx
useEffect(() => {
  // mounting: runs on first appearance
  return () => {
    // unmounting: runs on removal
  };
}, []);
```

**Interview Notes:**
- 🔥 Frequency: High
- Class equivalents: `componentDidMount`, `componentDidUpdate`, `componentWillUnmount`.

---

### 109. Function Components vs Class Components

| Function Component | Class Component |
|---|---|
| A simple function | Uses `class` and `extends React.Component` |
| Uses Hooks for state and effects | Uses `this.state` and lifecycle methods |
| Less code, easier to read | More code, `this` can confuse |
| The modern standard | Older style, still supported |

```jsx
class Hello extends React.Component {
  render() {
    return <h1>Hello</h1>;
  }
}
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "Function components with Hooks are recommended. Class components still work but are not used for new code."
- Note: Error Boundaries still need a class component.

---

### 110. Why State Must Not Be Mutated

**Simple Definition:** "Mutating" means changing the original object or array directly. React checks whether state changed by comparing the **old reference** with the **new reference**. If you change the same object, the reference is the same, so React thinks nothing changed and skips the update.

```jsx
// Wrong: same object, no re-render
user.name = "Sam";
setUser(user);

// Right: new object
setUser({ ...user, name: "Sam" });
```

**Interview Notes:**
- 🔥 Frequency: High
- Also: mutation breaks `React.memo` and makes bugs hard to find.

---

### 111. Strict Mode in Development

**Simple Definition:** `<StrictMode>` is a helper that checks your app for hidden problems. In development only, it runs components and effects **twice** on purpose to catch bugs. It does nothing in production.

```jsx
<StrictMode>
  <App />
</StrictMode>
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: "Why does my console.log print twice?" That is Strict Mode. It is not a bug, and it does not happen in the production build.

---

### 112. React Batching and Update Scheduling

**Simple Definition:** React collects several state updates and applies them together in one re-render. It also decides when to do the work, so the screen stays smooth.

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "React 18 batches all updates automatically, including those inside promises and timeouts."

---

### 113. State Snapshots

**Simple Definition:** Each render has its own **snapshot** of state, like a photo. Inside that render and its handlers, the state value does not change, even after you call the setter.

```jsx
function handleClick() {
  setCount(count + 1);
  setCount(count + 1);
  // count is still the same snapshot value (say 0), so result is 1, not 2
}
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "State is a snapshot per render. Setting state asks for a new render with a new snapshot."
- This explains stale values in timers, too.

---

### 114. Render Purity

**Simple Definition:** A component should be a **pure function**: same props and state in, same JSX out. During rendering, do not change outside variables, call APIs, or use random or time values directly.

```jsx
// Impure: changes something outside
let count = 0;
function Bad() {
  count++;
  return <p>{count}</p>;
}
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "Rendering must be free of side effects. Put side effects in event handlers or `useEffect`."

---

### 115. Avoiding Unnecessary Re-renders

**Simple Definition:** Ways to reduce wasted work:
- `React.memo` for components
- `useCallback` for functions passed down
- `useMemo` for heavy calculations
- Keep state close to where it is used
- Split big components into smaller ones
- Use `key` properly

**Interview Notes:**
- 🔥 Frequency: High
- Say: "Measure first with React DevTools Profiler. Don't optimize before there is a real problem."
- Confusion: Wrapping everything in `memo` is not good practice.

---

### 116. Error Boundaries

**Simple Definition:** An Error Boundary is a component that catches errors in the components below it, and shows a backup screen instead of crashing the whole app.

```jsx
class ErrorBoundary extends React.Component {
  state = { hasError: false };

  static getDerivedStateFromError() {
    return { hasError: true };
  }

  render() {
    if (this.state.hasError) return <h1>Something went wrong</h1>;
    return this.props.children;
  }
}

<ErrorBoundary>
  <MyComponent />
</ErrorBoundary>
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Confusion: It must be a **class component**. It does **not** catch errors in event handlers, async code, or in itself.

---

### 117. Portals

**Simple Definition:** A Portal lets a component show its content in a **different place in the page**, outside its parent. Common for modals and tooltips.

```jsx
import { createPortal } from "react-dom";

function Modal({ children }) {
  return createPortal(
    <div className="modal">{children}</div>,
    document.body
  );
}
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "Portals render children outside the parent's HTML, but events still bubble up through the React tree."

---

### 118. Suspense Fundamentals

**Simple Definition:** `Suspense` lets you show a **loading screen** while a part of your app is waiting to be ready (for example, a lazy-loaded component).

```jsx
<Suspense fallback={<p>Loading...</p>}>
  <HeavyComponent />
</Suspense>
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "`fallback` is what shows while waiting."

---

### 119. Lazy Loading Components with React.lazy()

**Simple Definition:** Load a component's code **only when needed**, not at the start. This makes the first page load faster.

```jsx
import { lazy, Suspense } from "react";

const Dashboard = lazy(() => import("./Dashboard"));

function App() {
  return (
    <Suspense fallback={<p>Loading...</p>}>
      <Dashboard />
    </Suspense>
  );
}
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: `React.lazy` must be used together with `Suspense`. It works with **default exports**.

---

# Level 6 — Routing with React Router

### 120. Client-Side Routing

**Simple Definition:** Routing means showing a different screen for a different URL. In client-side routing, the browser does **not** ask the server for a new page. JavaScript changes what is shown and updates the URL.

**Interview Notes:**
- 🔥 Frequency: High
- Say: "Client-side routing changes the screen without a full page reload, so navigation feels fast."
- Confusion: React itself has no routing. We add the `react-router-dom` library.

---

### 121. Installing and Configuring React Router

**Simple Definition:** Install it, then wrap your app in a router.

```bash
npm install react-router-dom
```

```jsx
import { BrowserRouter } from "react-router-dom";

createRoot(document.getElementById("root")).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Confusion: The router must wrap every component that uses routing features.

---

### 122. BrowserRouter

**Simple Definition:** `BrowserRouter` is the main wrapper that turns on routing. It uses the browser's normal URL (like `/about`).

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "`BrowserRouter` uses clean URLs. When hosting, the server must send `index.html` for all paths, or refreshing a page like `/about` gives a 404."
- `HashRouter` is the older style: URLs look like `/#/about`.

---

### 123. Routes and Route

**Simple Definition:** `Routes` holds all your pages. Each `Route` says "when the URL is this path, show this component".

```jsx
import { Routes, Route } from "react-router-dom";

<Routes>
  <Route path="/" element={<Home />} />
  <Route path="/about" element={<About />} />
</Routes>
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: `element` takes JSX (`<Home />`), not just the name (`Home`).

---

### 124. Link vs NavLink

**Simple Definition:**
- `Link`: a link that changes the page **without reload**.
- `NavLink`: same as `Link`, but it knows if it is the **current page**, so you can style the active link.

```jsx
<Link to="/about">About</Link>

<NavLink
  to="/about"
  className={({ isActive }) => (isActive ? "active" : "")}
>
  About
</NavLink>
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: A plain `<a href>` reloads the entire page and loses state. Use `Link` instead.

---

### 125. Navigation with useNavigate

**Simple Definition:** `useNavigate` gives a function to change the page using code, such as after a form submit or login.

```jsx
const navigate = useNavigate();

function handleLogin() {
  // after login works
  navigate("/dashboard");
}

navigate(-1); // go back one page
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "Use `Link` for clicks on links and `useNavigate` for navigation that happens after some logic."

---

### 126. Dynamic Route Parameters

**Simple Definition:** A route with a changing part, written with a colon. One route can show many pages, like `/user/1`, `/user/2`.

```jsx
<Route path="/user/:id" element={<UserPage />} />
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "`:id` is a placeholder. Its value comes from the URL."

---

### 127. Reading Parameters with useParams

**Simple Definition:** `useParams` gives you the changing part of the URL.

```jsx
import { useParams } from "react-router-dom";

function UserPage() {
  const { id } = useParams();
  return <h1>User {id}</h1>;
}
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: Params are always **strings**. Convert with `Number(id)` if you need a number.

---

### 128. Query Parameters and Search Parameters

**Simple Definition:** The part of the URL after `?`, like `/products?category=shoes&page=2`. Read and change it with `useSearchParams`.

```jsx
import { useSearchParams } from "react-router-dom";

const [searchParams, setSearchParams] = useSearchParams();

const category = searchParams.get("category"); // "shoes"
setSearchParams({ category: "bags", page: 1 });
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Confusion: Route params (`/user/5`) are part of the path and required. Query params (`?page=2`) are optional extras, good for filters and search.

---

### 129. Nested Routes

**Simple Definition:** Routes placed inside other routes. The inner page appears inside the outer page's layout.

```jsx
<Route path="/dashboard" element={<Dashboard />}>
  <Route path="profile" element={<Profile />} />
  <Route path="settings" element={<Settings />} />
</Route>
```

This gives `/dashboard/profile` and `/dashboard/settings`.

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: Child paths have no `/` at the start, so they join the parent path. The parent must have an `<Outlet />` to show the child.

---

### 130. Layout Routes and Outlet

**Simple Definition:** A layout route holds shared parts (navbar, footer). `<Outlet />` is the empty spot where the child page appears.

```jsx
function Layout() {
  return (
    <>
      <Navbar />
      <Outlet />
      <Footer />
    </>
  );
}

<Route element={<Layout />}>
  <Route path="/" element={<Home />} />
  <Route path="/about" element={<About />} />
</Route>
```

**Interview Notes:**
- 🔥 Frequency: High
- Say: "`Outlet` is where nested routes show up inside the parent."
- Note: A layout route with no `path` adds no extra URL part.

---

### 131. Index Routes

**Simple Definition:** The **default** child page shown when the URL matches only the parent.

```jsx
<Route path="/dashboard" element={<Dashboard />}>
  <Route index element={<Overview />} />
  <Route path="settings" element={<Settings />} />
</Route>
```

At `/dashboard`, `Overview` appears inside the Outlet.

**Interview Notes:**
- ⭐ Frequency: Medium
- Confusion: An index route has the `index` attribute and no `path`.

---

### 132. Protected Routes

**Simple Definition:** Pages that only logged-in users may open. If not logged in, send them to the login page.

```jsx
import { Navigate } from "react-router-dom";

function ProtectedRoute({ isLoggedIn, children }) {
  if (!isLoggedIn) {
    return <Navigate to="/login" replace />;
  }
  return children;
}

<Route
  path="/dashboard"
  element={
    <ProtectedRoute isLoggedIn={isLoggedIn}>
      <Dashboard />
    </ProtectedRoute>
  }
/>
```

**Interview Notes:**
- 🔥 Frequency: High (often a coding task)
- Say: "A protected route is a wrapper that checks login status and redirects if needed."
- Confusion: This only hides the page on the front end. The server must also check permission, because users can still call your APIs directly.

---

### 133. Authentication-Based Navigation

**Simple Definition:** Moving users around depending on whether they are logged in:
- Not logged in and opens a private page: go to login
- Logs in successfully: go to the dashboard (or the page they wanted)
- Logs out: go back to login or home

```jsx
function handleLogin() {
  setIsLoggedIn(true);
  navigate("/dashboard");
}
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Tip: Keep login status in Context so every page can read it. Use `replace` so the Back button doesn't return to the login page.

---

### 134. Not Found Routes

**Simple Definition:** A "catch-all" route that shows a 404 page when no other route matches. Use path `*`.

```jsx
<Routes>
  <Route path="/" element={<Home />} />
  <Route path="*" element={<NotFound />} />
</Routes>
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Confusion: `*` matches anything, but React Router picks the most specific match first, so put it anywhere in the list safely.

---

### 135. Programmatic Navigation

**Simple Definition:** Changing the page from code instead of a link click. Uses `useNavigate`, or `<Navigate />` for redirects while rendering.

```jsx
navigate("/home");                    // go to a page
navigate("/login", { replace: true });// replace current history entry
navigate(-1);                         // back
navigate("/profile", { state: { from: "home" } }); // send extra data
```

**Interview Notes:**
- 🔥 Frequency: High
- Confusion: `replace: true` does not add a new history entry, so Back skips the current page.
- Do not call `navigate()` directly while rendering. Call it in an event handler or `useEffect`.

---

### 136. Route-Based Code Splitting

**Simple Definition:** Load each page's code only when the user visits that page. Combine `React.lazy`, `Suspense` and routes. This makes the first load faster.

```jsx
const Home = lazy(() => import("./pages/Home"));
const About = lazy(() => import("./pages/About"));

<Suspense fallback={<p>Loading...</p>}>
  <Routes>
    <Route path="/" element={<Home />} />
    <Route path="/about" element={<About />} />
  </Routes>
</Suspense>
```

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "Splitting by route is the easiest and most effective place to split code, because users see one page at a time."

---

### 137. URL State vs Component State

**Simple Definition:**
- **URL state**: info stored in the URL (page number, filter, search text, selected item id).
- **Component state**: info stored with `useState` that disappears on refresh.

| URL state | Component state |
|---|---|
| Survives refresh | Lost on refresh |
| Can be shared as a link | Cannot be shared |
| Back button works | Back button does not affect it |
| For filters, pages, search | For small things like open/close a menu |

**Interview Notes:**
- ⭐ Frequency: Medium
- Say: "If a user should be able to bookmark or share the screen as it is, put that info in the URL."

---

## Final Tip

Learn in this order: **Components → Props → State → useEffect → Context → Router**. Practice by building a Todo app, a Counter, a Fetch-and-show-users page, and a small multi-page site with login. Most interview questions come from these.
