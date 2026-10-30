# React Notes for Beginners (Topics 138 to 300)

Simple notes. No heavy words. Each topic has:

- **Simple Meaning**: what it is, in easy words (you can say this in an interview)
- **Code**: a small example (only where code makes sense)
- **Interview Angle**: how often it is asked, and the mistakes people make

> **How to read the "Asked in interviews?" tag**
> - **Very often**: you will almost surely get this question
> - **Often**: asked in many interviews
> - **Sometimes**: asked in some interviews, mostly for deeper rounds
> - **Rarely**: good to know, but not commonly asked

---

## Contents

- Level 7: API Integration and Data Fetching (138 to 158)
- Level 8: State Management (159 to 178)
- Level 9: Forms and Validation (179 to 189)
- Level 10: Authentication and Security (190 to 201)
- Level 11: Performance Optimization (202 to 219)
- Level 12: Advanced React Concepts (220 to 235)
- Level 13: Testing and Accessibility (236 to 249)
- Level 14: Production and Deployment (250 to 260)
- Level 15: React Interview Questions and Practical Problems (261 to 283)
- Level 16: Practical React Projects (284 to 300)

---

# Level 7: API Integration and Data Fetching

## 138. Understanding APIs in React

**Simple Meaning**
An API is a messenger. Your React app asks a server for data (like a list of products), and the server sends the data back. React does not store this data itself. It asks for it using an API.

Think of a restaurant: you (React) tell the waiter (API) what you want, the waiter goes to the kitchen (server), and brings food (data) back.

**Code**
```jsx
// URL of an API that gives a list of users
const url = "https://jsonplaceholder.typicode.com/users";
```

**Interview Angle**
- Asked in interviews? **Often** (as a starting question)
- Short answer: "An API lets my React app talk to a server to get or send data."
- Confusion: React is **not** an API. React only shows the screen. The API lives on a server.

---

## 139. HTTP Request and Response Basics

**Simple Meaning**
- **Request**: your app asking the server for something.
- **Response**: the server's answer.

A request has: a **URL** (where to ask), a **method** (what you want to do, like GET), and sometimes **data** (body) and **headers** (extra info).
A response has: a **status code** (a number telling what happened) and **data**.

Common status codes:
| Code | Meaning |
|---|---|
| 200 | Success |
| 201 | Created something new |
| 400 | You sent a wrong request |
| 401 | You are not logged in |
| 403 | You are logged in but not allowed |
| 404 | Not found |
| 500 | The server broke |

**Code**
```js
const response = await fetch("https://jsonplaceholder.typicode.com/posts/1");
console.log(response.status); // 200
const data = await response.json(); // the actual data
```

**Interview Angle**
- Asked in interviews? **Very often**
- Be ready to explain 200, 401, 403, 404, 500.
- Confusion: 401 means "who are you?" (not logged in). 403 means "I know who you are, but you can't enter."

---

## 140. Fetch API in React

**Simple Meaning**
`fetch` is a built-in browser tool to send requests. You do not need to install anything. It gives back a **Promise** (a "I will give you the answer later" promise).

**Code**
```jsx
import { useEffect, useState } from "react";

function Users() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((res) => res.json())
      .then((data) => setUsers(data));
  }, []);

  return (
    <ul>
      {users.map((u) => (
        <li key={u.id}>{u.name}</li>
      ))}
    </ul>
  );
}
```

**Interview Angle**
- Asked in interviews? **Very often**
- Big confusion: `fetch` does **not** throw an error for 404 or 500. It only fails when the network itself fails. You must check `response.ok` yourself.
- You must call `.json()` to read the data. It is also a promise.

---

## 141. Axios Basics

**Simple Meaning**
Axios is a small library (you install it) that does the same job as `fetch`, but with less typing and some extra comfort. It turns the data to JSON for you and throws an error for bad status codes like 404 and 500.

**Code**
```bash
npm install axios
```
```jsx
import axios from "axios";

const res = await axios.get("https://jsonplaceholder.typicode.com/users");
console.log(res.data); // data is already ready to use
```

**Interview Angle**
- Asked in interviews? **Often**
- Confusion: in Axios the data is inside `res.data`, not `res`.

---

## 142. Fetch API vs Axios

**Simple Meaning**
Both get data from a server. The difference is comfort.

| | fetch | axios |
|---|---|---|
| Install needed? | No | Yes |
| Convert to JSON | You do `res.json()` | Automatic |
| Error on 404/500 | No, you check `res.ok` | Yes, automatically |
| Send JSON body | You do `JSON.stringify` | Automatic |
| Cancel request | AbortController | AbortController |
| Timeout | Manual | Built in option |

**Code**
```js
// fetch
const res = await fetch(url);
if (!res.ok) throw new Error("Request failed");
const data = await res.json();

// axios
const { data } = await axios.get(url);
```

**Interview Angle**
- Asked in interviews? **Very often**
- Good answer: "fetch is built in and needs no install. Axios needs install but saves time with automatic JSON and error handling."
- Do not say "Axios is always better". Small apps can use fetch just fine.

---

## 143. GET, POST, PUT, PATCH and DELETE Requests

**Simple Meaning**
These are the five main "actions" you can ask a server to do.

| Method | What it does | Example |
|---|---|---|
| GET | Read data | Get all todos |
| POST | Create new data | Add a new todo |
| PUT | Replace the whole item | Replace a full todo |
| PATCH | Change only a part | Only change the todo title |
| DELETE | Remove data | Delete a todo |

**Code**
```js
// GET
fetch("/api/todos");

// POST
fetch("/api/todos", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ title: "Learn React" }),
});

// PUT (replace everything)
fetch("/api/todos/1", {
  method: "PUT",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ title: "New title", done: true }),
});

// PATCH (change only one thing)
fetch("/api/todos/1", {
  method: "PATCH",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ done: true }),
});

// DELETE
fetch("/api/todos/1", { method: "DELETE" });
```

**Interview Angle**
- Asked in interviews? **Very often**
- Top confusion: **PUT vs PATCH**. PUT replaces the full item. PATCH changes only what you send.

---

## 144. Loading, Success, Error and Empty States

**Simple Meaning**
When you get data from a server, the screen can be in 4 situations:
1. **Loading**: still waiting. Show "Loading...".
2. **Success**: data arrived. Show it.
3. **Error**: something went wrong. Show a message.
4. **Empty**: it worked, but there is no data. Show "No items found".

If you do not handle these, users see a blank screen and think the app is broken.

**Code**
```jsx
function Users() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((res) => {
        if (!res.ok) throw new Error("Failed to load");
        return res.json();
      })
      .then((data) => setUsers(data))
      .catch((err) => setError(err.message))
      .finally(() => setLoading(false));
  }, []);

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error}</p>;
  if (users.length === 0) return <p>No users found</p>;

  return <ul>{users.map((u) => <li key={u.id}>{u.name}</li>)}</ul>;
}
```

**Interview Angle**
- Asked in interviews? **Very often** (almost every coding round)
- Confusion: people forget the **empty** state. Empty is not an error.

---

## 145. Handling API Errors

**Simple Meaning**
Things can go wrong: no internet, wrong URL, server crash, or not logged in. Handling errors means catching the problem and showing a friendly message instead of crashing the app.

**Code**
```jsx
async function loadData() {
  try {
    const res = await fetch("/api/data");
    if (!res.ok) {
      throw new Error("Server said: " + res.status);
    }
    const data = await res.json();
    setData(data);
  } catch (err) {
    setError("Something went wrong. Please try again.");
  }
}
```

**Interview Angle**
- Asked in interviews? **Very often**
- Confusion: with `fetch`, `catch` runs only for network failure. A 404 will not go to `catch` unless you throw it yourself using `res.ok`.
- Good practice: show a simple message to the user, and keep the technical detail in the console.

---

## 146. Async/Await in React

**Simple Meaning**
`async/await` is a cleaner way to write code that waits. `await` means "wait here until the answer comes". It makes the code look like normal step-by-step code.

**Code**
```jsx
useEffect(() => {
  // useEffect itself cannot be async, so make a function inside
  async function getUsers() {
    const res = await fetch("https://jsonplaceholder.typicode.com/users");
    const data = await res.json();
    setUsers(data);
  }
  getUsers();
}, []);
```

**Interview Angle**
- Asked in interviews? **Very often**
- Top confusion: **you cannot write `useEffect(async () => {})`**. useEffect must return nothing or a cleanup function. An async function returns a Promise, which breaks that rule. Make an inner async function and call it.

---

## 147. Data Fetching with useEffect

**Simple Meaning**
`useEffect` runs code after the screen is shown. It is the usual place to fetch data when a component first appears. The `[]` at the end means "run only once".

**Code**
```jsx
useEffect(() => {
  fetch("/api/products")
    .then((res) => res.json())
    .then((data) => setProducts(data));
}, []); // run once when the component appears

// Run again when "id" changes
useEffect(() => {
  fetch(`/api/products/${id}`)
    .then((res) => res.json())
    .then(setProduct);
}, [id]);
```

**Interview Angle**
- Asked in interviews? **Very often**
- Confusion: if you forget the `[]`, the effect runs after every render. If it also sets state, it makes an endless loop of requests.
- In development, React's Strict Mode runs effects twice on purpose. That is normal and not a bug.

---

## 148. Avoiding Unnecessary API Calls

**Simple Meaning**
Every API call costs time and server power. Do not call the server when you do not need to.

Ways to avoid extra calls:
- Use a correct dependency array (`[]` or `[id]`).
- Wait until the user stops typing before searching (debounce).
- Do not call again if you already have the data (cache it).
- Do not call when the input is empty.

**Code**
```jsx
useEffect(() => {
  if (!query) return; // do nothing if the search box is empty

  const timer = setTimeout(() => {
    fetch(`/api/search?q=${query}`)
      .then((res) => res.json())
      .then(setResults);
  }, 500); // wait half a second after typing stops

  return () => clearTimeout(timer); // cancel the old timer
}, [query]);
```

**Interview Angle**
- Asked in interviews? **Often**
- Interviewers love to ask: "How do you stop an API call on every key press?" Answer: **debounce**.

---

## 149. Request Cancellation with AbortController

**Simple Meaning**
Sometimes you start a request, but then the user leaves the page or changes the search. The old request is now useless. `AbortController` lets you cancel it.

**Code**
```jsx
useEffect(() => {
  const controller = new AbortController();

  fetch(`/api/search?q=${query}`, { signal: controller.signal })
    .then((res) => res.json())
    .then(setResults)
    .catch((err) => {
      if (err.name === "AbortError") return; // we cancelled on purpose
      setError("Failed");
    });

  return () => controller.abort(); // cancel when leaving or when query changes
}, [query]);
```

**Interview Angle**
- Asked in interviews? **Often**
- Confusion: a cancelled request throws an `AbortError`. This is not a real error, so ignore it.
- Good answer: "I cancel old requests in the cleanup function of useEffect."

---

## 150. Race Conditions in Data Fetching

**Simple Meaning**
A race condition means two requests are "racing", and the wrong one wins.

Example: you type "a" (request 1), then "ab" (request 2). Request 2 is the one you want. But request 1 is slow and arrives last. The screen then shows the result of "a", which is wrong.

**Fix:** ignore old responses, or cancel them.

**Code**
```jsx
useEffect(() => {
  let ignore = false;

  fetch(`/api/search?q=${query}`)
    .then((res) => res.json())
    .then((data) => {
      if (!ignore) setResults(data); // only use the latest
    });

  return () => {
    ignore = true; // this request is now old
  };
}, [query]);
```

**Interview Angle**
- Asked in interviews? **Often** (senior and mid level)
- Say: "Cleanup runs before the next effect, so I mark the old request as ignored, or I abort it."

---

## 151. Search and Filtering with API Data

**Simple Meaning**
- **Search**: find items by typing a word.
- **Filter**: show only items that match a rule (like category = "shoes").

You can do it in two ways:
1. **On the screen (client side)**: get all data once, then filter in React. Good for small lists.
2. **On the server**: send the search word to the API and the server returns only matching data. Good for big lists.

**Code**
```jsx
const [search, setSearch] = useState("");
const [category, setCategory] = useState("all");

const visibleProducts = products
  .filter((p) => p.title.toLowerCase().includes(search.toLowerCase()))
  .filter((p) => category === "all" || p.category === category);

return (
  <>
    <input value={search} onChange={(e) => setSearch(e.target.value)} />
    {visibleProducts.map((p) => <p key={p.id}>{p.title}</p>)}
  </>
);
```

**Interview Angle**
- Asked in interviews? **Very often** (popular coding task)
- Tip: do not store the filtered list in a separate state. Calculate it from the original list. Two copies of the same data go out of sync.

---

## 152. Sorting API Data

**Simple Meaning**
Sorting means arranging items in an order, like price low to high.

**Code**
```jsx
const [sortBy, setSortBy] = useState("low");

// make a copy first using [...products]
const sorted = [...products].sort((a, b) =>
  sortBy === "low" ? a.price - b.price : b.price - a.price
);
```

**Interview Angle**
- Asked in interviews? **Often**
- Top mistake: `products.sort()` changes the original array. In React you must never change state directly. Always copy first with `[...products]`.

---

## 153. Pagination

**Simple Meaning**
Pagination means showing data in small pages (like 10 items per page) with Next and Previous buttons, instead of loading thousands of items at once.

**Code**
```jsx
const [page, setPage] = useState(1);
const perPage = 10;

const start = (page - 1) * perPage;
const currentItems = items.slice(start, start + perPage);
const totalPages = Math.ceil(items.length / perPage);

return (
  <>
    {currentItems.map((i) => <p key={i.id}>{i.name}</p>)}
    <button disabled={page === 1} onClick={() => setPage(page - 1)}>Prev</button>
    <span>{page} / {totalPages}</span>
    <button disabled={page === totalPages} onClick={() => setPage(page + 1)}>Next</button>
  </>
);
```

With a server, you send the page number: `fetch(`/api/items?page=${page}&limit=10`)`.

**Interview Angle**
- Asked in interviews? **Very often** (as a coding task)
- Formula to remember: `start = (page - 1) * perPage`.

---

## 154. Infinite Scrolling Basics

**Simple Meaning**
Infinite scrolling loads more items automatically when the user reaches the bottom of the list (like Instagram). No page buttons.

**Code**
```jsx
import { useEffect, useRef, useState } from "react";

function Feed() {
  const [items, setItems] = useState([]);
  const [page, setPage] = useState(1);
  const bottomRef = useRef(null);

  // load data whenever page changes
  useEffect(() => {
    fetch(`/api/items?page=${page}`)
      .then((res) => res.json())
      .then((data) => setItems((old) => [...old, ...data]));
  }, [page]);

  // watch the bottom element
  useEffect(() => {
    const observer = new IntersectionObserver(([entry]) => {
      if (entry.isIntersecting) setPage((p) => p + 1);
    });
    if (bottomRef.current) observer.observe(bottomRef.current);
    return () => observer.disconnect();
  }, []);

  return (
    <>
      {items.map((i) => <p key={i.id}>{i.name}</p>)}
      <div ref={bottomRef}>Loading more...</div>
    </>
  );
}
```

**Interview Angle**
- Asked in interviews? **Sometimes**
- Say the key idea: "Put a small invisible element at the bottom. When it becomes visible, load the next page."
- Add new data to old data (`[...old, ...data]`), do not replace it.

---

## 155. Environment Variables in Vite

**Simple Meaning**
Environment variables are settings stored outside your code, like the API address. You keep them in a `.env` file. This lets you use different values for development and production without changing code.

In Vite, the name **must start with `VITE_`**, otherwise you cannot use it in React.

**Code**
```bash
# .env file
VITE_API_URL=https://api.example.com
```
```jsx
const url = import.meta.env.VITE_API_URL;
fetch(`${url}/products`);
```

**Interview Angle**
- Asked in interviews? **Often**
- Confusion 1: Vite uses `import.meta.env`, not `process.env` (that is for Create React App).
- Confusion 2: anything in a React env variable is **visible to everyone** in the browser. Never put secret passwords there.
- Restart the dev server after changing `.env`.

---

## 156. CORS Fundamentals

**Simple Meaning**
CORS is a safety rule in the browser. By default, a website is not allowed to take data from a different website (different address). The server must say "yes, this website is allowed". If it does not, the browser blocks the response and you see a CORS error in the console.

**Key point:** The fix is on the **server**, not in React.

**Code**
```js
// Server side example (Node + Express)
import cors from "cors";
app.use(cors({ origin: "http://localhost:5173" }));
```

**Interview Angle**
- Asked in interviews? **Very often**
- Common confusion: "I will fix CORS in React." You can't. The server must allow it.
- During development, you can use a Vite **proxy** to avoid the error.
- Good answer: "CORS is the browser protecting users. The server decides who is allowed."

---

## 157. Separating API Services from Components

**Simple Meaning**
Do not write `fetch` code inside every component. Put all API code in separate files (a "service" file). Components just call a simple function. This keeps code clean and easy to change.

**Code**
```js
// services/userService.js
const BASE_URL = import.meta.env.VITE_API_URL;

export async function getUsers() {
  const res = await fetch(`${BASE_URL}/users`);
  if (!res.ok) throw new Error("Failed to load users");
  return res.json();
}
```
```jsx
// components/Users.jsx
import { getUsers } from "../services/userService";

useEffect(() => {
  getUsers().then(setUsers).catch((e) => setError(e.message));
}, []);
```

**Interview Angle**
- Asked in interviews? **Often** (project structure questions)
- Benefit: if the API address changes, you fix one file, not 20 components.

---

## 158. Handling Authentication Tokens in Requests

**Simple Meaning**
A token is like a ticket you get after login. For private API calls, you must show this ticket in every request. It is usually sent in the **Authorization header**.

**Code**
```js
const token = localStorage.getItem("token");

fetch("/api/profile", {
  headers: {
    Authorization: `Bearer ${token}`,
  },
});
```

With Axios, you can attach it once for all requests:
```js
import axios from "axios";

const api = axios.create({ baseURL: import.meta.env.VITE_API_URL });

api.interceptors.request.use((config) => {
  const token = localStorage.getItem("token");
  if (token) config.headers.Authorization = `Bearer ${token}`;
  return config;
});

export default api;
```

**Interview Angle**
- Asked in interviews? **Often**
- Remember the word **Bearer**. It comes before the token.
- Interceptors are a favourite follow-up question.

---

# Level 8: State Management

## 159. Local State vs Shared State

**Simple Meaning**
- **Local state**: data used by only one component. Example: is a dropdown open?
- **Shared state**: data needed by many components. Example: the logged-in user, the shopping cart.

Start with local state. Move to shared state only when many components really need the same data.

**Code**
```jsx
// Local: only this component cares
function Dropdown() {
  const [open, setOpen] = useState(false);
  return <button onClick={() => setOpen(!open)}>Menu</button>;
}
```

**Interview Angle**
- Asked in interviews? **Very often**
- Good answer: "I keep state as close as possible to where it is used. I share it only when needed."

---

## 160. Problems with Prop Drilling

**Simple Meaning**
Prop drilling means passing data through many components just to reach one deep component. The middle components do not need the data, but they must carry it.

```
App (has user) -> Layout -> Sidebar -> Profile (needs user)
```
Layout and Sidebar are just carrying it.

**Code**
```jsx
function App() {
  const user = "Ravi";
  return <Layout user={user} />;
}
function Layout({ user }) {
  return <Sidebar user={user} />;   // only passing
}
function Sidebar({ user }) {
  return <Profile user={user} />;   // only passing
}
function Profile({ user }) {
  return <p>{user}</p>;
}
```

**Problems:** messy code, hard to change, easy to make mistakes.
**Fix:** Context API, or a state library.

**Interview Angle**
- Asked in interviews? **Very often**
- Note: a few levels of props is fine. It is only a problem when it gets very deep.

---

## 161. Managing Shared State with Context API

**Simple Meaning**
Context is like a shared board in a room. Any component inside the room can read from it directly, without passing props down step by step.

Three steps: **create** the context, **provide** the value, **use** it.

**Code**
```jsx
import { createContext, useContext, useState } from "react";

// 1. Create
const UserContext = createContext();

// 2. Provide
function UserProvider({ children }) {
  const [user, setUser] = useState("Ravi");
  return (
    <UserContext.Provider value={{ user, setUser }}>
      {children}
    </UserContext.Provider>
  );
}

// 3. Use (in any child, at any depth)
function Profile() {
  const { user } = useContext(UserContext);
  return <p>Hello {user}</p>;
}

// Wrap the app
<UserProvider>
  <Profile />
</UserProvider>
```

**Interview Angle**
- Asked in interviews? **Very often**
- Confusion: Context is not a full state manager. It only shares data. You still use `useState` or `useReducer` to hold the data.
- A component can only use context if it is inside the Provider.

---

## 162. Context API Performance Considerations

**Simple Meaning**
When the value in a Context changes, **every component that uses that context re-renders**, even if it only needs a small part of the value. In big apps, this can make things slow.

Ways to reduce the problem:
- Split into small contexts (one for user, one for theme).
- Keep values that change often out of context.
- Use `useMemo` for the value you pass.

**Code**
```jsx
function UserProvider({ children }) {
  const [user, setUser] = useState(null);

  // without useMemo, a new object is made on every render
  const value = useMemo(() => ({ user, setUser }), [user]);

  return <UserContext.Provider value={value}>{children}</UserContext.Provider>;
}
```

**Interview Angle**
- Asked in interviews? **Often**
- Famous trap: `value={{ user, setUser }}` creates a **new object every render**, so all users of the context re-render. Wrap it in `useMemo`.

---

## 163. Introduction to Redux

**Simple Meaning**
Redux keeps all the shared data of your app in **one place** called the store. Any component can read from it or ask to change it. The changes follow strict rules, so it is easy to track what changed and why.

Use Redux when the app is big and many parts share lots of data.

**Code**
```bash
npm install @reduxjs/toolkit react-redux
```

**Interview Angle**
- Asked in interviews? **Very often**
- Good answer: "Redux is a single place to keep app data, with clear rules to update it."
- Confusion: Redux is not part of React. It is a separate library.
- Do not say "Redux is a must". Many apps do not need it.

---

## 164. Redux Store, Actions and Reducers

**Simple Meaning**
- **Store**: the box that holds all the data.
- **Action**: a message that says what happened. Example: "add one to the counter".
- **Reducer**: a function that takes the old data and the action, and returns the new data.

Think of a bank: the **store** is the vault, an **action** is a deposit slip, and the **reducer** is the clerk who updates the balance.

**Code**
```js
// Action
const incrementAction = { type: "counter/increment" };

// Reducer: (old state, action) => new state
function counterReducer(state = { value: 0 }, action) {
  if (action.type === "counter/increment") {
    return { value: state.value + 1 };
  }
  return state;
}
```

**Interview Angle**
- Asked in interviews? **Very often**
- Rule: a reducer must be **pure**. It only uses its inputs, never calls an API, and never changes the old state. It returns a new copy.

---

## 165. Redux Data Flow

**Simple Meaning**
Redux data moves in one direction (a circle):

1. User clicks a button.
2. The component **dispatches** an action.
3. The **reducer** makes new state.
4. The **store** saves it.
5. Components that use that data **update** on screen.

```
UI -> dispatch(action) -> reducer -> store -> UI
```

**Code**
```jsx
dispatch({ type: "counter/increment" });
```

**Interview Angle**
- Asked in interviews? **Very often**
- Phrase to use: "one-way data flow".
- Confusion: components never change the store directly. They only send actions.

---

## 166. Redux Toolkit

**Simple Meaning**
Redux Toolkit (RTK) is the modern, easier way to write Redux. Old Redux needed a lot of boring code. RTK cuts that code down and has good defaults. It is the way recommended by the Redux team.

**Code**
```bash
npm install @reduxjs/toolkit react-redux
```
It gives you: `configureStore`, `createSlice`, `createAsyncThunk`, and RTK Query.

**Interview Angle**
- Asked in interviews? **Very often**
- Say: "I use Redux Toolkit, not old plain Redux."
- Benefit: it lets you write code that looks like it changes state directly, but it is safe inside (it uses a tool called Immer).

---

## 167. configureStore()

**Simple Meaning**
`configureStore` creates the store. You tell it which slices (pieces of data) your app has.

**Code**
```js
// store.js
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "./counterSlice";

export const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
});
```
```jsx
// main.jsx: give the store to the app
import { Provider } from "react-redux";
import { store } from "./store";

<Provider store={store}>
  <App />
</Provider>
```

**Interview Angle**
- Asked in interviews? **Often**
- Remember: the `<Provider>` wrapper is what lets components reach the store.

---

## 168. createSlice()

**Simple Meaning**
A slice is one piece of your data plus the functions that change it. `createSlice` makes the reducer and the actions for you in one go.

**Code**
```js
// counterSlice.js
import { createSlice } from "@reduxjs/toolkit";

const counterSlice = createSlice({
  name: "counter",
  initialState: { value: 0 },
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
    decrement: (state) => {
      state.value -= 1;
    },
    addAmount: (state, action) => {
      state.value += action.payload;
    },
  },
});

export const { increment, decrement, addAmount } = counterSlice.actions;
export default counterSlice.reducer;
```

**Interview Angle**
- Asked in interviews? **Very often**
- The value you pass in an action is called `action.payload`.
- Two exports: the **actions** (named) and the **reducer** (default).

---

## 169. useSelector() and useDispatch()

**Simple Meaning**
- `useSelector`: **read** data from the store.
- `useDispatch`: **send** an action to change the data.

**Code**
```jsx
import { useSelector, useDispatch } from "react-redux";
import { increment, addAmount } from "./counterSlice";

function Counter() {
  const value = useSelector((state) => state.counter.value);
  const dispatch = useDispatch();

  return (
    <>
      <p>{value}</p>
      <button onClick={() => dispatch(increment())}>+1</button>
      <button onClick={() => dispatch(addAmount(5))}>+5</button>
    </>
  );
}
```

**Interview Angle**
- Asked in interviews? **Very often**
- Tip: select only what you need (`state.counter.value`), not the whole state. This avoids extra re-renders.
- Confusion: write `dispatch(increment())` with brackets, not `dispatch(increment)`.

---

## 170. Updating State with Redux Toolkit

**Simple Meaning**
Normally in React you must never change state directly. But inside `createSlice`, you **are allowed** to write code that looks like direct change. Behind the scenes, RTK makes a safe copy for you.

**Code**
```js
reducers: {
  addTodo: (state, action) => {
    state.todos.push(action.payload);          // allowed inside createSlice
  },
  removeTodo: (state, action) => {
    state.todos = state.todos.filter((t) => t.id !== action.payload);
  },
  toggleTodo: (state, action) => {
    const todo = state.todos.find((t) => t.id === action.payload);
    if (todo) todo.done = !todo.done;
  },
}
```

**Interview Angle**
- Asked in interviews? **Very often**
- Classic question: "Can we change state directly in Redux?" Answer: "Not in plain Redux. But in Redux Toolkit's createSlice we can write it that way, because Immer makes a safe copy."
- Do not do this **outside** a slice.

---

## 171. Async Logic with createAsyncThunk

**Simple Meaning**
Reducers cannot call APIs. So for API calls, Redux Toolkit gives `createAsyncThunk`. It runs your async function and automatically gives you three states: **pending** (waiting), **fulfilled** (success), **rejected** (failed).

**Code**
```js
import { createAsyncThunk, createSlice } from "@reduxjs/toolkit";

export const fetchUsers = createAsyncThunk("users/fetch", async () => {
  const res = await fetch("https://jsonplaceholder.typicode.com/users");
  return res.json();
});

const usersSlice = createSlice({
  name: "users",
  initialState: { list: [], loading: false, error: null },
  reducers: {},
  extraReducers: (builder) => {
    builder
      .addCase(fetchUsers.pending, (state) => {
        state.loading = true;
      })
      .addCase(fetchUsers.fulfilled, (state, action) => {
        state.loading = false;
        state.list = action.payload;
      })
      .addCase(fetchUsers.rejected, (state, action) => {
        state.loading = false;
        state.error = action.error.message;
      });
  },
});

export default usersSlice.reducer;
```
```jsx
// in a component
useEffect(() => {
  dispatch(fetchUsers());
}, [dispatch]);
```

**Interview Angle**
- Asked in interviews? **Very often**
- Remember the three states: pending, fulfilled, rejected.
- Confusion: they are written in `extraReducers`, not `reducers`.

---

## 172. RTK Query Fundamentals

**Simple Meaning**
RTK Query is a tool inside Redux Toolkit made only for **getting data from APIs**. It handles loading, errors, and **caching** (remembering data so it does not ask again) for you. You write much less code than with `createAsyncThunk`.

**Code**
```js
// api.js
import { createApi, fetchBaseQuery } from "@reduxjs/toolkit/query/react";

export const api = createApi({
  reducerPath: "api",
  baseQuery: fetchBaseQuery({ baseUrl: "https://jsonplaceholder.typicode.com" }),
  endpoints: (builder) => ({
    getUsers: builder.query({ query: () => "/users" }),
  }),
});

export const { useGetUsersQuery } = api;
```
```jsx
function Users() {
  const { data, isLoading, error } = useGetUsersQuery();
  if (isLoading) return <p>Loading...</p>;
  if (error) return <p>Error</p>;
  return data.map((u) => <p key={u.id}>{u.name}</p>);
}
```
(You also add `api.reducer` and `api.middleware` to the store.)

**Interview Angle**
- Asked in interviews? **Sometimes**
- Good answer: "RTK Query handles fetching and caching so I don't write loading and error code by hand."

---

## 173. Context API vs Redux Toolkit

**Simple Meaning**
| | Context API | Redux Toolkit |
|---|---|---|
| Install | Built into React | Extra library |
| Best for | Small shared data (theme, user) | Big apps, lots of changing data |
| Setup | Easy | More setup |
| Debug tools | Few | Great (Redux DevTools) |
| Re-renders | All users of the context | Only components using the changed data |

**Interview Angle**
- Asked in interviews? **Very often**
- Good answer: "Context for simple and rarely changing data. Redux Toolkit for large apps with complex, frequently changing data."
- Mistake: saying "Context replaces Redux". It does not fully replace it.

---

## 174. Zustand Basics

**Simple Meaning**
Zustand is a small and simple state library. You create a store with one function, and use it like a hook. No Provider, no actions, no reducers. Much less code than Redux.

**Code**
```bash
npm install zustand
```
```jsx
import { create } from "zustand";

const useCounterStore = create((set) => ({
  count: 0,
  increment: () => set((state) => ({ count: state.count + 1 })),
  reset: () => set({ count: 0 }),
}));

function Counter() {
  const count = useCounterStore((state) => state.count);
  const increment = useCounterStore((state) => state.increment);
  return <button onClick={increment}>Count: {count}</button>;
}
```

**Interview Angle**
- Asked in interviews? **Sometimes** (growing in popularity)
- Say: "Zustand is a light alternative to Redux with very little code."

---

## 175. Server State vs Client State

**Simple Meaning**
- **Client state**: data that lives only in your app. Example: is the menu open, dark mode on.
- **Server state**: data that lives on a server and you only borrow a copy. Example: the product list, user profile.

Server state is different because it can become **old** (someone else may change it), it needs loading and error handling, and it should be cached.

**Interview Angle**
- Asked in interviews? **Often**
- Good answer: "I use useState or Zustand for client state, and React Query or RTK Query for server state."
- This difference is the main reason tools like React Query exist.

---

## 176. TanStack Query (React Query)

**Simple Meaning**
TanStack Query (also called React Query) is a library that makes fetching data easy. It gives you loading, error, caching, and re-fetching without writing `useEffect` and many `useState` calls.

**Code**
```bash
npm install @tanstack/react-query
```
```jsx
import { QueryClient, QueryClientProvider, useQuery } from "@tanstack/react-query";

const queryClient = new QueryClient();

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      <Users />
    </QueryClientProvider>
  );
}

function Users() {
  const { data, isLoading, error } = useQuery({
    queryKey: ["users"],
    queryFn: () => fetch("https://jsonplaceholder.typicode.com/users").then((r) => r.json()),
  });

  if (isLoading) return <p>Loading...</p>;
  if (error) return <p>Error</p>;
  return data.map((u) => <p key={u.id}>{u.name}</p>);
}
```
For sending data (POST, PUT, DELETE), use `useMutation`.

**Interview Angle**
- Asked in interviews? **Often**
- Remember: `useQuery` is for **reading**, `useMutation` is for **changing**.
- `queryKey` is the name of the data. It is like a label on a box in storage.

---

## 177. Caching, Refetching and Cache Invalidation

**Simple Meaning**
- **Caching**: remembering data you already got, so you don't ask the server again.
- **Refetching**: asking the server again to get fresh data (for example when the user returns to the tab).
- **Cache invalidation**: telling the library "this saved data is old now, get it again". Usually done after you change something (like adding a todo).

**Code**
```jsx
import { useMutation, useQueryClient } from "@tanstack/react-query";

const queryClient = useQueryClient();

const addTodo = useMutation({
  mutationFn: (newTodo) =>
    fetch("/api/todos", { method: "POST", body: JSON.stringify(newTodo) }),
  onSuccess: () => {
    // mark the "todos" data as old, so it loads again
    queryClient.invalidateQueries({ queryKey: ["todos"] });
  },
});
```

**Interview Angle**
- Asked in interviews? **Often**
- Famous quote: "There are only two hard things in programming: cache invalidation and naming things."
- Know the word **staleTime**: how long data is considered fresh before React Query refetches.

---

## 178. Choosing the Right State Management Solution

**Simple Meaning**
Do not pick the biggest tool first. Pick the smallest tool that solves the problem.

| Situation | Use |
|---|---|
| Data for one component | `useState` |
| Complex state in one component | `useReducer` |
| A little shared data (theme, user) | Context API |
| Lots of shared client data, big team | Redux Toolkit |
| Simple shared data, less code | Zustand |
| Data from APIs | React Query or RTK Query |

**Interview Angle**
- Asked in interviews? **Very often** (senior roles)
- Best answer shows thinking: "It depends on app size and the type of data." Then give the table above.
- Mistake: "I use Redux for everything."

---

# Level 9: Forms and Validation

## 179. Controlled vs Uncontrolled Forms

**Simple Meaning**
- **Controlled**: React holds the input value in state. Every key press updates the state, and the input shows what the state says. React is "in control".
- **Uncontrolled**: the browser holds the value. You read it only when you need it (using a `ref`).

**Code**
```jsx
// Controlled
function ControlledForm() {
  const [name, setName] = useState("");
  return <input value={name} onChange={(e) => setName(e.target.value)} />;
}

// Uncontrolled
function UncontrolledForm() {
  const inputRef = useRef();
  const handleSubmit = () => alert(inputRef.current.value);
  return (
    <>
      <input ref={inputRef} defaultValue="" />
      <button onClick={handleSubmit}>Submit</button>
    </>
  );
}
```

**Interview Angle**
- Asked in interviews? **Very often**
- Quick rule: controlled uses `value` + `onChange`. Uncontrolled uses `ref` + `defaultValue`.
- Mistake: setting `value` without `onChange` makes the input read-only.

---

## 180. Managing Complex Form State

**Simple Meaning**
When a form has many fields, do not make one `useState` for each. Keep all fields in **one object**, and use one handler for all inputs.

**Code**
```jsx
const [form, setForm] = useState({ name: "", email: "", age: "" });

function handleChange(e) {
  const { name, value } = e.target;
  setForm({ ...form, [name]: value }); // [name] picks the right field
}

return (
  <>
    <input name="name" value={form.name} onChange={handleChange} />
    <input name="email" value={form.email} onChange={handleChange} />
    <input name="age" value={form.age} onChange={handleChange} />
  </>
);
```

**Interview Angle**
- Asked in interviews? **Very often**
- Key trick: `[name]: value` (square brackets). It uses the input's `name` as the key.
- Mistake: forgetting `...form`, which erases the other fields.

---

## 181. Client-Side Form Validation

**Simple Meaning**
Validation means checking if what the user typed is correct (email looks like an email, password is long enough). "Client-side" means the check happens in the browser, before sending to the server. It gives fast feedback.

**Code**
```jsx
function validate(form) {
  const errors = {};
  if (!form.name.trim()) errors.name = "Name is required";
  if (!/\S+@\S+\.\S+/.test(form.email)) errors.email = "Enter a valid email";
  if (form.password.length < 6) errors.password = "At least 6 characters";
  return errors;
}
```

**Interview Angle**
- Asked in interviews? **Very often**
- Important: client-side validation is for **user comfort**, not security. Users can bypass it. The server must **check again**.

---

## 182. Displaying Validation Errors

**Simple Meaning**
Show a clear message next to the field that has the problem. Keep errors in a state, and show them only when they exist.

**Code**
```jsx
const [errors, setErrors] = useState({});

return (
  <>
    <input name="email" value={form.email} onChange={handleChange} />
    {errors.email && <p style={{ color: "red" }}>{errors.email}</p>}
  </>
);
```

**Interview Angle**
- Asked in interviews? **Often**
- Good practice: show the error after the user leaves the field or submits. Do not show errors while they have just started typing.

---

## 183. Handling Form Submission

**Simple Meaning**
When the user clicks submit, the browser normally reloads the page. In React we stop that using `e.preventDefault()`, then check the data and send it.

**Code**
```jsx
async function handleSubmit(e) {
  e.preventDefault(); // stop page reload

  const newErrors = validate(form);
  setErrors(newErrors);
  if (Object.keys(newErrors).length > 0) return; // stop if errors

  await fetch("/api/signup", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(form),
  });
}

<form onSubmit={handleSubmit}>...</form>
```

**Interview Angle**
- Asked in interviews? **Very often**
- Confusion: use `onSubmit` on the `<form>`, not `onClick` on the button. That way pressing Enter also works.
- Do not forget `preventDefault()`.

---

## 184. React Hook Form

**Simple Meaning**
React Hook Form is a library that makes forms easy. It handles values, errors, and submission for you, with less code and fewer re-renders (it is fast).

**Code**
```bash
npm install react-hook-form
```
```jsx
import { useForm } from "react-hook-form";

function SignupForm() {
  const { register, handleSubmit, formState: { errors } } = useForm();

  const onSubmit = (data) => console.log(data);

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("email", { required: "Email is required" })} />
      {errors.email && <p>{errors.email.message}</p>}

      <input
        type="password"
        {...register("password", { required: true, minLength: 6 })}
      />
      {errors.password && <p>Password must be 6+ characters</p>}

      <button type="submit">Sign up</button>
    </form>
  );
}
```

**Interview Angle**
- Asked in interviews? **Often**
- Key words: `register`, `handleSubmit`, `errors`.
- Benefit: it uses uncontrolled inputs inside, so typing does not re-render the whole form.

---

## 185. Schema Validation with Zod

**Simple Meaning**
A schema is a **rule list** for your data. Zod lets you write these rules in one place, in a clear way. Instead of many `if` checks, you describe what valid data looks like.

**Code**
```bash
npm install zod
```
```js
import { z } from "zod";

const signupSchema = z.object({
  name: z.string().min(1, "Name is required"),
  email: z.string().email("Enter a valid email"),
  age: z.number().min(18, "Must be 18 or older"),
  password: z.string().min(6, "At least 6 characters"),
});

const result = signupSchema.safeParse({ name: "Ravi", email: "bad", age: 20, password: "123456" });
console.log(result.success); // false
```

**Interview Angle**
- Asked in interviews? **Sometimes**
- Benefit: one schema can be used on both frontend and backend.

---

## 186. Integrating React Hook Form with Zod

**Simple Meaning**
Connect them so React Hook Form uses your Zod rules to check the form. You get automatic errors with your custom messages.

**Code**
```bash
npm install @hookform/resolvers
```
```jsx
import { useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { z } from "zod";

const schema = z.object({
  email: z.string().email("Enter a valid email"),
  password: z.string().min(6, "At least 6 characters"),
});

function LoginForm() {
  const { register, handleSubmit, formState: { errors } } = useForm({
    resolver: zodResolver(schema),
  });

  return (
    <form onSubmit={handleSubmit((data) => console.log(data))}>
      <input {...register("email")} />
      <p>{errors.email?.message}</p>

      <input type="password" {...register("password")} />
      <p>{errors.password?.message}</p>

      <button>Login</button>
    </form>
  );
}
```

**Interview Angle**
- Asked in interviews? **Sometimes**
- Key word: **resolver**. It is the bridge between the form library and Zod.

---

## 187. File Uploads

**Simple Meaning**
To let a user upload a file (like a photo), use `<input type="file" />`. Read the file from `e.target.files`. To send it to a server, use `FormData`.

**Code**
```jsx
function Upload() {
  const [file, setFile] = useState(null);

  function handleSubmit(e) {
    e.preventDefault();
    const formData = new FormData();
    formData.append("photo", file);

    fetch("/api/upload", { method: "POST", body: formData });
    // do NOT set Content-Type yourself, the browser does it
  }

  return (
    <form onSubmit={handleSubmit}>
      <input type="file" accept="image/*" onChange={(e) => setFile(e.target.files[0])} />
      {file && <img src={URL.createObjectURL(file)} width="100" alt="preview" />}
      <button>Upload</button>
    </form>
  );
}
```

**Interview Angle**
- Asked in interviews? **Often**
- Confusion: file inputs are always **uncontrolled**. You cannot set their value in React.
- Do not set the `Content-Type` header manually when using `FormData`.
- Also check file size and type.

---

## 188. Form Reset and Default Values

**Simple Meaning**
- **Default values**: what the form shows at the start (for example, when editing an existing user).
- **Reset**: bringing the form back to its starting values (or empty) after submitting.

**Code**
```jsx
// Plain React
const initialForm = { name: "", email: "" };
const [form, setForm] = useState(initialForm);

function handleSubmit(e) {
  e.preventDefault();
  // ...send data
  setForm(initialForm); // reset
}

// React Hook Form
const { register, handleSubmit, reset } = useForm({
  defaultValues: { name: "Ravi", email: "ravi@mail.com" },
});

const onSubmit = (data) => {
  console.log(data);
  reset(); // back to default values
};
```

**Interview Angle**
- Asked in interviews? **Sometimes**
- Tip: keep the starting values in one variable so you can reuse it for reset.

---

## 189. Accessible Forms and Error Messages

**Simple Meaning**
Accessible means everyone can use the form, including people who use screen readers or only a keyboard.

Simple rules:
- Every input needs a **label**.
- Connect label and input with `htmlFor` and `id`.
- Tell screen readers about errors using `aria-invalid` and `aria-describedby`.
- Use `role="alert"` so errors are read out loud.

**Code**
```jsx
<label htmlFor="email">Email</label>
<input
  id="email"
  type="email"
  aria-invalid={errors.email ? "true" : "false"}
  aria-describedby="email-error"
/>
{errors.email && (
  <p id="email-error" role="alert">
    {errors.email}
  </p>
)}
```

**Interview Angle**
- Asked in interviews? **Sometimes** (but valued)
- Remember: in React it is `htmlFor`, not `for`.
- Mistake: using only a placeholder as the label. Placeholders disappear when typing.
- Do not show errors using only red color. Add text too.

---

# Level 10: Authentication and Security

## 190. Authentication vs Authorization

**Simple Meaning**
- **Authentication**: "Who are you?" Proving your identity (login).
- **Authorization**: "What are you allowed to do?" Checking your permissions.

Example: at an office, showing your ID card at the gate is authentication. Which rooms your card can open is authorization.

**Interview Angle**
- Asked in interviews? **Very often**
- Easy memory trick: Authentication = identity. Authorization = access.
- Mistake: mixing up the two words. Always say authentication happens first.

---

## 191. Login and Signup Flows

**Simple Meaning**
- **Signup**: user creates a new account.
- **Login**: user enters email and password, the server checks them, and sends back a token.

Login flow:
1. User fills the form and submits.
2. React sends email and password to the server.
3. Server checks them and returns a token and user info.
4. React saves the token and shows the logged-in screen.

**Code**
```jsx
async function handleLogin(e) {
  e.preventDefault();
  const res = await fetch("/api/login", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ email, password }),
  });

  if (!res.ok) {
    setError("Wrong email or password");
    return;
  }

  const data = await res.json();
  localStorage.setItem("token", data.token);
  setUser(data.user);
  navigate("/dashboard");
}
```

**Interview Angle**
- Asked in interviews? **Very often**
- Never store or log the plain password in the frontend. Just send it once over HTTPS.

---

## 192. Managing Authentication State

**Simple Meaning**
The whole app needs to know: "Is the user logged in? Who are they?" We store this in a shared place, usually **Context**, so any component can check it.

**Code**
```jsx
const AuthContext = createContext();

function AuthProvider({ children }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  // when the app opens, check if the user was already logged in
  useEffect(() => {
    const token = localStorage.getItem("token");
    if (token) {
      fetch("/api/me", { headers: { Authorization: `Bearer ${token}` } })
        .then((res) => res.json())
        .then(setUser)
        .finally(() => setLoading(false));
    } else {
      setLoading(false);
    }
  }, []);

  const logout = () => {
    localStorage.removeItem("token");
    setUser(null);
  };

  return (
    <AuthContext.Provider value={{ user, setUser, logout, loading }}>
      {children}
    </AuthContext.Provider>
  );
}

export const useAuth = () => useContext(AuthContext);
```

**Interview Angle**
- Asked in interviews? **Very often**
- Confusion: after a page refresh, React state is lost. That is why we check the saved token when the app starts.
- Keep a `loading` state so you don't flash the login page for a split second.

---

## 193. Protected Routes

**Simple Meaning**
A protected route is a page only logged-in users can see. If a visitor is not logged in, you send them to the login page.

**Code**
```jsx
import { Navigate } from "react-router-dom";

function ProtectedRoute({ children }) {
  const { user, loading } = useAuth();

  if (loading) return <p>Loading...</p>;
  if (!user) return <Navigate to="/login" replace />;

  return children;
}

// Use it
<Route
  path="/dashboard"
  element={
    <ProtectedRoute>
      <Dashboard />
    </ProtectedRoute>
  }
/>
```

**Interview Angle**
- Asked in interviews? **Very often** (popular coding task)
- Remember the `replace` keyword. It stops the user from pressing Back to return to the blocked page.
- Important: this only hides the page. See topic 200.

---

## 194. Access Tokens and Refresh Tokens — Basics

**Simple Meaning**
- **Access token**: a short-life ticket (like 15 minutes) used for every request.
- **Refresh token**: a long-life ticket (like 7 days) used only to get a **new** access token when the old one ends.

Why two? If someone steals the access token, it stops working soon. The user does not need to log in again and again because the refresh token quietly gets a new one.

**Code**
```js
// If the server says 401 (token expired), try to refresh
async function request(url) {
  let res = await fetch(url, { headers: { Authorization: `Bearer ${accessToken}` } });

  if (res.status === 401) {
    const refreshRes = await fetch("/api/refresh", { method: "POST", credentials: "include" });
    if (refreshRes.ok) {
      const data = await refreshRes.json();
      accessToken = data.accessToken;
      res = await fetch(url, { headers: { Authorization: `Bearer ${accessToken}` } });
    }
  }
  return res;
}
```

**Interview Angle**
- Asked in interviews? **Often**
- Good answer: "Access token is short and used often. Refresh token is long and used rarely, only to get a new access token."

---

## 195. Cookies vs Local Storage for Tokens

**Simple Meaning**
Both are places in the browser to keep the token.

| | localStorage | HttpOnly cookie |
|---|---|---|
| Can JavaScript read it? | Yes | **No** |
| Risk from XSS attacks | High (a bad script can steal it) | Low |
| Sent automatically to server | No, you add it | Yes |
| Other risk | | CSRF (needs extra protection like SameSite) |
| Setup | Easy | Server must set it |

Most security experts prefer **HttpOnly cookies** for tokens because JavaScript cannot read them.

**Code**
```js
// localStorage (easy but less safe)
localStorage.setItem("token", token);

// Cookie: server sets it, and in React you only allow it to be sent
fetch("/api/profile", { credentials: "include" });
```

**Interview Angle**
- Asked in interviews? **Very often**
- Good answer: "localStorage is easy but a script attack can steal the token. HttpOnly cookies cannot be read by JavaScript, so they are safer."
- Do not say either one is "100% safe".

---

## 196. Logout and Token Expiration

**Simple Meaning**
- **Logout**: remove the token and user data from the app, and send the user to the login page.
- **Token expiration**: tokens stop working after some time. When that happens, the server returns 401, and the app must log the user out (or refresh the token).

**Code**
```jsx
function logout() {
  localStorage.removeItem("token");
  setUser(null);
  navigate("/login");
}
```

**Interview Angle**
- Asked in interviews? **Often**
- With cookies, logout also needs a server call to clear the cookie.
- Good point: also clear any cached user data so the next person on the same computer cannot see it.

---

## 197. Role-Based UI Rendering

**Simple Meaning**
Different users see different things. An admin sees "Delete user", a normal user does not. The server sends the user's **role** and the UI shows or hides parts based on it.

**Code**
```jsx
function Dashboard() {
  const { user } = useAuth();

  return (
    <>
      <h1>Dashboard</h1>
      {user.role === "admin" && <button>Delete User</button>}
      {["admin", "editor"].includes(user.role) && <button>Edit Post</button>}
    </>
  );
}
```

**Interview Angle**
- Asked in interviews? **Often**
- Big warning: hiding a button is only for looks. The **server must also check the role**. See topic 200.

---

## 198. Frontend Security Fundamentals

**Simple Meaning**
The frontend runs in the user's browser, so anyone can look at it and change it. Basic safety rules:
- Never put passwords or secret keys in React code.
- Never trust the frontend alone. The server must check everything.
- Do not show user-typed text as raw HTML.
- Always use HTTPS.
- Keep your packages updated.
- Be careful where you store tokens.

**Code**
```jsx
// BAD: a secret in frontend code (anyone can see it)
const SECRET_KEY = "abc123";

// OK: only public values in VITE_ variables
const url = import.meta.env.VITE_API_URL;
```

**Interview Angle**
- Asked in interviews? **Often**
- One-line answer: "Anything in the frontend is public. So secrets and important checks belong on the server."

---

## 199. Cross-Site Scripting (XSS) Basics

**Simple Meaning**
XSS is when a bad person puts harmful JavaScript into your website (for example, inside a comment), and it runs in other users' browsers. It can steal tokens or user data.

React helps: it **escapes text by default**, so `{userInput}` is safe. The danger comes when you force raw HTML using `dangerouslySetInnerHTML`.

**Code**
```jsx
const comment = "<img src=x onerror='alert(1)'>";

// SAFE: shown as plain text
<p>{comment}</p>

// DANGEROUS: runs the HTML
<p dangerouslySetInnerHTML={{ __html: comment }} />
```
If you must show HTML, clean it first with a library like `DOMPurify`.

**Interview Angle**
- Asked in interviews? **Very often**
- Key phrase: `dangerouslySetInnerHTML`. The name itself is a warning.
- Mistake: saying "React is fully safe from XSS". It is safe by default, but you can break that safety.
- Also avoid using user-given values directly in links like `href={userInput}`.

---

## 200. Why Frontend Route Protection Is Not Authorization

**Simple Meaning**
A protected route in React only **hides** the page. But the code is in the user's browser, so a smart user can change it, open developer tools, or call your API directly without using your website.

Real protection must happen on the **server**. The server must check the token and role on every request.

**Code**
```jsx
// Frontend: only a nice experience
if (!user) return <Navigate to="/login" />;

// The real check happens on the server, for example:
// app.get("/api/admin", checkToken, checkRole("admin"), handler);
```

**Interview Angle**
- Asked in interviews? **Very often** (this is a favourite)
- Best line: "Frontend protection is for user experience. Server protection is for security."
- Mistake: thinking a protected route keeps data safe.

---

## 201. Handling Unauthorized API Responses

**Simple Meaning**
Sometimes the server replies **401** (not logged in or token expired) or **403** (not allowed). Your app should handle these in one central place: log the user out on 401, and show a "not allowed" message on 403.

**Code**
```js
import axios from "axios";

const api = axios.create({ baseURL: import.meta.env.VITE_API_URL });

api.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      localStorage.removeItem("token");
      window.location.href = "/login";
    }
    if (error.response?.status === 403) {
      alert("You do not have permission to do this.");
    }
    return Promise.reject(error);
  }
);
```

**Interview Angle**
- Asked in interviews? **Often**
- Know the difference: 401 = not logged in, 403 = logged in but not allowed.
- Handling it in one place (interceptor) is better than checking in every component.

---

# Level 11: Performance Optimization

## 202. React Performance Fundamentals

**Simple Meaning**
Performance means how fast and smooth your app feels. In React, most slowness comes from:
1. Components re-rendering too often.
2. Doing heavy work on every render.
3. Showing too many items at once.
4. Loading too much code at the start.

Golden rule: **First measure, then fix.** Do not make code complicated without knowing where the problem is.

**Interview Angle**
- Asked in interviews? **Very often**
- Good answer: "I find the slow part using React Profiler, then fix that part only."
- Mistake: adding `useMemo` and `useCallback` everywhere "just in case".

---

## 203. Identifying Unnecessary Re-renders

**Simple Meaning**
A re-render means React runs your component function again. It is normal. It is a problem only when the component re-renders but **nothing on screen changed**.

A component re-renders when:
- Its own state changes.
- Its parent re-renders (even if props are the same).
- A context it uses changes.

**Code**
```jsx
function Parent() {
  const [count, setCount] = useState(0);
  return (
    <>
      <button onClick={() => setCount(count + 1)}>{count}</button>
      <Child />  {/* Child re-renders on every click, even though it needs nothing */}
    </>
  );
}

function Child() {
  console.log("Child rendered"); // add this to see re-renders
  return <p>I am a child</p>;
}
```

**Interview Angle**
- Asked in interviews? **Very often**
- Common confusion: "Child re-renders only when its props change." Wrong. It re-renders whenever the parent does, unless you use `React.memo`.

---

## 204. React DevTools

**Simple Meaning**
React DevTools is a browser extension (Chrome, Firefox, Edge). It adds two tabs in the developer tools: **Components** (see your component tree, props and state) and **Profiler** (measure speed).

**How to use**
- Install the "React Developer Tools" extension.
- Open browser DevTools (F12) and click **Components**.
- Click a component to see its props, state, and hooks.
- Turn on "Highlight updates when components render" in settings to see which components re-render.

**Interview Angle**
- Asked in interviews? **Sometimes**
- Say: "I use React DevTools to check props and state, and to see what re-renders."

---

## 205. React Profiler

**Simple Meaning**
The Profiler records what happens while you use your app and shows which components took the most time to render and why they rendered.

**Steps**
1. Open DevTools and go to the **Profiler** tab.
2. Click the record button.
3. Use your app (click, type, scroll).
4. Stop recording.
5. Look at the chart. Long, bright bars are the slow components.

**Code** (the `<Profiler>` component can also be used in code)
```jsx
import { Profiler } from "react";

function onRender(id, phase, actualDuration) {
  console.log(id, phase, actualDuration + "ms");
}

<Profiler id="ProductList" onRender={onRender}>
  <ProductList />
</Profiler>
```

**Interview Angle**
- Asked in interviews? **Sometimes**
- Good answer: "I record using Profiler, find the slowest component, and then decide how to fix it."
- Profile a production build for accurate results, because development mode is slower.

---

## 206. Memoization and Its Trade-offs

**Simple Meaning**
Memoization means **remembering a result**, so you do not calculate it again when the input is the same. Like writing down 12 x 12 = 144 so you do not calculate every time.

In React: `React.memo`, `useMemo`, and `useCallback` all use this idea.

**Trade-offs (the price you pay)**
- Uses extra memory.
- Adds more code, harder to read.
- React must still compare the old and new inputs, which also takes time.
- If the thing you memoize is cheap, you may be slower, not faster.

**Interview Angle**
- Asked in interviews? **Very often**
- The best answer includes the downsides: "Memoization is not free. I use it only when I have measured a problem."

---

## 207. Optimizing Expensive Calculations

**Simple Meaning**
If a calculation is slow (filtering 10,000 items, heavy math) and it runs on every render, the app feels slow. Use `useMemo` to run it only when its inputs change.

**Code**
```jsx
// Slow: runs on every render, even when "theme" changes
const filtered = products.filter((p) => p.name.includes(search));

// Better: runs only when products or search change
const filtered = useMemo(
  () => products.filter((p) => p.name.includes(search)),
  [products, search]
);
```

**Interview Angle**
- Asked in interviews? **Often**
- Tip: do not use `useMemo` for tiny work like adding two numbers.

---

## 208. React.memo in Practice

**Simple Meaning**
`React.memo` wraps a component and tells React: "Do not re-render this if its props are the same as last time."

**Code**
```jsx
import { memo } from "react";

const Child = memo(function Child({ name }) {
  console.log("Child rendered");
  return <p>{name}</p>;
});

function Parent() {
  const [count, setCount] = useState(0);
  return (
    <>
      <button onClick={() => setCount(count + 1)}>{count}</button>
      <Child name="Ravi" />  {/* does NOT re-render when count changes */}
    </>
  );
}
```

**Interview Angle**
- Asked in interviews? **Very often**
- Top trap: it **does not work** if you pass a new object, array, or function each time as props, because they are never "the same". Fix with `useMemo` or `useCallback`.
- It compares props shallowly (just the top level).

---

## 209. useMemo in Practice

**Simple Meaning**
`useMemo` remembers a **value** (the result of a calculation). It recalculates only when the values in its dependency list change.

**Code**
```jsx
const total = useMemo(() => {
  return cart.reduce((sum, item) => sum + item.price * item.qty, 0);
}, [cart]);

// Also useful to keep an object the same, so a memo child does not re-render
const options = useMemo(() => ({ theme: "dark" }), []);
```

**Interview Angle**
- Asked in interviews? **Very often**
- Two uses: (1) skip heavy calculation, (2) keep the same object/array so children do not re-render.
- `useMemo` is a performance helper, not a promise. React may throw away the saved value in some cases.

---

## 210. useCallback in Practice

**Simple Meaning**
`useCallback` remembers a **function**. Normally, a new function is made on every render. `useCallback` keeps the same function until its dependencies change.

**Code**
```jsx
const Child = memo(function Child({ onClick }) {
  console.log("Child rendered");
  return <button onClick={onClick}>Click</button>;
});

function Parent() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    console.log("clicked");
  }, []);

  return (
    <>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>Add</button>
      <Child onClick={handleClick} />
    </>
  );
}
```

**Interview Angle**
- Asked in interviews? **Very often**
- Key point: `useCallback` is useful only with `React.memo` (or inside a dependency list). Alone, it does nothing helpful.
- Quick difference: `useMemo(() => value)` remembers a value. `useCallback(fn)` remembers the function. `useCallback(fn, deps)` is the same as `useMemo(() => fn, deps)`.

---

## 211. Avoiding Unnecessary Effects

**Simple Meaning**
Many people use `useEffect` when they do not need it. If you can work something out **during rendering**, do not use an effect.

**Code**
```jsx
// BAD: extra state + effect
const [fullName, setFullName] = useState("");
useEffect(() => {
  setFullName(firstName + " " + lastName);
}, [firstName, lastName]);

// GOOD: just calculate it
const fullName = firstName + " " + lastName;
```
```jsx
// BAD: effect to react to a click
useEffect(() => { if (submitted) sendData(); }, [submitted]);

// GOOD: do it inside the event handler
function handleSubmit() { sendData(); }
```

**Use effects only for:** talking to outside things (API calls, timers, event listeners on window).

**Interview Angle**
- Asked in interviews? **Often**
- Good line: "If it can be calculated from props or state, I don't use an effect."
- Extra effects cause extra renders.

---

## 212. Code Splitting

**Simple Meaning**
By default, all your JavaScript is put into one big file, and the user downloads everything at the start. Code splitting breaks it into **smaller pieces**, so the user downloads a page's code only when they visit that page. The first load becomes faster.

**Code**
```jsx
// The "import()" function loads code only when needed
const AdminPage = lazy(() => import("./AdminPage"));
```
(See the next topic for the full example.)

**Interview Angle**
- Asked in interviews? **Often**
- Best place to split: **by route** (each page loads on its own).
- Vite and other build tools make the split files automatically when you use `import()`.

---

## 213. Lazy Loading and Suspense

**Simple Meaning**
- **Lazy loading**: load a component only when it is needed.
- **Suspense**: shows a temporary screen (like "Loading...") while the lazy component downloads.

**Code**
```jsx
import { lazy, Suspense } from "react";
import { Routes, Route } from "react-router-dom";

const Home = lazy(() => import("./pages/Home"));
const About = lazy(() => import("./pages/About"));

function App() {
  return (
    <Suspense fallback={<p>Loading page...</p>}>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </Suspense>
  );
}
```

**Interview Angle**
- Asked in interviews? **Very often**
- Rules: `lazy` works only with **default exports**. A lazy component must be inside a `<Suspense>`, or React shows an error.
- `fallback` is what shows while waiting.

---

## 214. List Virtualization Basics

**Simple Meaning**
If you have 10,000 items, putting all of them in the page makes it very slow. Virtualization (also called windowing) renders **only the items you can see on screen** (maybe 15), and swaps them as you scroll.

**Code**
```bash
npm install react-window
```
```jsx
import { FixedSizeList } from "react-window";

function Row({ index, style }) {
  return <div style={style}>Item {index}</div>;
}

function BigList() {
  return (
    <FixedSizeList height={400} width={300} itemCount={10000} itemSize={35}>
      {Row}
    </FixedSizeList>
  );
}
```

**Interview Angle**
- Asked in interviews? **Often**
- Good answer: "I only render what the user can see." Popular libraries: `react-window`, `react-virtuoso`, `@tanstack/react-virtual`.

---

## 215. Optimizing Large Lists and Forms

**Simple Meaning**
Ways to make big lists fast:
- Use stable, unique `key` values (never the array index if the list can change).
- Wrap list items in `React.memo`.
- Use pagination or virtualization.
- Debounce search.

Ways to make big forms fast:
- Use React Hook Form (it re-renders less).
- Split the form into smaller components.
- Keep each input's state near the input.

**Code**
```jsx
const Item = memo(function Item({ item }) {
  return <li>{item.name}</li>;
});

function List({ items }) {
  return (
    <ul>
      {items.map((item) => (
        <Item key={item.id} item={item} />
      ))}
    </ul>
  );
}
```

**Interview Angle**
- Asked in interviews? **Often**
- Mistake: `key={index}`. It causes bugs and extra work when items are added, removed or reordered.

---

## 216. Image and Asset Optimization

**Simple Meaning**
Images are usually the heaviest part of a website. Make them lighter:
- Use modern formats like **WebP** or AVIF.
- Resize images to the size you really show.
- Use **lazy loading**, so images below the screen load later.
- Set `width` and `height` so the page does not jump around.

**Code**
```jsx
<img
  src="/photo.webp"
  alt="A red shoe"
  width="300"
  height="200"
  loading="lazy"
/>
```

**Interview Angle**
- Asked in interviews? **Often**
- Easy win to mention: `loading="lazy"`.
- Always write an `alt` text (also good for accessibility).

---

## 217. React Transitions and useTransition

**Simple Meaning**
Some updates are urgent (typing in a box). Others can wait a little (filtering a big list). `useTransition` lets you mark the slow update as "not urgent", so the screen stays smooth and typing never feels stuck.

**Code**
```jsx
import { useState, useTransition } from "react";

function Search({ items }) {
  const [text, setText] = useState("");
  const [list, setList] = useState(items);
  const [isPending, startTransition] = useTransition();

  function handleChange(e) {
    setText(e.target.value);              // urgent: show typed text now

    startTransition(() => {
      setList(items.filter((i) => i.includes(e.target.value))); // can wait
    });
  }

  return (
    <>
      <input value={text} onChange={handleChange} />
      {isPending && <p>Updating...</p>}
      {list.map((i) => <p key={i}>{i}</p>)}
    </>
  );
}
```

**Interview Angle**
- Asked in interviews? **Sometimes**
- Say: "useTransition marks a state update as low priority, so important updates like typing are not blocked."

---

## 218. useDeferredValue

**Simple Meaning**
`useDeferredValue` gives you a "late copy" of a value. The input uses the fast, new value. The slow part of the screen uses the late copy, which updates a moment after. It is like `useTransition`, but you use it when you only have the **value**, not control of the code that sets it.

**Code**
```jsx
import { useState, useDeferredValue } from "react";

function Search({ items }) {
  const [text, setText] = useState("");
  const deferredText = useDeferredValue(text);

  const results = items.filter((i) => i.includes(deferredText));

  return (
    <>
      <input value={text} onChange={(e) => setText(e.target.value)} />
      {results.map((i) => <p key={i}>{i}</p>)}
    </>
  );
}
```

**Interview Angle**
- Asked in interviews? **Sometimes**
- Difference: `useTransition` wraps the **update** (setState). `useDeferredValue` wraps the **value**.
- It is not the same as debounce. Debounce waits for a fixed time. `useDeferredValue` has no fixed delay.

---

## 219. Core Web Vitals Fundamentals

**Simple Meaning**
Core Web Vitals are three scores Google uses to judge how good your website feels.

| Name | Full name | What it checks | Good score |
|---|---|---|---|
| LCP | Largest Contentful Paint | How fast the main content appears | Under 2.5 seconds |
| INP | Interaction to Next Paint | How fast the page reacts to clicks and typing | Under 200 ms |
| CLS | Cumulative Layout Shift | Does the page jump around while loading? | Under 0.1 |

**Simple tips**
- LCP: optimize images, use code splitting.
- INP: avoid heavy work on clicks, use `useTransition`.
- CLS: set image sizes, do not push content down suddenly.

(INP replaced an older score called FID.)

**Interview Angle**
- Asked in interviews? **Sometimes**
- Know the three names and one simple meaning each.
- You can check them using Lighthouse in Chrome DevTools.

---

# Level 12: Advanced React Concepts

## 220. Concurrent Rendering — Fundamentals

**Simple Meaning**
In old React, once it started updating the screen, it had to finish the whole job without stopping. If the job was big, the page froze.

Concurrent rendering lets React **work on updates in small steps, pause, and handle urgent things first** (like a click or a key press). The screen stays responsive.

Think of a cook who is making a big meal, but stops for a moment to answer the door, then goes back to cooking.

**Code**
You do not write special code for it. You get it by using React 18+ (`createRoot`), and you use tools like `useTransition` and `useDeferredValue` to say what is less important.
```jsx
import { createRoot } from "react-dom/client";
createRoot(document.getElementById("root")).render(<App />);
```

**Interview Angle**
- Asked in interviews? **Sometimes**
- Do not say "React uses multiple threads". It does not. It is still one thread, but it can pause and switch work.

---

## 221. Interruptible Rendering — Conceptual Basics

**Simple Meaning**
Interruptible rendering means React can **stop a slow, low-priority update halfway**, handle a more urgent one, and then continue (or even throw away the old work and restart with fresh data).

Example: you are typing in a search box. The list update is slow. React pauses the list work, shows your typed letter right away, and then continues the list.

**Code**
```jsx
startTransition(() => {
  setBigList(newList);   // low priority, can be interrupted
});
setText(value);          // high priority, runs first
```

**Interview Angle**
- Asked in interviews? **Sometimes**
- Because of this, render functions should be **pure** (no side effects). React may run them more than once or throw away the result.

---

## 222. Automatic Batching

**Simple Meaning**
Batching means React **groups several state updates into one re-render**, instead of re-rendering after each one. In React 18, this works everywhere automatically: in event handlers, timeouts, promises, and so on.

**Code**
```jsx
function handleClick() {
  setCount((c) => c + 1);
  setName("Ravi");
  setLoading(false);
  // React 18: only ONE re-render for all three
}

// Even inside async code
fetch("/api").then(() => {
  setData(result);
  setLoading(false);
  // React 18: still only ONE re-render
});
```

**Interview Angle**
- Asked in interviews? **Often**
- Difference from React 17: older React batched only inside React event handlers. React 18 batches everywhere.
- If you really need an instant re-render, use `flushSync` (rare).

---

## 223. useId

**Simple Meaning**
`useId` creates a **unique ID** for you. It is useful for connecting a label to an input, especially when the same component is used many times on a page.

**Code**
```jsx
import { useId } from "react";

function EmailField() {
  const id = useId();
  return (
    <>
      <label htmlFor={id}>Email</label>
      <input id={id} type="email" />
    </>
  );
}
```

**Interview Angle**
- Asked in interviews? **Sometimes**
- Do **not** use `useId` to make `key` values for lists. It is meant for HTML ids.
- It gives the same ID on the server and the browser, which avoids errors in SSR.

---

## 224. useSyncExternalStore — Use Cases

**Simple Meaning**
This hook lets React safely read data that lives **outside React**, such as the browser's online status, window size, or a custom store. It keeps the screen correct, even with concurrent rendering.

You will mostly meet it inside libraries (Redux, Zustand use it inside). You rarely write it yourself.

**Code**
```jsx
import { useSyncExternalStore } from "react";

function subscribe(callback) {
  window.addEventListener("online", callback);
  window.addEventListener("offline", callback);
  return () => {
    window.removeEventListener("online", callback);
    window.removeEventListener("offline", callback);
  };
}

function useOnlineStatus() {
  return useSyncExternalStore(subscribe, () => navigator.onLine);
}

function Status() {
  const isOnline = useOnlineStatus();
  return <p>{isOnline ? "Online" : "Offline"}</p>;
}
```

**Interview Angle**
- Asked in interviews? **Rarely**
- Good one-liner: "It connects React to outside data sources safely."

---

## 225. useImperativeHandle — Use Cases

**Simple Meaning**
Normally, a parent cannot control the inside of a child. With `useImperativeHandle`, a child can choose **which functions to give** to the parent (like `focus()` or `reset()`), without giving full access to everything inside.

**Code**
```jsx
import { forwardRef, useImperativeHandle, useRef } from "react";

const FancyInput = forwardRef(function FancyInput(props, ref) {
  const inputRef = useRef();

  useImperativeHandle(ref, () => ({
    focus() {
      inputRef.current.focus();
    },
    clear() {
      inputRef.current.value = "";
    },
  }));

  return <input ref={inputRef} />;
});

function App() {
  const ref = useRef();
  return (
    <>
      <FancyInput ref={ref} />
      <button onClick={() => ref.current.focus()}>Focus</button>
      <button onClick={() => ref.current.clear()}>Clear</button>
    </>
  );
}
```
(In React 19, you can pass `ref` directly as a prop, and `forwardRef` is no longer needed.)

**Interview Angle**
- Asked in interviews? **Rarely**
- Use only when really needed. Props and state are the normal way.

---

## 226. forwardRef and Ref Forwarding

**Simple Meaning**
A `ref` is a direct link to an element. But if you put `ref` on your own component, it does not reach the element inside. `forwardRef` lets a component **pass the ref down** to an element inside it.

**Code**
```jsx
import { forwardRef, useRef } from "react";

const MyInput = forwardRef(function MyInput(props, ref) {
  return <input ref={ref} {...props} />;
});

function App() {
  const inputRef = useRef();
  return (
    <>
      <MyInput ref={inputRef} placeholder="Type here" />
      <button onClick={() => inputRef.current.focus()}>Focus input</button>
    </>
  );
}
```

**Interview Angle**
- Asked in interviews? **Often** (for reusable components)
- Confusion: `ref` is not a normal prop in React 18. Without `forwardRef` it won't arrive in the child.
- In React 19, `ref` works as a normal prop for function components.

---

## 227. Imperative vs Declarative Programming

**Simple Meaning**
- **Imperative**: you give step-by-step instructions on **how** to do it.
- **Declarative**: you describe **what** you want, and the system figures out how.

React is declarative. You describe what the screen should look like for a given state, and React updates the screen.

**Code**
```js
// Imperative (plain JavaScript): step by step
const p = document.getElementById("msg");
if (isLoggedIn) {
  p.textContent = "Welcome";
} else {
  p.textContent = "Please login";
}
```
```jsx
// Declarative (React): describe the result
<p>{isLoggedIn ? "Welcome" : "Please login"}</p>
```

**Interview Angle**
- Asked in interviews? **Often**
- Easy example: "Imperative is giving directions turn by turn. Declarative is just telling the taxi the address."

---

## 228. Error Boundaries and Fallback UIs

**Simple Meaning**
If a component crashes while rendering, the **whole app goes blank**. An error boundary is a safety net. It catches the crash in its children and shows a **fallback UI** (like "Something went wrong") instead.

Error boundaries are written as **class components** (there is no hook for it). The easy way is to use the `react-error-boundary` library.

**Code**
```bash
npm install react-error-boundary
```
```jsx
import { ErrorBoundary } from "react-error-boundary";

function Fallback({ error, resetErrorBoundary }) {
  return (
    <div>
      <p>Something went wrong.</p>
      <button onClick={resetErrorBoundary}>Try again</button>
    </div>
  );
}

<ErrorBoundary FallbackComponent={Fallback}>
  <Dashboard />
</ErrorBoundary>
```

**Interview Angle**
- Asked in interviews? **Very often**
- Important: error boundaries catch errors in **rendering** only. They do **not** catch errors in event handlers, async code (like fetch), or the boundary itself.
- Place them around big sections, so one crash does not break everything.

---

## 229. Suspense for Lazy-Loaded Components

**Simple Meaning**
`Suspense` shows a fallback while something is not ready. The most common use is with `lazy`, while the component's code is downloading. (Newer frameworks also use it while data is loading.)

**Code**
```jsx
const Chart = lazy(() => import("./Chart"));

function Report() {
  return (
    <Suspense fallback={<p>Loading chart...</p>}>
      <Chart />
    </Suspense>
  );
}
```

**Interview Angle**
- Asked in interviews? **Often**
- Combine ideas: **Suspense** handles "still loading", **Error Boundary** handles "failed". Often used together.

---

## 230. Server-Side Rendering (SSR)

**Simple Meaning**
Normally in React (client-side rendering), the browser gets an empty page and JavaScript builds the screen. With SSR, the **server builds the HTML first** and sends a ready page. The user sees content faster, and search engines can read it easily.

**Code**
Usually done with a framework like Next.js.
```jsx
// Next.js (pages router) example
export async function getServerSideProps() {
  const res = await fetch("https://api.example.com/products");
  const products = await res.json();
  return { props: { products } };
}

export default function Products({ products }) {
  return products.map((p) => <p key={p.id}>{p.name}</p>);
}
```

**Interview Angle**
- Asked in interviews? **Very often**
- Benefits: faster first view, better SEO. Cost: needs a server, more complex.
- Compare: CSR = browser builds. SSR = server builds on every request.

---

## 231. Static Site Generation (SSG)

**Simple Meaning**
With SSG, the HTML pages are built **once, at build time** (before anyone visits), and saved as files. When a user visits, the ready file is served instantly. It is very fast and cheap. Best for pages that rarely change (blogs, docs, marketing pages).

**Code**
```jsx
// Next.js (pages router) example
export async function getStaticProps() {
  const res = await fetch("https://api.example.com/posts");
  const posts = await res.json();
  return { props: { posts } };
}
```

**Interview Angle**
- Asked in interviews? **Often**
- Easy comparison:
  - **SSG**: built once at build time.
  - **SSR**: built on every request.
  - **CSR**: built in the browser.
- Weakness: if data changes, you must rebuild (or use revalidation).

---

## 232. Hydration

**Simple Meaning**
When the server sends ready HTML (SSR or SSG), the page looks complete but buttons do not work yet. **Hydration** is when React loads in the browser and "wakes up" that HTML by attaching click handlers and state. It is like adding electricity to a finished machine.

**Code**
```jsx
import { hydrateRoot } from "react-dom/client";
hydrateRoot(document.getElementById("root"), <App />);
```

**Interview Angle**
- Asked in interviews? **Often** (when SSR is discussed)
- Common error: **hydration mismatch**. This happens when server HTML and browser HTML are different. Typical causes: using `Date.now()`, `Math.random()`, or `window` while rendering.

---

## 233. Server Components vs Client Components

**Simple Meaning**
- **Server Components**: run **only on the server**. They send plain output to the browser, with no JavaScript for that component. They can read from a database directly. They cannot use `useState`, `useEffect`, or click handlers.
- **Client Components**: run in the browser. They can use state, effects, and events.

In Next.js App Router, components are Server Components by default. Add `"use client"` at the top to make a Client Component.

**Code**
```jsx
// Server Component (no directive needed, can be async)
export default async function Products() {
  const res = await fetch("https://api.example.com/products");
  const products = await res.json();
  return <ul>{products.map((p) => <li key={p.id}>{p.name}</li>)}</ul>;
}
```
```jsx
"use client"; // makes it a Client Component
import { useState } from "react";

export default function LikeButton() {
  const [likes, setLikes] = useState(0);
  return <button onClick={() => setLikes(likes + 1)}>Likes: {likes}</button>;
}
```

**Interview Angle**
- Asked in interviews? **Often** (for modern React roles)
- Confusion: "Server Components" is **not** the same as "Server-Side Rendering". SSR still sends all JavaScript to the browser for hydration. Server Components send none for those parts.
- Simple rule: need clicks or state? Client Component. Just showing data? Server Component.

---

## 234. React Frameworks and Next.js Fundamentals

**Simple Meaning**
React is only a library for building screens. It does not give you routing, server rendering, or a build setup. A **framework** like Next.js gives you all of these ready-made.

Next.js gives:
- File-based routing (a file in `app/about/page.js` becomes `/about`).
- SSR, SSG, and Server Components.
- API routes.
- Image and font optimization.

**Code**
```bash
npx create-next-app@latest
```
```jsx
// app/about/page.js  ->  shown at /about
export default function About() {
  return <h1>About Us</h1>;
}
```

**Interview Angle**
- Asked in interviews? **Often**
- Good answer: "React is a library. Next.js is a framework built on React that adds routing, server rendering and more."
- Other frameworks: Remix (now merged into React Router), Gatsby.

---

## 235. React Compiler — Basic Purpose and Implications

**Simple Meaning**
The React Compiler is a build tool that **automatically adds memoization** for you. It reads your code and decides where to skip extra re-renders. This means you may not need to write `useMemo`, `useCallback`, and `React.memo` by hand in most cases.

**Code**
```jsx
// Before: you write memoization by hand
const handleClick = useCallback(() => doSomething(id), [id]);

// With the compiler: write normal code, compiler optimizes it
const handleClick = () => doSomething(id);
```

**Implications**
- Cleaner code with less manual optimization.
- Your code must follow React's rules (pure components, no changing state directly).
- You still need to understand memoization, because old code and interviews still use it.

**Interview Angle**
- Asked in interviews? **Sometimes** (growing)
- Good answer: "The compiler automatically optimizes re-renders, so I write less useMemo and useCallback. But I still need to follow the React rules."

---

# Level 13: Testing and Accessibility

## 236. Why Test React Applications?

**Simple Meaning**
Testing means writing small programs that check if your app works correctly. Instead of clicking everything by hand after each change, the tests do it for you in seconds.

Why test:
- Catch bugs before users do.
- Change code without fear of breaking old features.
- Tests also work like instructions that show how a component should behave.

**Interview Angle**
- Asked in interviews? **Very often**
- Good answer: "Tests give me confidence that my change did not break something else."
- Do not say "tests make an app bug-free". They reduce bugs, not remove them.

---

## 237. Unit vs Integration Tests

**Simple Meaning**
- **Unit test**: tests one small piece alone (one function, one small component).
- **Integration test**: tests several pieces working together (a form + validation + submit button).
- (End-to-end tests check the whole app like a real user, using tools like Cypress or Playwright.)

**Code**
```jsx
// Unit: one small function
test("adds two numbers", () => {
  expect(add(2, 3)).toBe(5);
});

// Integration: typing in the form and seeing a result
test("shows welcome message after login", async () => {
  render(<LoginPage />);
  await userEvent.type(screen.getByLabelText("Email"), "a@b.com");
  await userEvent.click(screen.getByRole("button", { name: "Login" }));
  expect(await screen.findByText("Welcome")).toBeInTheDocument();
});
```

**Interview Angle**
- Asked in interviews? **Very often**
- For React apps, integration tests are very valuable, because users use features, not single functions.

---

## 238. Vitest Fundamentals

**Simple Meaning**
Vitest is a tool that **runs your tests**. It is fast and works very well with Vite projects. Its commands are almost the same as Jest, so if you know one, you know the other.

**Code**
```bash
npm install -D vitest
```
```js
// math.test.js
import { describe, it, expect } from "vitest";
import { add } from "./math";

describe("add function", () => {
  it("adds two numbers", () => {
    expect(add(2, 3)).toBe(5);
  });

  it("works with negative numbers", () => {
    expect(add(-1, -1)).toBe(-2);
  });
});
```
Run with: `npx vitest`

**Interview Angle**
- Asked in interviews? **Often**
- Key words: `describe` (group), `it` or `test` (one test), `expect` (the check).
- Say: "Vitest is like Jest but made for Vite."

---

## 239. React Testing Library

**Simple Meaning**
React Testing Library (RTL) helps you test React components **the way a user uses them**. It does not look at the inside code (state, functions). It looks at what appears on screen, and what a user can click or type.

**Code**
```bash
npm install -D @testing-library/react @testing-library/jest-dom @testing-library/user-event jsdom
```
```jsx
import { render, screen } from "@testing-library/react";

test("shows the heading", () => {
  render(<h1>Hello</h1>);
  expect(screen.getByText("Hello")).toBeInTheDocument();
});
```
Main helpers: `render` (draw the component), `screen` (search the screen), `getBy...` (find an element).

**Interview Angle**
- Asked in interviews? **Very often**
- Main idea: "Test what the user sees, not how the code is written inside."
- Preferred way to find elements: `getByRole`, `getByLabelText`. Use `getByTestId` as the last choice.

---

## 240. Testing Component Rendering

**Simple Meaning**
This checks that a component shows the right things when it is drawn, with the right props.

**Code**
```jsx
// Greeting.jsx
function Greeting({ name }) {
  return <h1>Hello, {name}!</h1>;
}
```
```jsx
// Greeting.test.jsx
import { render, screen } from "@testing-library/react";

test("shows the name", () => {
  render(<Greeting name="Ravi" />);
  expect(screen.getByText("Hello, Ravi!")).toBeInTheDocument();
});

test("does not show an error at the start", () => {
  render(<Greeting name="Ravi" />);
  expect(screen.queryByText("Error")).not.toBeInTheDocument();
});
```

**Interview Angle**
- Asked in interviews? **Often**
- Know the three finders:
  - `getBy`: must exist, or it errors.
  - `queryBy`: returns null if missing (use it to check something is **not** there).
  - `findBy`: waits for it to appear (for async things).

---

## 241. Testing User Interactions

**Simple Meaning**
This checks what happens when a user clicks, types, or selects. Use `userEvent`, which acts like a real user.

**Code**
```jsx
// Counter.jsx
function Counter() {
  const [count, setCount] = useState(0);
  return (
    <>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Add</button>
    </>
  );
}
```
```jsx
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";

test("increases count on click", async () => {
  const user = userEvent.setup();
  render(<Counter />);

  await user.click(screen.getByRole("button", { name: "Add" }));

  expect(screen.getByText("Count: 1")).toBeInTheDocument();
});
```

**Interview Angle**
- Asked in interviews? **Often**
- Mistake: forgetting `await` before `user.click`. The test may pass or fail randomly.
- `userEvent` is better than `fireEvent` because it behaves more like a real person.

---

## 242. Testing Forms and Validation

**Simple Meaning**
Type into the inputs, press submit, and check that the correct error or success message appears.

**Code**
```jsx
test("shows error for an empty email", async () => {
  const user = userEvent.setup();
  render(<LoginForm />);

  await user.click(screen.getByRole("button", { name: "Login" }));

  expect(screen.getByText("Email is required")).toBeInTheDocument();
});

test("calls submit with the typed values", async () => {
  const user = userEvent.setup();
  const onSubmit = vi.fn(); // a fake function that records calls
  render(<LoginForm onSubmit={onSubmit} />);

  await user.type(screen.getByLabelText("Email"), "a@b.com");
  await user.type(screen.getByLabelText("Password"), "123456");
  await user.click(screen.getByRole("button", { name: "Login" }));

  expect(onSubmit).toHaveBeenCalledWith({ email: "a@b.com", password: "123456" });
});
```

**Interview Angle**
- Asked in interviews? **Often**
- `vi.fn()` creates a fake function (a "mock") so you can check if it was called.
- Using `getByLabelText` also proves your form is accessible.

---

## 243. Mocking API Requests

**Simple Meaning**
In tests, you should **not call the real server** (it is slow, may be down, and data changes). Instead, you fake the response. This is called mocking.

Two ways:
1. Mock `fetch` directly (simple).
2. Use **MSW (Mock Service Worker)**, which fakes the network at a deeper level (popular choice).

**Code**
```jsx
// Simple way: mock fetch
import { vi } from "vitest";

test("shows users from the API", async () => {
  global.fetch = vi.fn().mockResolvedValue({
    ok: true,
    json: async () => [{ id: 1, name: "Ravi" }],
  });

  render(<Users />);

  expect(await screen.findByText("Ravi")).toBeInTheDocument();
});
```
```js
// MSW way
import { http, HttpResponse } from "msw";
import { setupServer } from "msw/node";

const server = setupServer(
  http.get("/api/users", () => HttpResponse.json([{ id: 1, name: "Ravi" }]))
);
beforeAll(() => server.listen());
afterEach(() => server.resetHandlers());
afterAll(() => server.close());
```

**Interview Angle**
- Asked in interviews? **Often**
- Use `findBy` (it waits) for data that arrives later.
- Also test the failing case (server error), not only success.

---

## 244. Testing Custom Hooks

**Simple Meaning**
A custom hook cannot run alone, because hooks only work inside components. So we use `renderHook` from React Testing Library, which gives the hook a small hidden component to live in.

**Code**
```js
// useCounter.js
import { useState } from "react";
export function useCounter(start = 0) {
  const [count, setCount] = useState(start);
  const increment = () => setCount((c) => c + 1);
  return { count, increment };
}
```
```js
// useCounter.test.js
import { renderHook, act } from "@testing-library/react";

test("increments the count", () => {
  const { result } = renderHook(() => useCounter(0));

  act(() => {
    result.current.increment();
  });

  expect(result.current.count).toBe(1);
});
```

**Interview Angle**
- Asked in interviews? **Sometimes**
- Key words: `renderHook`, `result.current`, and `act` (wraps anything that changes state).

---

## 245. Semantic HTML in React

**Simple Meaning**
Semantic HTML means using tags that **describe their meaning**, not just a `div` for everything. Browsers, search engines, and screen readers understand them.

| Instead of | Use |
|---|---|
| `<div>` for a top bar | `<header>` |
| `<div>` for menu links | `<nav>` |
| `<div>` for main part | `<main>` |
| `<div onClick>` as a button | `<button>` |
| `<div>` for side content | `<aside>` |
| `<div>` for bottom | `<footer>` |

**Code**
```jsx
// Bad
<div onClick={save}>Save</div>

// Good
<button onClick={save}>Save</button>
```

**Interview Angle**
- Asked in interviews? **Often**
- Big point: a real `<button>` gives you keyboard support (Tab, Enter, Space) for free. A `div` does not.
- Use one `<h1>` per page, and keep headings in order (h1, h2, h3).

---

## 246. ARIA Attributes — When Needed

**Simple Meaning**
ARIA attributes are extra labels that help screen readers understand your page. But the **first rule of ARIA is: do not use ARIA if a normal HTML tag already does the job.**

Use ARIA when HTML is not enough:
- `aria-label`: gives a name to an element with no visible text (like an icon button).
- `aria-expanded`: tells if a menu is open or closed.
- `aria-hidden`: hides decoration from screen readers.
- `aria-live`: announces changes on screen (like "Item added").
- `role`: tells what a custom element is.

**Code**
```jsx
<button aria-label="Close" onClick={close}>X</button>

<button aria-expanded={open} onClick={() => setOpen(!open)}>Menu</button>

<p aria-live="polite">{message}</p>
```

**Interview Angle**
- Asked in interviews? **Sometimes**
- Wrong ARIA is **worse** than no ARIA. Prefer semantic HTML first.

---

## 247. Keyboard Navigation

**Simple Meaning**
Some people cannot use a mouse. Everything clickable must also work with the keyboard: **Tab** to move forward, **Shift+Tab** to go back, **Enter/Space** to press buttons, **Esc** to close popups, **Arrow keys** for menus.

**Code**
```jsx
function Card({ onOpen }) {
  // if you must use a div, add role, tabIndex and a key handler
  return (
    <div
      role="button"
      tabIndex={0}
      onClick={onOpen}
      onKeyDown={(e) => {
        if (e.key === "Enter" || e.key === " ") onOpen();
      }}
    >
      Open
    </div>
  );
}
```
Better: just use `<button>`.

**Interview Angle**
- Asked in interviews? **Sometimes**
- `tabIndex={0}` puts an element in the Tab order. `tabIndex={-1}` makes it focusable only by code. Avoid positive numbers.
- Never remove the focus outline without giving another clear style.

---

## 248. Focus Management

**Simple Meaning**
Focus means which element is currently "selected" by the keyboard. When something changes on the page (a modal opens, an error appears, the route changes), you should move focus to the right place so keyboard and screen reader users are not lost.

**Code**
```jsx
function SearchBox() {
  const inputRef = useRef();

  useEffect(() => {
    inputRef.current.focus(); // focus the input when the page opens
  }, []);

  return <input ref={inputRef} placeholder="Search" />;
}
```
Examples:
- Modal opens: focus goes inside the modal.
- Modal closes: focus returns to the button that opened it.
- Form submit fails: focus the first field with an error.

**Interview Angle**
- Asked in interviews? **Sometimes**
- Tool: `useRef` + `.focus()`.

---

## 249. Accessible Modals and Dialogs

**Simple Meaning**
A modal is a popup that sits on top of the page. To make it accessible:
- Use `role="dialog"` and `aria-modal="true"`.
- Give it a title using `aria-labelledby`.
- Move focus inside when it opens.
- Keep Tab inside the modal (focus trap).
- Close with the **Esc** key.
- Return focus to the opener when it closes.

The easiest way is to use the built-in HTML `<dialog>` element, or a library like Radix UI or React Aria.

**Code**
```jsx
function Modal({ open, onClose, children }) {
  const closeRef = useRef();

  useEffect(() => {
    if (!open) return;
    closeRef.current.focus();

    const onKey = (e) => e.key === "Escape" && onClose();
    document.addEventListener("keydown", onKey);
    return () => document.removeEventListener("keydown", onKey);
  }, [open, onClose]);

  if (!open) return null;

  return (
    <div role="dialog" aria-modal="true" aria-labelledby="modal-title">
      <h2 id="modal-title">Confirm</h2>
      {children}
      <button ref={closeRef} onClick={onClose}>Close</button>
    </div>
  );
}
```

**Interview Angle**
- Asked in interviews? **Often** (as a coding task)
- Know: `role="dialog"`, `aria-modal`, Esc to close, focus trap, return focus.

---

# Level 14: Production and Deployment

## 250. Development vs Production Builds

**Simple Meaning**
- **Development**: for you while coding. It has helpful warnings, fast reload, and readable code, but it is big and slow.
- **Production**: for real users. The code is made small (minified), warnings are removed, and it is as fast as possible.

| | Development | Production |
|---|---|---|
| Command | `npm run dev` | `npm run build` |
| File size | Big | Small |
| Warnings | Yes | No |
| Speed | Slower | Faster |
| Source code | Readable | Squeezed (minified) |

**Interview Angle**
- Asked in interviews? **Often**
- Never deploy the dev server. Always deploy the build output.
- Strict Mode double-running of effects happens only in development.

---

## 251. Vite Production Build

**Simple Meaning**
Vite creates the final, optimized version of your app with one command. The result goes into a folder called **`dist`**. This folder is what you upload to a host.

**Code**
```bash
npm run build      # creates the dist folder
npm run preview    # test the production build on your computer
```
What Vite does: minifies code, splits it into chunks, adds a hash to file names (for caching), and removes unused code (tree shaking).

**Interview Angle**
- Asked in interviews? **Often**
- Remember: folder name is `dist` (in Vite). In Create React App it was `build`.
- Use `npm run preview` to test before you deploy.

---

## 252. Environment-Based Configuration

**Simple Meaning**
Your app needs different settings in different places: local, testing, and live. Keep them in separate `.env` files.

**Code**
```bash
# .env.development
VITE_API_URL=http://localhost:5000

# .env.production
VITE_API_URL=https://api.myapp.com
```
```js
const apiUrl = import.meta.env.VITE_API_URL;
```
Vite picks the right file by itself: `npm run dev` uses development, `npm run build` uses production.

**Interview Angle**
- Asked in interviews? **Often**
- Add `.env` files with private values to `.gitignore`.
- Remember the `VITE_` prefix.

---

## 253. Deploying React Applications

**Simple Meaning**
Deploying means putting your app on the internet so anyone can open it. A React app (after build) is just static files (HTML, CSS, JS), so you can host it almost anywhere.

Steps:
1. Run `npm run build`.
2. Upload the `dist` folder to a host.
3. The host gives you a link.

Popular hosts: Vercel, Netlify, GitHub Pages, Firebase Hosting, Cloudflare Pages.

**Interview Angle**
- Asked in interviews? **Often**
- Say: "I build the app and host the static files, usually on Vercel or Netlify."

---

## 254. Vercel and Netlify Deployment Basics

**Simple Meaning**
Both services connect to your GitHub. Every time you push code, they build and publish your site automatically.

**Steps (same idea for both)**
1. Push your project to GitHub.
2. Sign in to Vercel or Netlify, and click "Add new project".
3. Pick your repository.
4. Settings (usually detected automatically for Vite):
   - Build command: `npm run build`
   - Output folder: `dist`
5. Add environment variables in their dashboard.
6. Click Deploy.

**Good things:** free plan, automatic HTTPS, preview links for each branch, easy rollback.

**Interview Angle**
- Asked in interviews? **Sometimes**
- Know the two settings: **build command** and **output directory**.
- Environment variables are added in their dashboard, not in the Git repo.

---

## 255. Client-Side Routing on Deployment

**Simple Meaning**
In React Router, pages like `/about` do not exist as real files. React creates them in the browser. If a user refreshes on `/about`, the server looks for an `about` file, finds nothing, and shows **404**.

**Fix:** tell the host to always send `index.html` for every URL, so React Router can take over.

**Code**
```json
// vercel.json
{
  "rewrites": [{ "source": "/(.*)", "destination": "/index.html" }]
}
```
```
# Netlify: public/_redirects
/*    /index.html   200
```

**Interview Angle**
- Asked in interviews? **Very often**
- Classic question: "Why do I get 404 when I refresh my React app on a deployed site?" The answer above.

---

## 256. Handling Build Errors

**Simple Meaning**
Sometimes the app works with `npm run dev` but fails on `npm run build`. Common reasons and fixes:

| Problem | Fix |
|---|---|
| Wrong file name case (`Header.jsx` vs `header.jsx`) | Match the exact case. Linux servers care, Windows does not. |
| Missing package | `npm install` the package |
| Unused variable/import treated as error | Remove it |
| Env variable missing | Add it in the host dashboard |
| Wrong Node version | Set the same Node version on the host |
| Type errors (TypeScript) | Fix the types |

**Tip:** read the **first** error message in the log. Later errors are often caused by the first one.

**Interview Angle**
- Asked in interviews? **Sometimes**
- Famous: "Works on my machine, fails on the server" is often a **file-name case** or **missing env variable** problem.

---

## 257. Debugging Production Issues

**Simple Meaning**
When a bug shows up on the live site, you cannot use your normal dev tools easily, since the code is squeezed.

Ways to debug:
- Open the browser **Console** and **Network** tabs. Look for red errors and failed requests.
- Use **source maps** (files that link squeezed code back to your real code).
- Use error tracking tools like Sentry.
- Check if an env variable is wrong or missing.
- Reproduce locally with `npm run build` + `npm run preview`.
- Roll back to the last good version if it is serious.

**Interview Angle**
- Asked in interviews? **Often**
- Good answer shows steps: "Check console and network, reproduce locally using a production build, use error monitoring, and rollback if urgent."

---

## 258. Environment Variable Security

**Simple Meaning**
Anything you put in a React environment variable **ends up inside the JavaScript file**, and anyone can read it. So `.env` in React is **not secret**.

**Rules**
- Never put passwords, private API keys, or database links in `VITE_` variables.
- Keep real secrets on a backend server.
- Do not commit `.env` files to GitHub (add to `.gitignore`).
- If a secret leaked by mistake, **change it** right away.

**Code**
```bash
# .gitignore
.env
.env.local
```

**Interview Angle**
- Asked in interviews? **Very often**
- Common wrong belief: "`.env` makes my key safe." In frontend code, it does not.
- Right answer: "Call a secret API through my own backend, which holds the key."

---

## 259. Frontend Logging and Error Monitoring

**Simple Meaning**
Once real users use your app, you cannot see their screens. Error monitoring tools **automatically collect errors** from users' browsers and send them to you, with details like what the user did before the crash.

Popular tools: Sentry, LogRocket, Datadog.

**Code**
```bash
npm install @sentry/react
```
```jsx
import * as Sentry from "@sentry/react";

Sentry.init({ dsn: "your-sentry-dsn", environment: "production" });

// Report an error by hand
try {
  doSomething();
} catch (err) {
  Sentry.captureException(err);
}
```
Pair this with an Error Boundary so crashes are reported too.

**Interview Angle**
- Asked in interviews? **Sometimes**
- Do not log passwords or personal data.
- Remove noisy `console.log` before production.

---

## 260. Basic SEO Considerations for React Apps

**Simple Meaning**
SEO means helping search engines (like Google) find and understand your pages. A normal React app (CSR) sends an almost empty HTML page, which can make SEO harder.

What helps:
- Give each page its own **title** and **description** (use `react-helmet-async`, or use Next.js).
- Use **semantic HTML** and proper headings.
- Add `alt` text on images.
- Use real links (`<a>` or `<Link>`) so crawlers can follow them.
- For SEO-heavy sites (blogs, shops), use **SSR or SSG** (like Next.js).
- Make the site fast (Core Web Vitals).

**Code**
```jsx
import { Helmet } from "react-helmet-async";

function About() {
  return (
    <>
      <Helmet>
        <title>About Us | MyApp</title>
        <meta name="description" content="Learn about our team." />
      </Helmet>
      <h1>About Us</h1>
    </>
  );
}
```

**Interview Angle**
- Asked in interviews? **Often**
- Good answer: "Plain React is weaker for SEO because content loads with JavaScript. For SEO-heavy sites I use Next.js with SSR or SSG."

---

# Level 15: React Interview Questions and Practical Problems

> For this level, each topic is written as a **question with a ready answer**. Read the "Say this in interview" line, then understand the rest.

## 261. Props vs State

**Simple Meaning**
- **Props**: data a component **receives** from its parent. Read-only. The component cannot change them.
- **State**: data a component **owns and manages itself**. It can change, and when it changes, the screen updates.

**Say this in interview:** "Props come from outside and cannot be changed by the component. State lives inside the component and can change."

**Code**
```jsx
function Greeting({ name }) {          // name is a prop
  const [count, setCount] = useState(0); // count is state
  return (
    <button onClick={() => setCount(count + 1)}>
      {name} clicked {count} times
    </button>
  );
}
<Greeting name="Ravi" />
```

**Interview Angle**
- Asked in interviews? **Very often** (almost always the first question)
- Confusion: a child can show a prop, but never change it. To change it, the parent must change it (the parent passes down a function).

---

## 262. Why React Uses a Virtual DOM

**Simple Meaning**
The real DOM (the page in the browser) is slow to change. The Virtual DOM is a **light copy of the page kept in memory** (just JavaScript objects). When something changes, React:
1. Makes a new virtual copy.
2. Compares it with the old copy (called "diffing").
3. Updates **only the parts that changed** in the real page.

This is faster than rebuilding the whole page.

**Say this in interview:** "Virtual DOM is a light copy of the real DOM. React compares old and new copies and updates only what changed."

**Interview Angle**
- Asked in interviews? **Very often**
- Confusion: Virtual DOM is not always "faster than the real DOM". It is a smart way to avoid unnecessary changes and keep code simple.

---

## 263. Why React Components Re-render

**Simple Meaning**
A component re-renders (runs again) when:
1. Its **state** changes.
2. Its **props** change (or its parent re-renders).
3. A **context** it uses changes.

**Say this in interview:** "A component re-renders when its state changes, when its parent re-renders, or when a context it uses changes."

**Code**
```jsx
function Parent() {
  const [n, setN] = useState(0);
  return (
    <>
      <button onClick={() => setN(n + 1)}>+</button>
      <Child /> {/* re-renders too, because the parent did */}
    </>
  );
}
```

**Interview Angle**
- Asked in interviews? **Very often**
- Common wrong answer: "Only when props change." Not true. When the parent re-renders, all children re-render unless wrapped in `React.memo`.
- Also: setting state to the **same** value usually does not cause a re-render.

---

## 264. Why Keys Are Important

**Simple Meaning**
When you show a list, React needs a way to tell each item apart. The `key` is like an **ID card** for each item. With keys, React knows which item was added, removed or moved, and updates only that.

**Say this in interview:** "Keys help React identify list items so it updates the right ones correctly and quickly."

**Code**
```jsx
// Good: unique, stable id
{todos.map((todo) => <li key={todo.id}>{todo.text}</li>)}

// Risky: index as key (when the list can be reordered or deleted from)
{todos.map((todo, index) => <li key={index}>{todo.text}</li>)}
```

**Interview Angle**
- Asked in interviews? **Very often**
- Problem with index keys: if you delete the first item, all the indexes shift, and React may show wrong data (especially inputs inside the list).
- Index is fine only if the list never changes order and never gets added or removed items.
- Keys must be unique **among siblings**, not across the whole app. Never use `Math.random()` as a key.

---

## 265. Controlled vs Uncontrolled Components

**Simple Meaning**
- **Controlled**: React state controls the input value (`value` + `onChange`).
- **Uncontrolled**: the browser holds the value, and you read it with a `ref` when needed.

**Say this in interview:** "In a controlled component, React state is the single source of truth. In an uncontrolled one, the DOM holds the value."

**Code**
```jsx
// Controlled
<input value={name} onChange={(e) => setName(e.target.value)} />

// Uncontrolled
<input ref={inputRef} defaultValue="Ravi" />
```

**Interview Angle**
- Asked in interviews? **Very often**
- Use controlled when you need live validation or to change the value from code. Use uncontrolled for simple forms and file inputs.

---

## 266. useState Update Behavior

**Simple Meaning**
Two important facts:
1. State updates are **not instant**. The new value is available in the **next render**.
2. Several updates are **batched** (grouped) into one render.

If the new value depends on the old value, use the **function form**.

**Code**
```jsx
const [count, setCount] = useState(0);

function handleClick() {
  setCount(count + 1);
  setCount(count + 1);
  setCount(count + 1);
  // Result: count becomes 1, not 3
  // because "count" is 0 in all three lines
}

function handleClickCorrect() {
  setCount((c) => c + 1);
  setCount((c) => c + 1);
  setCount((c) => c + 1);
  // Result: count becomes 3
}

function showOld() {
  setCount(5);
  console.log(count); // still the OLD value, not 5
}
```

**Interview Angle**
- Asked in interviews? **Very often** (output-based question)
- Remember: use `setCount(c => c + 1)` when the new value depends on the old.
- Objects and arrays: always make a **new copy** (`{...obj}`, `[...arr]`). Changing them directly will not update the screen.

---

## 267. useEffect Dependency Array Questions

**Simple Meaning**
The second argument of `useEffect` controls **when** it runs.

| Written as | Runs when |
|---|---|
| `useEffect(fn)` | After **every** render |
| `useEffect(fn, [])` | **Only once**, after the first render |
| `useEffect(fn, [a, b])` | First render, and whenever `a` or `b` changes |

**Code**
```jsx
useEffect(() => { console.log("every render"); });
useEffect(() => { console.log("only once"); }, []);
useEffect(() => { console.log("when id changes"); }, [id]);
```

**Interview Angle**
- Asked in interviews? **Very often**
- Rule: put **every** outside value that the effect uses (props, state) into the array. Skipping some gives old (stale) values.
- Objects, arrays and functions created inside the component are **new every render**, so putting them in the array makes the effect run every time.

---

## 268. useEffect Cleanup Questions

**Simple Meaning**
The function you **return** from `useEffect` is the cleanup. React runs it:
1. Before the effect runs again.
2. When the component is removed from the screen.

Use it to stop things you started: timers, event listeners, subscriptions, API requests.

**Code**
```jsx
useEffect(() => {
  const timer = setInterval(() => console.log("tick"), 1000);

  return () => clearInterval(timer); // cleanup: stop the timer
}, []);

useEffect(() => {
  function onResize() { console.log(window.innerWidth); }
  window.addEventListener("resize", onResize);

  return () => window.removeEventListener("resize", onResize);
}, []);
```

**Interview Angle**
- Asked in interviews? **Very often**
- Without cleanup, you get **memory leaks** and bugs like timers that keep running after the component is gone.
- In development Strict Mode, React runs "effect, cleanup, effect" once to check your cleanup is correct.

---

## 269. useRef vs useState

**Simple Meaning**
Both remember a value between renders. The big difference:
- Changing **state** causes a **re-render**.
- Changing a **ref** does **not** cause a re-render.

Use `useState` for things shown on screen. Use `useRef` for things you only need to remember quietly (timer id, previous value, a link to a DOM element).

**Code**
```jsx
function Example() {
  const [count, setCount] = useState(0);   // screen updates on change
  const clicks = useRef(0);                // screen does NOT update
  const inputRef = useRef();               // link to an input element

  return (
    <>
      <p>{count}</p>
      <button onClick={() => { setCount(count + 1); clicks.current += 1; }}>Add</button>
      <input ref={inputRef} />
      <button onClick={() => inputRef.current.focus()}>Focus</button>
    </>
  );
}
```

**Interview Angle**
- Asked in interviews? **Very often**
- Value lives in `ref.current`.
- Do not read or write `ref.current` during rendering. Do it in event handlers or effects.

---

## 270. useMemo vs useCallback

**Simple Meaning**
- `useMemo` remembers a **value** (result of a calculation).
- `useCallback` remembers a **function**.

**Say this in interview:** "useMemo caches a calculated value. useCallback caches a function so it keeps the same reference between renders."

**Code**
```jsx
const total = useMemo(() => items.reduce((s, i) => s + i.price, 0), [items]);

const handleClick = useCallback(() => {
  console.log("clicked");
}, []);
```

**Interview Angle**
- Asked in interviews? **Very often**
- Add: they only help when combined with `React.memo`, or when the value is in another hook's dependency array, or the calculation is heavy.
- Do not overuse them.

---

## 271. React.memo and Memoization

**Simple Meaning**
`React.memo` skips re-rendering a component if its props did not change. Memoization = remembering the last result.

**Code**
```jsx
const Card = React.memo(function Card({ title }) {
  console.log("Card rendered");
  return <h3>{title}</h3>;
});
```

**Interview Angle**
- Asked in interviews? **Very often**
- Why it sometimes does not work: you pass a new object, array or function each render. Fix with `useMemo` / `useCallback`.
- It only compares props shallowly. State changes inside the component still re-render it.

---

## 272. Stale Closures in React

**Simple Meaning**
A closure is when a function "remembers" the variables around it at the time it was created. A **stale closure** happens when a function remembers an **old value** of state, because it was created in an earlier render and never got updated.

**Code**
```jsx
function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    const id = setInterval(() => {
      console.log(count);       // always prints 0 (stale!)
      setCount(count + 1);      // always sets 1
    }, 1000);
    return () => clearInterval(id);
  }, []);                        // count missing from the array

  return <p>{count}</p>;
}
```
Fix 1: use the function form of setState.
```jsx
setCount((c) => c + 1);   // always uses the latest value
```
Fix 2: add `count` to the dependency array (the effect re-runs each time).
Fix 3: store the latest value in a `ref`.

**Interview Angle**
- Asked in interviews? **Very often** (a favourite tricky question)
- Typical cause: empty `[]` dependency array, with timers or event listeners.
- Best quick fix: `setState(prev => ...)`.

---

## 273. Infinite Re-render and Effect Loop Questions

**Simple Meaning**
An infinite loop happens when a component keeps updating itself forever.

**Common causes and fixes**
```jsx
// 1. Setting state directly while rendering
function Bad() {
  const [n, setN] = useState(0);
  setN(n + 1);         // loop! runs on every render
  return <p>{n}</p>;
}

// 2. Calling the function instead of passing it
<button onClick={setCount(count + 1)}>Add</button>     // loop! runs immediately
<button onClick={() => setCount(count + 1)}>Add</button> // correct

// 3. Effect that sets state, with no dependency array
useEffect(() => {
  setData([1, 2, 3]);
});                        // loop! runs after every render
useEffect(() => {
  setData([1, 2, 3]);
}, []);                    // correct

// 4. An object/array in the dependency array
const options = { a: 1 };            // new object every render
useEffect(() => { fetchData(options); }, [options]);   // loop-like behavior
```

**Interview Angle**
- Asked in interviews? **Very often**
- Look for: state set during render, `onClick={fn()}`, missing `[]`, objects in dependency arrays.

---

## 274. Context API vs Redux

**Simple Meaning**
Context is a built-in way to share data without passing props. Redux is a separate library that manages big, shared data with strict rules and strong tools.

| | Context | Redux |
|---|---|---|
| Built in | Yes | No |
| Best for | Theme, user, language | Large, complex data |
| Dev tools | Few | Excellent |
| Extra setup | Little | More |
| Re-render control | Weak | Strong |

**Say this in interview:** "Context is for passing data down easily. Redux is a full state management tool for large apps. They are not the same thing, and Context does not fully replace Redux."

**Interview Angle**
- Asked in interviews? **Very often**
- See topic 173 for more.

---

## 275. Lifting State Up

**Simple Meaning**
When two components need the same data, move the state to their **closest common parent**. The parent holds the data and passes it down as props, with functions to change it.

**Code**
```jsx
function Parent() {
  const [text, setText] = useState("");   // state lives in the parent

  return (
    <>
      <Input text={text} onTextChange={setText} />
      <Preview text={text} />
    </>
  );
}

function Input({ text, onTextChange }) {
  return <input value={text} onChange={(e) => onTextChange(e.target.value)} />;
}

function Preview({ text }) {
  return <p>You typed: {text}</p>;
}
```

**Interview Angle**
- Asked in interviews? **Very often**
- Say: "Siblings cannot talk directly, so I put the state in the parent."

---

## 276. Reconciliation and Stable Keys

**Simple Meaning**
Reconciliation is the process React uses to **compare the old tree with the new tree** and decide the smallest changes needed.

Two simple rules React uses:
1. If an element's **type** changes (like `div` to `span`), React throws away the old one and builds a new one.
2. In lists, React uses **keys** to match old and new items.

A **stable key** is one that stays the same for the same item every time (like a database id).

**Code**
```jsx
// Changing the key makes React treat it as a brand new component (resets its state)
<Profile key={userId} userId={userId} />
```

**Interview Angle**
- Asked in interviews? **Often**
- Trick to remember: changing a component's `key` **resets its state**.
- Never define components inside other components. They are re-created on every render, and lose their state.

---

## 277. Component Lifecycle Questions

**Simple Meaning**
A component has three stages:
1. **Mount**: appears on screen for the first time.
2. **Update**: re-renders because state or props changed.
3. **Unmount**: removed from the screen.

In function components, `useEffect` covers all three.

**Code**
```jsx
useEffect(() => {
  console.log("Mounted");               // runs once at mount
  return () => console.log("Unmounted"); // runs at unmount
}, []);

useEffect(() => {
  console.log("Updated: count changed"); // runs on mount and when count changes
}, [count]);
```

| Class component | Function component |
|---|---|
| componentDidMount | `useEffect(fn, [])` |
| componentDidUpdate | `useEffect(fn, [dep])` |
| componentWillUnmount | cleanup function in `useEffect` |

**Interview Angle**
- Asked in interviews? **Very often**
- Do not think of `useEffect` as lifecycle methods exactly. It is better to think "run this when these values change".

---

## 278. How to Optimize a Slow React App

**Simple Meaning**
Do it step by step:
1. **Measure first** (React Profiler, Lighthouse).
2. Stop unneeded re-renders: `React.memo`, `useMemo`, `useCallback`.
3. Keep state close to where it is used. Do not put everything at the top.
4. Use **code splitting** and `lazy` for pages.
5. Use **virtualization** for long lists.
6. **Debounce** search and fast events.
7. Optimize images (WebP, lazy loading).
8. Use `useTransition` / `useDeferredValue` for heavy updates.
9. Use proper `key` values.
10. Cache API data (React Query).

**Say this in interview:** "First I measure to find the real problem. Then I fix that one: stop extra re-renders, split code, virtualize long lists, and optimize images."

**Interview Angle**
- Asked in interviews? **Very often**
- Mistake: jumping to `useMemo` everywhere without measuring.

---

## 279. How to Fetch Data and Handle Errors

**Simple Meaning**
Use `useEffect` to fetch, and keep three states: `data`, `loading`, `error`. Always check `res.ok`, use `try/catch`, and clean up (abort) when needed.

**Code**
```jsx
function Posts() {
  const [posts, setPosts] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const controller = new AbortController();

    async function load() {
      try {
        const res = await fetch("https://jsonplaceholder.typicode.com/posts", {
          signal: controller.signal,
        });
        if (!res.ok) throw new Error("Request failed: " + res.status);
        setPosts(await res.json());
      } catch (err) {
        if (err.name !== "AbortError") setError(err.message);
      } finally {
        setLoading(false);
      }
    }

    load();
    return () => controller.abort();
  }, []);

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error}</p>;
  if (posts.length === 0) return <p>No posts</p>;
  return <ul>{posts.map((p) => <li key={p.id}>{p.title}</li>)}</ul>;
}
```

**Interview Angle**
- Asked in interviews? **Very often** (coding round)
- Points to mention: loading, error, empty state, `res.ok`, cleanup. In real projects, mention React Query.

---

## 280. How to Structure a React Project

**Simple Meaning**
A clean structure makes a project easy to understand and grow. A common beginner-friendly layout:

```
src/
  assets/        images, fonts
  components/    small reusable parts (Button, Modal, Navbar)
  pages/         one file per page (Home, Login, Dashboard)
  hooks/         custom hooks (useFetch, useDebounce)
  context/       context providers (AuthContext)
  services/      API call files
  utils/         helper functions (formatDate)
  routes/        route setup, ProtectedRoute
  App.jsx
  main.jsx
```

For bigger apps, group **by feature**:
```
src/features/
  auth/        (components, hooks, api, slice)
  products/
  cart/
```

**Tips**
- One component per file, file name matches the component.
- Keep components small and focused.
- Keep API code out of components.

**Interview Angle**
- Asked in interviews? **Often**
- No single right answer. Explain your reason: "I separate reusable UI, pages, API code, and helpers so each file has one job."

---

## 281. Debugging React Code

**Simple Meaning**
Steps to find bugs:
1. **Read the error message** in the console. It tells the file and line.
2. Use `console.log` to see values.
3. Use **React DevTools** to check props and state.
4. Use the **Network tab** for API problems.
5. Use `debugger` or breakpoints in the Sources tab.
6. Make the problem **smaller**: comment out parts until the bug disappears.
7. Check common mistakes (below).

**Common mistakes**
- Changing state directly (`arr.push()`).
- Missing `key` in lists.
- Wrong dependency array.
- Calling a function instead of passing it (`onClick={fn()}`).
- Forgetting to return JSX or a closing tag.
- Wrong import (default vs named).

**Interview Angle**
- Asked in interviews? **Often**
- Interviewers like to hear a **method**, not just "console.log".

---

## 282. React Output-Based Questions

**Simple Meaning**
Interviewers show code and ask "What will be printed?" or "What will the screen show?". They test your understanding of state, effects and rendering.

**Question 1**
```jsx
function App() {
  const [count, setCount] = useState(0);
  function handle() {
    setCount(count + 1);
    setCount(count + 1);
  }
  return <button onClick={handle}>{count}</button>;
}
```
**Answer:** After one click, it shows **1**. Both lines use `count = 0`.

**Question 2**
```jsx
function App() {
  const [count, setCount] = useState(0);
  function handle() {
    setCount(count + 1);
    console.log(count);
  }
  return <button onClick={handle}>{count}</button>;
}
```
**Answer:** The console shows **0** on the first click (old value). The screen then shows 1.

**Question 3**
```jsx
useEffect(() => {
  console.log("A");
  return () => console.log("B");
}, [count]);
```
**Answer:** On mount: A. When `count` changes: **B, then A** (cleanup first). On unmount: B.

**Question 4**
```jsx
console.log("1");
setTimeout(() => console.log("2"), 0);
Promise.resolve().then(() => console.log("3"));
console.log("4");
```
**Answer:** 1, 4, 3, 2. (Normal code first, then promises, then timers.)

**Question 5**
```jsx
const [list, setList] = useState([1, 2, 3]);
function add() {
  list.push(4);
  setList(list);
}
```
**Answer:** The screen **does not update**. It is the same array (same reference), so React sees no change. Use `setList([...list, 4])`.

**Interview Angle**
- Asked in interviews? **Very often**
- Think about: when the value is read, whether state is old or new, and whether the reference changed.

---

## 283. React Coding Round Practice

**Simple Meaning**
These are the tasks most often given live. Practise each one until you can write it without help.

**Common tasks**
1. Counter with increment, decrement, reset.
2. Todo list (add, delete, mark done).
3. Toggle (show/hide, dark mode).
4. Fetch and show a list from an API (with loading and error).
5. Search/filter a list.
6. Debounced search input.
7. Tabs and accordion.
8. Form with validation.
9. Pagination.
10. Modal.
11. Star rating.
12. Timer / stopwatch.
13. Custom hook (`useFetch`, `useDebounce`, `useLocalStorage`).
14. Infinite scroll.

**Sample: a quick custom hook**
```jsx
function useDebounce(value, delay = 500) {
  const [debounced, setDebounced] = useState(value);

  useEffect(() => {
    const timer = setTimeout(() => setDebounced(value), delay);
    return () => clearTimeout(timer);
  }, [value, delay]);

  return debounced;
}
```

**Tips for the round**
- Talk while coding. Say what you are doing and why.
- Start simple, get it working, then improve.
- Handle loading, error, and empty states.
- Use meaningful names and proper `key` values.
- If stuck, explain your thinking out loud.

**Interview Angle**
- Asked in interviews? **Very often**

---

# Level 16: Practical React Projects

> For each project you get: **What you build**, **What you learn**, **Starter code** (short and working), and **Interview Angle**. Type the code yourself, then try to add the "Try next" ideas.

## 284. Counter Application

**What you build**
A number with buttons to add, subtract and reset.

**What you learn:** `useState`, event handlers, function form of setState.

**Code**
```jsx
import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>{count}</h1>
      <button onClick={() => setCount((c) => c - 1)}>-</button>
      <button onClick={() => setCount(0)}>Reset</button>
      <button onClick={() => setCount((c) => c + 1)}>+</button>
    </div>
  );
}
```

**Try next:** do not allow numbers below 0, add a step size input.

**Interview Angle**
- Asked in interviews? **Very often** (warm-up task)
- Interviewers watch: do you use `setCount(c => c + 1)`? Do you handle edge cases?

---

## 285. Todo App with CRUD Operations

**What you build**
A list where you can **C**reate, **R**ead, **U**pdate and **D**elete tasks.

**What you learn:** state with arrays, `map`, `filter`, keys, controlled inputs.

**Code**
```jsx
import { useState } from "react";

export default function Todo() {
  const [text, setText] = useState("");
  const [todos, setTodos] = useState([]);
  const [editId, setEditId] = useState(null);

  function handleSubmit(e) {
    e.preventDefault();
    if (!text.trim()) return;

    if (editId) {
      // Update
      setTodos(todos.map((t) => (t.id === editId ? { ...t, text } : t)));
      setEditId(null);
    } else {
      // Create
      setTodos([...todos, { id: Date.now(), text, done: false }]);
    }
    setText("");
  }

  function toggle(id) {
    setTodos(todos.map((t) => (t.id === id ? { ...t, done: !t.done } : t)));
  }

  function remove(id) {
    setTodos(todos.filter((t) => t.id !== id)); // Delete
  }

  function startEdit(todo) {
    setEditId(todo.id);
    setText(todo.text);
  }

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <input value={text} onChange={(e) => setText(e.target.value)} />
        <button>{editId ? "Update" : "Add"}</button>
      </form>

      {todos.length === 0 && <p>No tasks yet</p>}

      <ul>
        {todos.map((t) => (
          <li key={t.id}>
            <span
              onClick={() => toggle(t.id)}
              style={{ textDecoration: t.done ? "line-through" : "none", cursor: "pointer" }}
            >
              {t.text}
            </span>
            <button onClick={() => startEdit(t)}>Edit</button>
            <button onClick={() => remove(t.id)}>Delete</button>
          </li>
        ))}
      </ul>
    </div>
  );
}
```

**Try next:** save todos in localStorage, add filters (All / Done / Pending).

**Interview Angle**
- Asked in interviews? **Very often**
- Key points: never change state directly (`push`), use `filter` for delete, `map` for update, unique ids as keys.

---

## 286. Searchable and Filterable List

**What you build**
A list with a search box and a category dropdown.

**What you learn:** derived data (calculating from state instead of storing a copy), `filter`.

**Code**
```jsx
import { useState } from "react";

const products = [
  { id: 1, name: "Red Shirt", category: "clothes" },
  { id: 2, name: "Blue Jeans", category: "clothes" },
  { id: 3, name: "Laptop", category: "tech" },
  { id: 4, name: "Phone", category: "tech" },
];

export default function ProductList() {
  const [search, setSearch] = useState("");
  const [category, setCategory] = useState("all");

  const visible = products.filter(
    (p) =>
      p.name.toLowerCase().includes(search.toLowerCase()) &&
      (category === "all" || p.category === category)
  );

  return (
    <div>
      <input placeholder="Search..." value={search} onChange={(e) => setSearch(e.target.value)} />
      <select value={category} onChange={(e) => setCategory(e.target.value)}>
        <option value="all">All</option>
        <option value="clothes">Clothes</option>
        <option value="tech">Tech</option>
      </select>

      {visible.length === 0 ? (
        <p>No results</p>
      ) : (
        <ul>{visible.map((p) => <li key={p.id}>{p.name}</li>)}</ul>
      )}
    </div>
  );
}
```

**Interview Angle**
- Asked in interviews? **Very often**
- Point to say: "I don't store the filtered list in state. I calculate it from the original list and the search values."

---

## 287. Tabs and Accordion Components

**What you build**
- **Tabs**: click a heading to see its content.
- **Accordion**: click a title to open or close a section.

**What you learn:** conditional rendering, which item is "active", reusable components.

**Code**
```jsx
import { useState } from "react";

export function Tabs({ tabs }) {
  const [active, setActive] = useState(0);
  return (
    <div>
      <div role="tablist">
        {tabs.map((t, i) => (
          <button
            key={t.title}
            role="tab"
            aria-selected={active === i}
            onClick={() => setActive(i)}
            style={{ fontWeight: active === i ? "bold" : "normal" }}
          >
            {t.title}
          </button>
        ))}
      </div>
      <div role="tabpanel">{tabs[active].content}</div>
    </div>
  );
}

export function Accordion({ items }) {
  const [openIndex, setOpenIndex] = useState(null);
  return (
    <div>
      {items.map((item, i) => (
        <div key={item.title}>
          <button
            aria-expanded={openIndex === i}
            onClick={() => setOpenIndex(openIndex === i ? null : i)}
          >
            {item.title}
          </button>
          {openIndex === i && <p>{item.content}</p>}
        </div>
      ))}
    </div>
  );
}
```
Use it:
```jsx
<Tabs tabs={[{ title: "One", content: "First" }, { title: "Two", content: "Second" }]} />
<Accordion items={[{ title: "What is React?", content: "A UI library." }]} />
```

**Try next:** allow many accordion items open at once, add keyboard arrow keys.

**Interview Angle**
- Asked in interviews? **Very often**
- Keep **only the active index** in state. Show how you made it reusable with props.

---

## 288. Reusable Modal Component

**What you build**
A popup that can show any content, closes with a button, the Esc key, or by clicking outside.

**What you learn:** props, `children`, `useEffect` cleanup, accessibility, portals.

**Code**
```jsx
import { useEffect } from "react";
import { createPortal } from "react-dom";

export default function Modal({ open, onClose, title, children }) {
  useEffect(() => {
    if (!open) return;
    const onKey = (e) => e.key === "Escape" && onClose();
    document.addEventListener("keydown", onKey);
    return () => document.removeEventListener("keydown", onKey);
  }, [open, onClose]);

  if (!open) return null;

  return createPortal(
    <div
      onClick={onClose}
      style={{ position: "fixed", inset: 0, background: "rgba(0,0,0,0.5)", display: "grid", placeItems: "center" }}
    >
      <div
        role="dialog"
        aria-modal="true"
        aria-label={title}
        onClick={(e) => e.stopPropagation()}  // clicking inside should not close
        style={{ background: "white", padding: 20, borderRadius: 8 }}
      >
        <h2>{title}</h2>
        {children}
        <button onClick={onClose}>Close</button>
      </div>
    </div>,
    document.body
  );
}
```
Use it:
```jsx
const [open, setOpen] = useState(false);
<button onClick={() => setOpen(true)}>Open</button>
<Modal open={open} onClose={() => setOpen(false)} title="Hello">
  <p>Modal content</p>
</Modal>
```

**Interview Angle**
- Asked in interviews? **Very often**
- Points to mention: `createPortal` (render outside the parent), `stopPropagation`, Esc key with cleanup, accessibility roles, focus handling.

---

## 289. Form with Validation

**What you build**
A signup form that checks the fields and shows errors.

**What you learn:** controlled inputs, one object for form state, validation function, submit handling.

**Code**
```jsx
import { useState } from "react";

export default function SignupForm() {
  const [form, setForm] = useState({ name: "", email: "", password: "" });
  const [errors, setErrors] = useState({});
  const [success, setSuccess] = useState(false);

  function handleChange(e) {
    setForm({ ...form, [e.target.name]: e.target.value });
  }

  function validate() {
    const e = {};
    if (!form.name.trim()) e.name = "Name is required";
    if (!/\S+@\S+\.\S+/.test(form.email)) e.email = "Enter a valid email";
    if (form.password.length < 6) e.password = "Password needs 6+ characters";
    return e;
  }

  function handleSubmit(e) {
    e.preventDefault();
    const newErrors = validate();
    setErrors(newErrors);
    if (Object.keys(newErrors).length === 0) {
      setSuccess(true);
      setForm({ name: "", email: "", password: "" });
    }
  }

  return (
    <form onSubmit={handleSubmit} noValidate>
      <label htmlFor="name">Name</label>
      <input id="name" name="name" value={form.name} onChange={handleChange} />
      {errors.name && <p role="alert">{errors.name}</p>}

      <label htmlFor="email">Email</label>
      <input id="email" name="email" value={form.email} onChange={handleChange} />
      {errors.email && <p role="alert">{errors.email}</p>}

      <label htmlFor="password">Password</label>
      <input id="password" name="password" type="password" value={form.password} onChange={handleChange} />
      {errors.password && <p role="alert">{errors.password}</p>}

      <button type="submit">Sign up</button>
      {success && <p>Signup successful!</p>}
    </form>
  );
}
```

**Try next:** rebuild it with React Hook Form + Zod.

**Interview Angle**
- Asked in interviews? **Very often**
- Mention: `preventDefault`, labels, `[e.target.name]` trick, validation function, and that the server must validate again.

---

## 290. Weather App Using an API

**What you build**
Type a city and see its current temperature and weather.

**What you learn:** API calls, loading/error states, handling user input, env variables.

We use **Open-Meteo**, which is free and needs no API key. It has two steps: find the city's location, then get the weather.

**Code**
```jsx
import { useState } from "react";

export default function Weather() {
  const [city, setCity] = useState("");
  const [weather, setWeather] = useState(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState("");

  async function handleSearch(e) {
    e.preventDefault();
    if (!city.trim()) return;

    setLoading(true);
    setError("");
    setWeather(null);

    try {
      // Step 1: city name -> latitude and longitude
      const geoRes = await fetch(
        `https://geocoding-api.open-meteo.com/v1/search?name=${encodeURIComponent(city)}&count=1`
      );
      const geo = await geoRes.json();
      if (!geo.results) throw new Error("City not found");

      const { latitude, longitude, name } = geo.results[0];

      // Step 2: get the weather
      const wRes = await fetch(
        `https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}&current_weather=true`
      );
      if (!wRes.ok) throw new Error("Could not load weather");
      const data = await wRes.json();

      setWeather({ name, ...data.current_weather });
    } catch (err) {
      setError(err.message);
    } finally {
      setLoading(false);
    }
  }

  return (
    <div>
      <form onSubmit={handleSearch}>
        <input value={city} onChange={(e) => setCity(e.target.value)} placeholder="Enter city" />
        <button>Search</button>
      </form>

      {loading && <p>Loading...</p>}
      {error && <p role="alert">{error}</p>}
      {weather && (
        <div>
          <h2>{weather.name}</h2>
          <p>Temperature: {weather.temperature} °C</p>
          <p>Wind: {weather.windspeed} km/h</p>
        </div>
      )}
    </div>
  );
}
```

**Try next:** show a 5-day forecast, remember the last city, add a °C/°F switch.

**Interview Angle**
- Asked in interviews? **Very often**
- Mention: loading and error states, `encodeURIComponent` for the city name, `try/catch/finally`, and keeping API URLs in env variables (if the API needs a key, use a backend).

---

## 291. Product Listing with Search, Filters and Sorting

**What you build**
A product page that can search, filter by category, and sort by price.

**What you learn:** combining several controls, derived data, API fetch.

**Code**
```jsx
import { useEffect, useMemo, useState } from "react";

export default function Products() {
  const [products, setProducts] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState("");
  const [search, setSearch] = useState("");
  const [category, setCategory] = useState("all");
  const [sort, setSort] = useState("none");

  useEffect(() => {
    fetch("https://fakestoreapi.com/products")
      .then((res) => {
        if (!res.ok) throw new Error("Failed to load");
        return res.json();
      })
      .then(setProducts)
      .catch((e) => setError(e.message))
      .finally(() => setLoading(false));
  }, []);

  const categories = useMemo(
    () => ["all", ...new Set(products.map((p) => p.category))],
    [products]
  );

  const visible = useMemo(() => {
    let list = products.filter(
      (p) =>
        p.title.toLowerCase().includes(search.toLowerCase()) &&
        (category === "all" || p.category === category)
    );
    if (sort === "low") list = [...list].sort((a, b) => a.price - b.price);
    if (sort === "high") list = [...list].sort((a, b) => b.price - a.price);
    return list;
  }, [products, search, category, sort]);

  if (loading) return <p>Loading...</p>;
  if (error) return <p>{error}</p>;

  return (
    <div>
      <input placeholder="Search" value={search} onChange={(e) => setSearch(e.target.value)} />
      <select value={category} onChange={(e) => setCategory(e.target.value)}>
        {categories.map((c) => <option key={c}>{c}</option>)}
      </select>
      <select value={sort} onChange={(e) => setSort(e.target.value)}>
        <option value="none">Sort</option>
        <option value="low">Price: Low to High</option>
        <option value="high">Price: High to Low</option>
      </select>

      {visible.length === 0 && <p>No products found</p>}
      <div>
        {visible.map((p) => (
          <div key={p.id}>
            <img src={p.image} alt={p.title} width="80" />
            <p>{p.title}</p>
            <p>${p.price}</p>
          </div>
        ))}
      </div>
    </div>
  );
}
```

**Interview Angle**
- Asked in interviews? **Very often**
- Mention: copy the array before `sort`, derive instead of storing the filtered list, and explain why `useMemo` is used (or when it is not needed).

---

## 292. Pagination Component

**What you build**
A reusable component with Prev, Next and page numbers.

**What you learn:** math for slicing, props, disabled buttons.

**Code**
```jsx
import { useState } from "react";

function Pagination({ page, totalPages, onChange }) {
  const pages = Array.from({ length: totalPages }, (_, i) => i + 1);

  return (
    <nav aria-label="Pagination">
      <button disabled={page === 1} onClick={() => onChange(page - 1)}>Prev</button>
      {pages.map((p) => (
        <button
          key={p}
          onClick={() => onChange(p)}
          aria-current={p === page ? "page" : undefined}
          style={{ fontWeight: p === page ? "bold" : "normal" }}
        >
          {p}
        </button>
      ))}
      <button disabled={page === totalPages} onClick={() => onChange(page + 1)}>Next</button>
    </nav>
  );
}

export default function List() {
  const items = Array.from({ length: 53 }, (_, i) => `Item ${i + 1}`);
  const perPage = 10;
  const [page, setPage] = useState(1);

  const totalPages = Math.ceil(items.length / perPage);
  const start = (page - 1) * perPage;
  const current = items.slice(start, start + perPage);

  return (
    <div>
      <ul>{current.map((i) => <li key={i}>{i}</li>)}</ul>
      <Pagination page={page} totalPages={totalPages} onChange={setPage} />
    </div>
  );
}
```

**Try next:** show only a few page numbers with "..." for big lists; reset to page 1 when the search changes.

**Interview Angle**
- Asked in interviews? **Very often**
- Formula: `start = (page - 1) * perPage`, `totalPages = Math.ceil(total / perPage)`.
- Common bug: after filtering, the current page may no longer exist. Reset the page to 1.

---

## 293. Debounced Search Application

**What you build**
A search box that calls the API only after the user **stops typing** for a short time.

**What you learn:** custom hook, `setTimeout` cleanup, avoiding extra API calls, cancelling old requests.

**Code**
```jsx
import { useEffect, useState } from "react";

function useDebounce(value, delay = 500) {
  const [debounced, setDebounced] = useState(value);
  useEffect(() => {
    const timer = setTimeout(() => setDebounced(value), delay);
    return () => clearTimeout(timer);
  }, [value, delay]);
  return debounced;
}

export default function Search() {
  const [query, setQuery] = useState("");
  const [results, setResults] = useState([]);
  const [loading, setLoading] = useState(false);
  const debouncedQuery = useDebounce(query, 500);

  useEffect(() => {
    if (!debouncedQuery.trim()) {
      setResults([]);
      return;
    }

    const controller = new AbortController();
    setLoading(true);

    fetch(`https://dummyjson.com/products/search?q=${encodeURIComponent(debouncedQuery)}`, {
      signal: controller.signal,
    })
      .then((res) => res.json())
      .then((data) => {
        setResults(data.products);
        setLoading(false);
      })
      .catch((err) => {
        if (err.name !== "AbortError") setLoading(false);
      });

    return () => controller.abort(); // cancel the old request
  }, [debouncedQuery]);

  return (
    <div>
      <input value={query} onChange={(e) => setQuery(e.target.value)} placeholder="Search products" />
      {loading && <p>Searching...</p>}
      <ul>{results.map((p) => <li key={p.id}>{p.title}</li>)}</ul>
    </div>
  );
}
```

**Interview Angle**
- Asked in interviews? **Very often** (top favourite)
- Explain: debounce = wait until the user stops. Throttle = allow at most one call every X time. Cleanup clears the old timer. AbortController avoids race conditions.

---

## 294. Authentication UI with Protected Routes

**What you build**
A login page, a dashboard page that only logged-in users can see, and a logout button.

**What you learn:** Context for auth, React Router, `Navigate`, localStorage.

**Setup:** `npm install react-router-dom`

**Code**
```jsx
// AuthContext.jsx
import { createContext, useContext, useState } from "react";

const AuthContext = createContext();
export const useAuth = () => useContext(AuthContext);

export function AuthProvider({ children }) {
  const [user, setUser] = useState(() => {
    const saved = localStorage.getItem("user");
    return saved ? JSON.parse(saved) : null;
  });

  function login(email, password) {
    // Fake login. In a real app, call your API here.
    if (email === "test@mail.com" && password === "123456") {
      const u = { email };
      setUser(u);
      localStorage.setItem("user", JSON.stringify(u));
      return true;
    }
    return false;
  }

  function logout() {
    setUser(null);
    localStorage.removeItem("user");
  }

  return <AuthContext.Provider value={{ user, login, logout }}>{children}</AuthContext.Provider>;
}
```
```jsx
// App.jsx
import { BrowserRouter, Routes, Route, Navigate, useNavigate } from "react-router-dom";
import { useState } from "react";
import { AuthProvider, useAuth } from "./AuthContext";

function ProtectedRoute({ children }) {
  const { user } = useAuth();
  return user ? children : <Navigate to="/login" replace />;
}

function Login() {
  const { login } = useAuth();
  const navigate = useNavigate();
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  const [error, setError] = useState("");

  function handleSubmit(e) {
    e.preventDefault();
    if (login(email, password)) navigate("/dashboard");
    else setError("Wrong email or password");
  }

  return (
    <form onSubmit={handleSubmit}>
      <input value={email} onChange={(e) => setEmail(e.target.value)} placeholder="Email" />
      <input type="password" value={password} onChange={(e) => setPassword(e.target.value)} placeholder="Password" />
      <button>Login</button>
      {error && <p role="alert">{error}</p>}
    </form>
  );
}

function Dashboard() {
  const { user, logout } = useAuth();
  return (
    <div>
      <h1>Welcome {user.email}</h1>
      <button onClick={logout}>Logout</button>
    </div>
  );
}

export default function App() {
  return (
    <AuthProvider>
      <BrowserRouter>
        <Routes>
          <Route path="/login" element={<Login />} />
          <Route path="/dashboard" element={<ProtectedRoute><Dashboard /></ProtectedRoute>} />
          <Route path="*" element={<Navigate to="/login" />} />
        </Routes>
      </BrowserRouter>
    </AuthProvider>
  );
}
```
Test login: `test@mail.com` / `123456`.

**Interview Angle**
- Asked in interviews? **Very often**
- Must say: "This protects the UI only. Real protection must be done on the server." (See topic 200.)
- Mention: lazy initial state `useState(() => ...)` to read from localStorage, `replace` in Navigate.

---

## 295. Shopping Cart with Shared State

**What you build**
Products with an "Add to cart" button, and a cart that shows items, quantity and total, shared across the app.

**What you learn:** Context + `useReducer`, updating arrays and objects, derived totals.

**Code**
```jsx
import { createContext, useContext, useReducer } from "react";

const CartContext = createContext();
export const useCart = () => useContext(CartContext);

function cartReducer(state, action) {
  switch (action.type) {
    case "ADD": {
      const exists = state.find((i) => i.id === action.item.id);
      if (exists) {
        return state.map((i) => (i.id === action.item.id ? { ...i, qty: i.qty + 1 } : i));
      }
      return [...state, { ...action.item, qty: 1 }];
    }
    case "DECREASE":
      return state
        .map((i) => (i.id === action.id ? { ...i, qty: i.qty - 1 } : i))
        .filter((i) => i.qty > 0);
    case "REMOVE":
      return state.filter((i) => i.id !== action.id);
    case "CLEAR":
      return [];
    default:
      return state;
  }
}

export function CartProvider({ children }) {
  const [cart, dispatch] = useReducer(cartReducer, []);

  const total = cart.reduce((sum, i) => sum + i.price * i.qty, 0); // derived, not stored
  const count = cart.reduce((sum, i) => sum + i.qty, 0);

  return (
    <CartContext.Provider value={{ cart, dispatch, total, count }}>
      {children}
    </CartContext.Provider>
  );
}
```
```jsx
// Using it
const products = [
  { id: 1, name: "Shoes", price: 50 },
  { id: 2, name: "Hat", price: 20 },
];

function Shop() {
  const { dispatch } = useCart();
  return products.map((p) => (
    <div key={p.id}>
      {p.name} - ${p.price}
      <button onClick={() => dispatch({ type: "ADD", item: p })}>Add to cart</button>
    </div>
  ));
}

function Cart() {
  const { cart, dispatch, total } = useCart();
  return (
    <div>
      {cart.map((i) => (
        <div key={i.id}>
          {i.name} x {i.qty}
          <button onClick={() => dispatch({ type: "DECREASE", id: i.id })}>-</button>
          <button onClick={() => dispatch({ type: "ADD", item: i })}>+</button>
          <button onClick={() => dispatch({ type: "REMOVE", id: i.id })}>Remove</button>
        </div>
      ))}
      <h3>Total: ${total}</h3>
    </div>
  );
}

// Wrap: <CartProvider><Shop /><Cart /></CartProvider>
```

**Interview Angle**
- Asked in interviews? **Very often**
- Mention: totals are **calculated**, not stored. Why `useReducer` (many related actions). Why Context (shared by many parts). Could also use Redux Toolkit or Zustand.

---

## 296. Dashboard with API Integration

**What you build**
A dashboard with summary cards (total users, total posts) and a table of data from an API.

**What you learn:** fetching several APIs at once, `Promise.all`, loading and error states, small reusable components.

**Code**
```jsx
import { useEffect, useState } from "react";

function StatCard({ title, value }) {
  return (
    <div style={{ border: "1px solid #ccc", padding: 16, borderRadius: 8 }}>
      <p>{title}</p>
      <h2>{value}</h2>
    </div>
  );
}

export default function Dashboard() {
  const [users, setUsers] = useState([]);
  const [posts, setPosts] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState("");

  useEffect(() => {
    const controller = new AbortController();

    async function load() {
      try {
        const [uRes, pRes] = await Promise.all([
          fetch("https://jsonplaceholder.typicode.com/users", { signal: controller.signal }),
          fetch("https://jsonplaceholder.typicode.com/posts", { signal: controller.signal }),
        ]);
        if (!uRes.ok || !pRes.ok) throw new Error("Failed to load data");

        setUsers(await uRes.json());
        setPosts(await pRes.json());
      } catch (err) {
        if (err.name !== "AbortError") setError(err.message);
      } finally {
        setLoading(false);
      }
    }

    load();
    return () => controller.abort();
  }, []);

  if (loading) return <p>Loading dashboard...</p>;
  if (error) return <p role="alert">{error}</p>;

  return (
    <div>
      <div style={{ display: "flex", gap: 16 }}>
        <StatCard title="Total Users" value={users.length} />
        <StatCard title="Total Posts" value={posts.length} />
      </div>

      <h3>Users</h3>
      <table>
        <thead>
          <tr><th>Name</th><th>Email</th><th>City</th></tr>
        </thead>
        <tbody>
          {users.map((u) => (
            <tr key={u.id}>
              <td>{u.name}</td>
              <td>{u.email}</td>
              <td>{u.address.city}</td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
}
```

**Try next:** add a chart (Recharts), a refresh button, and move the fetch code to a service file.

**Interview Angle**
- Asked in interviews? **Often**
- Mention: `Promise.all` runs requests together (faster than one after another). If one fails, `Promise.all` fails. `Promise.allSettled` lets the others succeed.

---

## 297. Task Management App with Drag and Drop

**What you build**
A board with columns (To Do, In Progress, Done) where you drag cards between columns.

**What you learn:** state with objects, browser drag events, immutable updates.

This version uses the **built-in HTML drag and drop**, so no library is needed. (For production, libraries like `dnd-kit` work better, especially on phones and with keyboards.)

**Code**
```jsx
import { useState } from "react";

const columns = ["todo", "progress", "done"];
const titles = { todo: "To Do", progress: "In Progress", done: "Done" };

export default function Board() {
  const [tasks, setTasks] = useState([
    { id: 1, text: "Learn React", status: "todo" },
    { id: 2, text: "Build a project", status: "progress" },
    { id: 3, text: "Deploy it", status: "todo" },
  ]);
  const [text, setText] = useState("");

  function addTask(e) {
    e.preventDefault();
    if (!text.trim()) return;
    setTasks([...tasks, { id: Date.now(), text, status: "todo" }]);
    setText("");
  }

  function handleDragStart(e, id) {
    e.dataTransfer.setData("taskId", String(id));
  }

  function handleDrop(e, status) {
    const id = Number(e.dataTransfer.getData("taskId"));
    setTasks(tasks.map((t) => (t.id === id ? { ...t, status } : t)));
  }

  return (
    <div>
      <form onSubmit={addTask}>
        <input value={text} onChange={(e) => setText(e.target.value)} placeholder="New task" />
        <button>Add</button>
      </form>

      <div style={{ display: "flex", gap: 16, marginTop: 16 }}>
        {columns.map((col) => (
          <div
            key={col}
            onDragOver={(e) => e.preventDefault()}   // needed to allow dropping
            onDrop={(e) => handleDrop(e, col)}
            style={{ flex: 1, minHeight: 200, border: "1px solid #ccc", padding: 8 }}
          >
            <h3>{titles[col]}</h3>
            {tasks
              .filter((t) => t.status === col)
              .map((t) => (
                <div
                  key={t.id}
                  draggable
                  onDragStart={(e) => handleDragStart(e, t.id)}
                  style={{ background: "#f4f4f4", margin: "6px 0", padding: 8, cursor: "grab" }}
                >
                  {t.text}
                </div>
              ))}
          </div>
        ))}
      </div>
    </div>
  );
}
```

**Interview Angle**
- Asked in interviews? **Sometimes**
- Key point: `onDragOver` with `preventDefault()` is required, or `onDrop` will not fire.
- Mention: keyboard users need another way to move tasks (accessibility), and libraries like `dnd-kit` help with that.

---

## 298. Custom Hooks Library

**What you build**
A small collection of reusable hooks you can use in every project.

**What you learn:** what makes a custom hook (a function starting with `use` that calls other hooks), reusing logic.

**Code**
```jsx
// hooks/useToggle.js
import { useState, useCallback } from "react";
export function useToggle(initial = false) {
  const [value, setValue] = useState(initial);
  const toggle = useCallback(() => setValue((v) => !v), []);
  return [value, toggle];
}
```
```jsx
// hooks/useLocalStorage.js
import { useState, useEffect } from "react";
export function useLocalStorage(key, initialValue) {
  const [value, setValue] = useState(() => {
    try {
      const saved = localStorage.getItem(key);
      return saved ? JSON.parse(saved) : initialValue;
    } catch {
      return initialValue;
    }
  });

  useEffect(() => {
    localStorage.setItem(key, JSON.stringify(value));
  }, [key, value]);

  return [value, setValue];
}
```
```jsx
// hooks/useDebounce.js
import { useState, useEffect } from "react";
export function useDebounce(value, delay = 500) {
  const [debounced, setDebounced] = useState(value);
  useEffect(() => {
    const t = setTimeout(() => setDebounced(value), delay);
    return () => clearTimeout(t);
  }, [value, delay]);
  return debounced;
}
```
```jsx
// hooks/useFetch.js
import { useState, useEffect } from "react";
export function useFetch(url) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const controller = new AbortController();
    setLoading(true);
    setError(null);

    fetch(url, { signal: controller.signal })
      .then((res) => {
        if (!res.ok) throw new Error("Request failed: " + res.status);
        return res.json();
      })
      .then(setData)
      .catch((err) => {
        if (err.name !== "AbortError") setError(err.message);
      })
      .finally(() => setLoading(false));

    return () => controller.abort();
  }, [url]);

  return { data, loading, error };
}
```
```jsx
// hooks/usePrevious.js
import { useRef, useEffect } from "react";
export function usePrevious(value) {
  const ref = useRef();
  useEffect(() => {
    ref.current = value;
  });
  return ref.current;
}
```
```jsx
// hooks/useOnClickOutside.js
import { useEffect } from "react";
export function useOnClickOutside(ref, handler) {
  useEffect(() => {
    function listener(e) {
      if (!ref.current || ref.current.contains(e.target)) return;
      handler(e);
    }
    document.addEventListener("mousedown", listener);
    return () => document.removeEventListener("mousedown", listener);
  }, [ref, handler]);
}
```
Use it:
```jsx
const [dark, setDark] = useLocalStorage("dark", false);
const { data, loading, error } = useFetch("https://jsonplaceholder.typicode.com/users");
```

**Interview Angle**
- Asked in interviews? **Very often**
- Rules: the name must start with `use`, call hooks only at the top level, and each component using the hook gets its **own separate state** (hooks share logic, not data).

---

## 299. Performance-Optimized Large List

**What you build**
A list of 10,000 items that stays smooth, with search.

**What you learn:** `React.memo`, stable keys, `useCallback`, virtualization, `useDeferredValue`.

**Setup:** `npm install react-window`

**Code**
```jsx
import { memo, useCallback, useDeferredValue, useMemo, useState } from "react";
import { FixedSizeList } from "react-window";

const allItems = Array.from({ length: 10000 }, (_, i) => ({
  id: i,
  name: `Item number ${i + 1}`,
}));

// memo: a row re-renders only if its own props change
const Row = memo(function Row({ index, style, data }) {
  const item = data.items[index];
  return (
    <div style={style}>
      {item.name}
      <button onClick={() => data.onSelect(item.id)}>Select</button>
    </div>
  );
});

export default function BigList() {
  const [search, setSearch] = useState("");
  const [selected, setSelected] = useState(null);

  // slow work uses the "late" copy, so typing stays smooth
  const deferredSearch = useDeferredValue(search);

  const filtered = useMemo(
    () => allItems.filter((i) => i.name.toLowerCase().includes(deferredSearch.toLowerCase())),
    [deferredSearch]
  );

  const onSelect = useCallback((id) => setSelected(id), []);

  // keep the same object so rows are not re-created for nothing
  const itemData = useMemo(() => ({ items: filtered, onSelect }), [filtered, onSelect]);

  return (
    <div>
      <input value={search} onChange={(e) => setSearch(e.target.value)} placeholder="Search 10,000 items" />
      <p>Showing {filtered.length} items. Selected: {selected ?? "none"}</p>

      <FixedSizeList
        height={400}
        width={400}
        itemCount={filtered.length}
        itemSize={40}
        itemData={itemData}
      >
        {Row}
      </FixedSizeList>
    </div>
  );
}
```

**What each trick does**
| Trick | Why |
|---|---|
| Virtualization (`react-window`) | Draws only ~10 visible rows, not 10,000 |
| `React.memo` | Rows do not re-render without need |
| `useCallback` / `useMemo` | Keep props the same, so memo works |
| `useDeferredValue` | Typing stays smooth during heavy filtering |
| Stable `key`/ids | Correct and fast updates |

**Interview Angle**
- Asked in interviews? **Often**
- Best answer: "I'd first measure with the Profiler. For 10,000 items, virtualization gives the biggest win."

---

## 300. Full React Portfolio Project

**What you build**
A personal website that shows who you are and your work. Recruiters will open it, so make it clean and fast.

**Pages / sections**
- **Home / Hero**: your name, role, short intro, a button to your projects.
- **About**: short story, skills.
- **Projects**: cards with image, description, tech used, **live link** and **GitHub link**.
- **Skills**: simple list or tags.
- **Contact**: a working contact form (use EmailJS or Formspree) and social links.
- **Resume**: a download button.

**Concepts to use (from these notes)**
| Concept | Where |
|---|---|
| Components and props | Project cards, skill tags |
| React Router | Home, Projects, Contact pages |
| Controlled forms + validation | Contact form |
| `useEffect` + API | Show your GitHub repos using the GitHub API |
| Context | Dark / light theme |
| `useLocalStorage` hook | Remember the theme |
| Lazy loading + Suspense | Load pages when needed |
| Image optimization | WebP images, `loading="lazy"` |
| Accessibility | Semantic tags, alt text, keyboard focus |
| SEO | Page titles and descriptions |
| Deployment | Vercel or Netlify, with redirect rule |
| Env variables | Contact form keys (public keys only) |

**Starter code (theme switch + project cards)**
```jsx
import { createContext, useContext, useEffect, useState } from "react";

const ThemeContext = createContext();
export const useTheme = () => useContext(ThemeContext);

export function ThemeProvider({ children }) {
  const [theme, setTheme] = useState(() => localStorage.getItem("theme") || "light");

  useEffect(() => {
    document.documentElement.setAttribute("data-theme", theme);
    localStorage.setItem("theme", theme);
  }, [theme]);

  const toggle = () => setTheme((t) => (t === "light" ? "dark" : "light"));
  return <ThemeContext.Provider value={{ theme, toggle }}>{children}</ThemeContext.Provider>;
}
```
```jsx
const projects = [
  {
    id: 1,
    title: "Weather App",
    description: "Search any city and see the live weather.",
    tech: ["React", "Open-Meteo API"],
    live: "https://example.com",
    github: "https://github.com/you/weather",
  },
];

function ProjectCard({ project }) {
  return (
    <article>
      <h3>{project.title}</h3>
      <p>{project.description}</p>
      <p>{project.tech.join(", ")}</p>
      <a href={project.live} target="_blank" rel="noreferrer">Live</a>{" "}
      <a href={project.github} target="_blank" rel="noreferrer">Code</a>
    </article>
  );
}

export function Projects() {
  return (
    <section>
      <h2>Projects</h2>
      {projects.map((p) => <ProjectCard key={p.id} project={p} />)}
    </section>
  );
}
```
```css
/* CSS for theme */
:root[data-theme="light"] { --bg: #ffffff; --text: #111111; }
:root[data-theme="dark"]  { --bg: #111111; --text: #f5f5f5; }
body { background: var(--bg); color: var(--text); }
```

**Final checklist before you share it**
- [ ] Works on mobile and desktop
- [ ] Every image has `alt` text
- [ ] No console errors
- [ ] All links work
- [ ] Lighthouse score is good
- [ ] Deployed, and refresh on any page works (no 404)
- [ ] Each project has a live link and a GitHub link
- [ ] No secret keys in the code

**Interview Angle**
- Asked in interviews? **Very often**: "Tell me about a project you built."
- Prepare a short story for each project: **What problem it solves, what you built, one hard problem you solved, and what you would improve.**
- Be ready to explain every line of your own code.

---

# Final Quick Revision

**Top 15 things interviewers love to ask (from these notes)**
1. Props vs State
2. Why keys are important
3. Virtual DOM and reconciliation
4. Why a component re-renders
5. Controlled vs uncontrolled components
6. `useState` update behavior (batching, function form)
7. `useEffect` dependency array and cleanup
8. `useRef` vs `useState`
9. `useMemo` vs `useCallback` vs `React.memo`
10. Stale closures
11. Context API vs Redux
12. Fetching data with loading and error states
13. Race conditions and AbortController
14. Why frontend route protection is not real security
15. How to optimize a slow React app

**Good luck. Practise by building, not only by reading.**
