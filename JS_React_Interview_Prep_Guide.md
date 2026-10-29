# JavaScript + React Interview Prep Guide

> **Goal:** After you finish this list, you should be able to answer most fresher/junior (0–3 years) frontend interview questions with confidence.
> **Priority:** 🔥 = asked in almost every interview · ⭐ = asked very often · 🙂 = asked sometimes
> **How to use:** Tick the box ✅ only when you can answer **out loud, in your own words, in 30–60 seconds** (not just read it).

---

# Part 1: How to Prepare (Read This First)

## The 5-step method for every question
1. **Read** the topic from your notes.
2. **Say it out loud** in simple words, as if you are explaining to a friend.
3. **Write a small code example** from memory (no copy-paste).
4. **Break it:** change the code and guess what happens, then run it.
5. **Revise** after 1 day, 3 days and 7 days.

## How to answer in an interview (simple formula)
**Definition → Example → Why / When to use → Common mistake**

Example for "What is a closure?":
- *Definition:* "A closure is when an inner function remembers the variables of its outer function even after the outer function is finished."
- *Example:* counter function.
- *Why:* private data, debounce, memoization.
- *Mistake:* the `var` in a loop with `setTimeout`.

## 8-Week Study Plan (about 2 hours a day)

| Week | Focus | Goal |
|---|---|---|
| 1 | JS basics: variables, types, coercion, functions, arrays, objects | Finish Section A & B |
| 2 | JS core: scope, hoisting, `this`, closures, prototypes | Finish Section C & D |
| 3 | JS async: callbacks, promises, async/await, event loop + DOM basics | Finish Section E & F |
| 4 | JS coding practice (25+ problems) + polyfills | Finish Section G |
| 5 | React basics: JSX, components, props, state, events, lists, forms | Finish Section H & I |
| 6 | React hooks deeply + data fetching + context | Finish Section J & K |
| 7 | React performance, routing, state management, patterns, testing | Finish Section L, M, N |
| 8 | Build 1 mini project + mock interviews + revise weak areas | Section O, P, Q |

## Golden rules
- **Don't just read. Speak.** Practice answers out loud or record yourself.
- **Depth over quantity.** Knowing 40 topics well beats knowing 150 topics shallowly.
- **Build projects.** Interviewers always ask, "Tell me about your project." Build at least: Todo app, a weather/movie app using an API, and one bigger app (e-commerce cart / dashboard).
- **If you don't know, say so and reason.** "I haven't used it, but I think it works like..." is better than guessing wrongly.
- **Practice 2 mock interviews a week** with a friend, or by talking to an AI tool.

---

# Part 2: JavaScript Questions (in learning order)

## Section A: Basics (Week 1)

- [ ] 1. 🔥 What is JavaScript? Is it compiled or interpreted? How is it different from Java?
- [ ] 2. 🔥 What is the difference between `var`, `let` and `const`?
- [ ] 3. 🔥 What are the data types in JavaScript? What is the difference between primitive and reference types?
- [ ] 4. 🔥 Why does `typeof null` return `"object"`? How do you check for an array?
- [ ] 5. 🔥 What is the difference between `null` and `undefined`?
- [ ] 6. 🔥 What is the difference between `==` and `===`?
- [ ] 7. 🔥 What is type coercion? Explain with examples (`"5" + 2`, `"5" - 2`, `[] + {}`).
- [ ] 8. 🔥 What are truthy and falsy values? List all the falsy values.
- [ ] 9. ⭐ What is `NaN`? Why is `NaN === NaN` false? How do you check for it?
- [ ] 10. ⭐ What is the difference between a function declaration and a function expression?
- [ ] 11. 🔥 What are arrow functions? How are they different from normal functions?
- [ ] 12. ⭐ What are default parameters, rest parameters and the spread operator? What is the difference between rest and spread?
- [ ] 13. 🙂 What are template literals?
- [ ] 14. ⭐ What is the difference between `break` and `continue`? Why can't you `break` out of `forEach`?

## Section B: Arrays and Objects (Week 1)

- [ ] 15. 🔥 What is the difference between `map`, `filter`, `reduce` and `forEach`?
- [ ] 16. 🔥 What is the difference between `slice` and `splice`?
- [ ] 17. 🔥 How does `sort()` work? Why does `[10, 9, 1].sort()` give a wrong order?
- [ ] 18. ⭐ What is the difference between `find`, `filter`, `some` and `every`?
- [ ] 19. ⭐ What is the difference between `push/pop` and `shift/unshift`? Which ones change the original array?
- [ ] 20. 🔥 What is destructuring? (array and object)
- [ ] 21. 🔥 What is a shallow copy and a deep copy? How do you make each?
- [ ] 22. ⭐ What are the problems of `JSON.parse(JSON.stringify(obj))`? What is `structuredClone`?
- [ ] 23. 🔥 What is the difference between `Object.keys`, `Object.values` and `Object.entries`?
- [ ] 24. ⭐ What are optional chaining `?.` and nullish coalescing `??`? How is `??` different from `||`?
- [ ] 25. ⭐ What is the difference between `Object.freeze` and `Object.seal`? Is `const` the same as freeze?
- [ ] 26. ⭐ How do you remove duplicates from an array? (Give 2–3 ways)
- [ ] 27. 🙂 What is the difference between `Set` and `Map`? When to use `WeakMap`?
- [ ] 28. ⭐ How do you compare two objects or two arrays? Why is `{} === {}` false?

## Section C: Scope, Hoisting, `this` (Week 2)

- [ ] 29. 🔥 What is scope? Explain global, function and block scope.
- [ ] 30. 🔥 What is hoisting? How do `var`, `let`, `const` and functions behave?
- [ ] 31. 🔥 What is the Temporal Dead Zone?
- [ ] 32. ⭐ What is lexical scope and the scope chain?
- [ ] 33. ⭐ What is an execution context and the call stack?
- [ ] 34. 🔥 How does the `this` keyword work in different situations (global, method, function, arrow, event handler, constructor)?
- [ ] 35. 🔥 What are `call`, `apply` and `bind`? What is the difference?
- [ ] 36. 🔥 What is a closure? Give real-life uses.
- [ ] 37. 🔥 Output question: `for (var i...) setTimeout(...)` prints what? How to fix it?
- [ ] 38. 🙂 What is an IIFE and why was it used?
- [ ] 39. ⭐ What are higher-order functions, callbacks, and first-class functions?
- [ ] 40. ⭐ What are pure functions and side effects?
- [ ] 41. ⭐ What is recursion? What is a base case? What causes "Maximum call stack size exceeded"?

## Section D: Prototypes, Classes, Advanced Concepts (Week 2)

- [ ] 42. 🔥 What is a prototype and the prototype chain?
- [ ] 43. ⭐ What is the difference between `__proto__` and `prototype`?
- [ ] 44. 🔥 What is prototypal inheritance? How is it different from class-based inheritance?
- [ ] 45. 🔥 What are classes in JS? How do `extends` and `super` work?
- [ ] 46. ⭐ What is the `new` keyword? What happens step by step when you use it?
- [ ] 47. 🙂 What are getters, setters and private fields (`#`)?
- [ ] 48. 🙂 What are static methods?
- [ ] 49. 🙂 What is strict mode?
- [ ] 50. 🙂 What are property descriptors (`writable`, `enumerable`, `configurable`)?
- [ ] 51. ⭐ What is currying? What is partial application?
- [ ] 52. 🔥 What is memoization?
- [ ] 53. 🙂 What is function composition / pipe?
- [ ] 54. 🙂 What are the error types in JS? How do you create a custom error?
- [ ] 55. 🙂 What is garbage collection? What causes memory leaks in the browser?
- [ ] 56. ⭐ CommonJS vs ES modules. What are named vs default exports?
- [ ] 57. 🙂 What is `for...in` vs `for...of`? What are iterators and generators?

## Section E: Asynchronous JavaScript (Week 3)

- [ ] 58. 🔥 Synchronous vs asynchronous. Is JavaScript single-threaded?
- [ ] 59. ⭐ What is callback hell? How do you solve it?
- [ ] 60. 🔥 What is a Promise? What are its states?
- [ ] 61. 🔥 What are `then`, `catch` and `finally`? How does promise chaining work?
- [ ] 62. 🔥 Difference between `Promise.all`, `allSettled`, `race` and `any`.
- [ ] 63. 🔥 What are `async/await`? How do you handle errors?
- [ ] 64. 🔥 Sequential vs parallel execution with `await`. How do you make it parallel?
- [ ] 65. 🔥 What is the event loop? Explain call stack, Web APIs, callback queue.
- [ ] 66. 🔥 What are microtasks and macrotasks? Which runs first?
- [ ] 67. 🔥 Output question: mix of `setTimeout`, `Promise.then` and `console.log`.
- [ ] 68. ⭐ How does `fetch` work? Does `fetch` reject on a 404 error?
- [ ] 69. 🙂 What is `AbortController`? What are race conditions in async code?
- [ ] 70. ⭐ Common HTTP methods and status codes (200, 201, 400, 401, 403, 404, 500).

## Section F: DOM and Browser (Week 3)

- [ ] 71. ⭐ What is the DOM? Difference between `innerHTML`, `innerText` and `textContent`.
- [ ] 72. ⭐ `querySelector` vs `getElementById`. What does `querySelectorAll` return?
- [ ] 73. 🔥 Event bubbling and capturing.
- [ ] 74. 🔥 What is event delegation? Why is it useful?
- [ ] 75. 🔥 `preventDefault()` vs `stopPropagation()`.
- [ ] 76. ⭐ `event.target` vs `event.currentTarget`.
- [ ] 77. 🔥 Debouncing vs throttling. Give use cases.
- [ ] 78. ⭐ `localStorage` vs `sessionStorage` vs cookies.
- [ ] 79. ⭐ What are `JSON.stringify` and `JSON.parse`? What happens with invalid JSON?
- [ ] 80. 🙂 `DOMContentLoaded` vs `load`. What are `async` and `defer` in script tags?
- [ ] 81. 🙂 What are Web Workers? What is CORS? (Know the basic idea)

## Section G: Coding Questions (Week 4)

Practice each one **without looking** at the answer. Write on paper or a plain editor.

**Strings / Arrays**
- [ ] 82. 🔥 Reverse a string. Check palindrome.
- [ ] 83. 🔥 Check if two strings are anagrams.
- [ ] 84. 🔥 Find the first non-repeating character.
- [ ] 85. 🔥 Count the frequency of each character or word.
- [ ] 86. 🔥 Remove duplicates from an array.
- [ ] 87. 🔥 Flatten a nested array (recursion + `flat`).
- [ ] 88. 🔥 Two Sum.
- [ ] 89. ⭐ Find the largest / second largest number.
- [ ] 90. ⭐ Find missing and duplicate numbers.
- [ ] 91. ⭐ Rotate an array by k positions.
- [ ] 92. ⭐ Group array of objects by a key (`reduce`).
- [ ] 93. ⭐ Sort an array of objects by a property.
- [ ] 94. 🙂 Binary search.
- [ ] 95. 🙂 Fibonacci (recursion + memoization). Factorial.

**Function-based (very important)**
- [ ] 96. 🔥 Implement `debounce` and `throttle`.
- [ ] 97. 🔥 Implement a `curry` function and `add(1)(2)(3)`.
- [ ] 98. 🔥 Implement `memoize`.
- [ ] 99. 🔥 Write a polyfill for `map`, `filter`, `reduce`.
- [ ] 100. 🔥 Write a polyfill for `bind`.
- [ ] 101. 🔥 Implement `Promise.all` from scratch.
- [ ] 102. ⭐ Implement a function that runs only once (`once`).
- [ ] 103. ⭐ Deep clone an object (recursively).
- [ ] 104. 🙂 Implement a simple event emitter (`on`, `emit`, `off`).
- [ ] 105. 🙂 Implement a simple `Promise` class (basic version).

**Output-based (very common!)**
- [ ] 106. 🔥 Hoisting, TDZ and scope outputs.
- [ ] 107. 🔥 Closure outputs (loops, counters).
- [ ] 108. 🔥 `this` outputs (object methods, arrow functions, lost `this`).
- [ ] 109. 🔥 Event loop outputs.
- [ ] 110. 🔥 Type coercion outputs (`[] + []`, `null >= 0`, `"b" + "a" + +"a"`).

---

# Part 3: React Questions (in learning order)

> **Before React:** Make sure you are comfortable with ES6 (destructuring, spread, arrow functions, modules), array methods (`map`, `filter`), and promises/`async-await`. Most React mistakes are really JavaScript mistakes.

## Section H: React Basics (Week 5)

- [ ] 111. 🔥 What is React? Why do we use it? Library or framework?
- [ ] 112. 🔥 What is JSX? Can browsers understand it? (Babel/compiler converts it)
- [ ] 113. 🔥 What are components? Functional vs class components.
- [ ] 114. 🔥 What is the Virtual DOM? How does it make React fast?
- [ ] 115. 🔥 What is reconciliation / the diffing algorithm?
- [ ] 116. 🔥 What are props? Are props read-only?
- [ ] 117. 🔥 What is state? Difference between props and state.
- [ ] 118. ⭐ What are Fragments? Why are they used?
- [ ] 119. ⭐ How do you handle events in React? (`onClick`, synthetic events)
- [ ] 120. 🔥 Why do we need `key` in lists? Why not use the index as a key?
- [ ] 121. ⭐ How do you do conditional rendering? (ternary, `&&`, early return)
- [ ] 122. ⭐ What is `children` prop?
- [ ] 123. 🙂 What is the difference between real DOM and virtual DOM?
- [ ] 124. 🙂 What is a single-page application (SPA)? Pros and cons.
- [ ] 125. 🙂 What is the difference between React and React DOM? (Vite / CRA / Next.js basics)

## Section I: State, Forms and Data Flow (Week 5)

- [ ] 126. 🔥 Why can't we change state directly? How do you update objects and arrays in state immutably?
- [ ] 127. 🔥 Is `setState` / `useState` asynchronous? What is batching?
- [ ] 128. 🔥 When to use the functional update: `setCount(prev => prev + 1)`?
- [ ] 129. 🔥 Controlled vs uncontrolled components.
- [ ] 130. ⭐ How do you handle forms and validation in React?
- [ ] 131. 🔥 What is "lifting state up"?
- [ ] 132. 🔥 What is prop drilling? How can you avoid it?
- [ ] 133. ⭐ One-way data flow in React. How does a child talk to its parent?
- [ ] 134. 🙂 What is a pure component and why must render be pure?

## Section J: Hooks (Week 6)

- [ ] 135. 🔥 What are hooks? Why were they introduced?
- [ ] 136. 🔥 What are the Rules of Hooks? Why can't you use hooks inside conditions or loops?
- [ ] 137. 🔥 How does `useState` work? (initial value, lazy initialization)
- [ ] 138. 🔥 How does `useEffect` work? Explain the dependency array: none, `[]`, `[x]`.
- [ ] 139. 🔥 What is the cleanup function in `useEffect`? When does it run?
- [ ] 140. 🔥 Common `useEffect` bugs: infinite loops, stale values, missing dependencies.
- [ ] 141. 🔥 What is `useRef`? Uses: access DOM, store values without re-render.
- [ ] 142. 🔥 `useMemo` vs `useCallback`. When to use and when NOT to use.
- [ ] 143. 🔥 What is `useContext`? How do you create and use Context?
- [ ] 144. ⭐ What is `useReducer`? When is it better than `useState`?
- [ ] 145. 🔥 What are custom hooks? Write one (`useFetch`, `useDebounce`, `useLocalStorage`).
- [ ] 146. 🙂 What is `useLayoutEffect`? How is it different from `useEffect`?
- [ ] 147. 🙂 What are `useId`, `useTransition` and `useDeferredValue`? (Basic idea only)
- [ ] 148. ⭐ Class component lifecycle methods and their hook equivalents (`componentDidMount`, `componentDidUpdate`, `componentWillUnmount`).
- [ ] 149. ⭐ How do you fetch data in React? Handling loading and error states.
- [ ] 150. ⭐ How do you avoid race conditions or memory leaks in `useEffect` while fetching? (cleanup / AbortController)
- [ ] 151. 🙂 What is `forwardRef`? (In React 19, `ref` can be passed as a normal prop.)

## Section K: Rendering, Performance and Patterns (Week 7)

- [ ] 152. 🔥 What makes a component re-render? How do you stop unnecessary re-renders?
- [ ] 153. 🔥 What is `React.memo`? How is it different from `useMemo`?
- [ ] 154. 🔥 What is code splitting and lazy loading? (`React.lazy`, `Suspense`)
- [ ] 155. ⭐ What are Error Boundaries? Can they be written with hooks? (No, they need a class component or a library)
- [ ] 156. ⭐ What are Higher-Order Components (HOC)?
- [ ] 157. ⭐ What are render props? Why are custom hooks preferred now?
- [ ] 158. 🙂 What are Portals? (modals, tooltips)
- [ ] 159. 🙂 What is `StrictMode`? Why does an effect run twice in development?
- [ ] 160. 🙂 What is list virtualization? (large lists)
- [ ] 161. 🙂 What is the difference between CSR, SSR and SSG? (Next.js basics)
- [ ] 162. 🙂 How do you optimise a slow React app? (Profiler, memoization, splitting, lazy load, avoid inline heavy work)
- [ ] 163. 🙂 Composition vs inheritance in React.
- [ ] 164. 🙂 What is the React Compiler and what new features came with React 19? (Actions, `use`, `useActionState`, `useOptimistic`. Just know the basic idea.)

## Section L: Routing and State Management (Week 7)

- [ ] 165. 🔥 How does React Router work? (`BrowserRouter`, `Routes`, `Route`, `Link`, `useNavigate`, `useParams`)
- [ ] 166. ⭐ How do you protect a route (private route / login check)?
- [ ] 167. ⭐ What is nested routing? What is `Outlet`?
- [ ] 168. 🔥 What is Redux? Explain store, action, reducer, dispatch.
- [ ] 169. ⭐ What is Redux Toolkit? Why is it recommended?
- [ ] 170. ⭐ Context API vs Redux. When to use which?
- [ ] 171. 🙂 What are Redux middlewares (thunk)? How do you handle async actions?
- [ ] 172. 🙂 Know one more option: Zustand / React Query (TanStack Query). Why use React Query for server data?

## Section M: Testing and Tooling (Week 7)

- [ ] 173. 🙂 How do you test React components? (Jest + React Testing Library: what to test and what not to)
- [ ] 174. 🙂 What is Vite / Webpack / Babel? What does a bundler do?
- [ ] 175. 🙂 How do you handle environment variables and API keys safely?
- [ ] 176. 🙂 How do you style React apps? (CSS Modules, Tailwind, styled-components)
- [ ] 177. 🙂 How do you improve accessibility (a11y) in React? (semantic HTML, labels, alt text, keyboard support)

## Section N: React Coding / Machine Coding Tasks (Week 7–8)

Build each one **at least once**. These are asked in real interviews.

- [ ] 178. 🔥 Counter with increment, decrement, reset.
- [ ] 179. 🔥 Todo app (add, delete, edit, mark complete, filter).
- [ ] 180. 🔥 Fetch data from an API and show it in a list (with loading and error).
- [ ] 181. 🔥 Search box with **debounce** filtering a list.
- [ ] 182. 🔥 Form with validation (signup / login).
- [ ] 183. ⭐ Accordion / FAQ.
- [ ] 184. ⭐ Tabs component.
- [ ] 185. ⭐ Modal (open / close, click outside to close).
- [ ] 186. ⭐ Dark / light theme toggle using Context.
- [ ] 187. ⭐ Pagination or infinite scroll.
- [ ] 188. ⭐ Star rating component.
- [ ] 189. ⭐ Shopping cart (add, remove, change quantity, total price).
- [ ] 190. 🙂 Stopwatch / timer (with `useRef` and `setInterval` cleanup).
- [ ] 191. 🙂 Autocomplete / typeahead search.
- [ ] 192. 🙂 Image carousel / slider.
- [ ] 193. 🙂 Tic-tac-toe game.
- [ ] 194. 🙂 OTP input with auto-focus on next box.
- [ ] 195. 🙂 Nested comments or file explorer (recursive component).

---

# Part 4: Project and HR Questions (Week 8)

Prepare **short, honest answers** for these.

- [ ] 196. 🔥 Tell me about yourself. (30–60 seconds: background → skills → projects → goal)
- [ ] 197. 🔥 Explain your best project: What problem does it solve? Tech used? Your role? Hardest problem and how you solved it?
- [ ] 198. 🔥 Why did you choose React? Why this tech stack?
- [ ] 199. ⭐ How do you manage state in your project? Why that approach?
- [ ] 200. ⭐ How did you handle API calls, errors and loading in your project?
- [ ] 201. ⭐ What would you improve in your project if you had more time?
- [ ] 202. ⭐ Tell me about a bug that took a long time to fix. How did you debug it?
- [ ] 203. 🙂 How do you keep learning? How do you work in a team (Git, branches, pull requests)?
- [ ] 204. 🙂 Basic Git: `clone`, `branch`, `commit`, `merge` vs `rebase`, resolving conflicts.
- [ ] 205. 🙂 Where do you see yourself in 3 years? Do you have any questions for us?

---

# Part 5: Final Checklist Before Your Interview

**JavaScript confidence check — can you do these without help?**
- [ ] Explain closures with an example
- [ ] Explain the event loop with the "Start / Timeout / Promise / End" example
- [ ] Explain `this` in 5 situations
- [ ] Write `debounce`, `curry`, `memoize` and a `map` polyfill
- [ ] Write `Promise.all` from scratch
- [ ] Solve Two Sum, flatten array, remove duplicates in 2 ways

**React confidence check — can you do these without help?**
- [ ] Explain the Virtual DOM and reconciliation in simple words
- [ ] Explain every `useEffect` dependency case and cleanup
- [ ] Explain `useMemo` vs `useCallback` vs `React.memo`
- [ ] Build a Todo app and a search-with-debounce list in under 30 minutes
- [ ] Write a custom hook
- [ ] Explain Context vs Redux and when you would use each

## Common mistakes to avoid
1. Memorising definitions without writing code.
2. Skipping JavaScript and jumping straight to React.
3. Having projects you can't explain (never put something on your resume that you can't explain line by line).
4. Using AI to write all your project code. You must understand every line.
5. Not practising output-based questions. They are asked very often.
6. Panicking when you don't know an answer. Stay calm, think out loud.

## During the interview
- Listen to the full question first. Ask a small clarifying question if needed.
- Think out loud while coding. The interviewer wants to see **how you think**.
- Start with a simple working solution, then improve it.
- Test with an example and an edge case (empty input, `null`).
- Mention time complexity if you are solving a coding problem.

---

**Tip:** Use the notes file you already have for Section A–G concepts. Come back here for the *questions*, and tick them off one by one.
