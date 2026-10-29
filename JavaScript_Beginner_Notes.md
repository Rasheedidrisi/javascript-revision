# JavaScript Notes for Beginners (Simple Language + Interview Tips)

> **How to use these notes**
> - Each topic has 3 parts: **Simple Definition**, **Code Example**, and **Interview Angle**.
> - Interview Angle shows how often it is asked: 🔥 Very High · ⭐ High · 🙂 Medium · 💤 Low.
> - It also lists the **common confusion** that people make in interviews.
> - Tip: Read the definition, run the code yourself in the browser console (press `F12`), then read the interview part.

---

# Level 1: JavaScript Fundamentals

### 1. Introduction to JavaScript

**Simple Definition:**
JavaScript is a programming language. It is used to make websites do things. HTML builds the page, CSS makes it look nice, and JavaScript makes it *work* (clicks, forms, popups, animations). It also runs outside the browser (for example with Node.js) to build servers and apps.

**Code Example:**
```js
console.log("Hello, World!"); // prints a message
alert("Welcome!");            // shows a popup in the browser
```

**Interview Angle:** ⭐ High (usually the first question)
- Be ready to say: *"JavaScript is a lightweight, interpreted language used to make web pages interactive."*
- **Common confusion:** JavaScript is **not** Java. They are different languages with a similar name.

---

### 2. How JavaScript Works in the Browser

**Simple Definition:**
When you open a web page, the browser downloads HTML, CSS and JavaScript. It reads the HTML first and builds the page. When it finds JavaScript, it runs the code line by line, from top to bottom. The JavaScript can then change the page (text, colors, buttons) while you are using it.

**Code Example:**
```html
<h1 id="title">Hello</h1>
<script>
  document.getElementById("title").innerText = "Hello from JavaScript!";
</script>
```

**Interview Angle:** 🙂 Medium
- Simple answer: *"The browser reads the code and its JavaScript engine runs it, one line at a time."*
- **Common confusion:** People think the browser "compiles everything first and then runs". Modern engines do both quickly, but saying "reads and runs line by line" is accepted for beginners.

---

### 3. JavaScript Engine and Runtime Basics

**Simple Definition:**
- **Engine** = the program that understands and runs your JavaScript code. (Chrome uses **V8**, Firefox uses **SpiderMonkey**.)
- **Runtime** = the full environment where the engine works. It gives extra tools such as timers, `fetch`, and the DOM. Browser and Node.js are two different runtimes.

Think of it like this: the engine is the *brain*, and the runtime is the *whole body* with hands and eyes.

**Code Example:**
```js
// setTimeout is NOT part of the engine. The runtime (browser) gives it to us.
setTimeout(() => console.log("Hi after 1 second"), 1000);
```

**Interview Angle:** ⭐ High
- Know: V8 = Chrome and Node.js engine.
- **Common confusion:** Mixing up "engine" and "runtime". Remember: engine runs the code, runtime gives extra features.

---

### 4. Variables: var, let, const

**Simple Definition:**
A variable is a **named box** that stores a value so you can use it later. There are three ways to make one:
- `var` – old way. Avoid it today.
- `let` – use when the value can change.
- `const` – use when the value should **not** be re-assigned.

**Code Example:**
```js
let age = 20;
age = 21;            // allowed

const name = "Sam";
// name = "Ravi";    // ERROR: cannot re-assign a const

var city = "Pune";   // old style
```

**Interview Angle:** 🔥 Very High
- Differences to remember:

| | var | let | const |
|---|---|---|---|
| Scope | function | block `{ }` | block `{ }` |
| Re-assign | yes | yes | no |
| Re-declare in same scope | yes | no | no |
| Hoisted value | `undefined` | not usable (TDZ) | not usable (TDZ) |

- **Common confusion:** `const` does **not** make an object or array unchangeable. It only stops re-assigning the variable.
```js
const list = [1, 2];
list.push(3);   // works fine
// list = [5];  // error
```

---

### 5. Keywords and Identifiers

**Simple Definition:**
- **Keywords** are special words that JavaScript already uses for its own work (`let`, `if`, `function`, `return`). You cannot use them as variable names.
- **Identifiers** are the names *you* choose for variables, functions, etc.

Rules for identifiers: start with a letter, `_` or `$`; no spaces; no starting with a number; case matters (`age` and `Age` are different).

**Code Example:**
```js
let userName = "Asha";   // userName is an identifier
let _count = 5;          // valid
let $price = 100;        // valid
// let 1name = "x";      // invalid: starts with a number
// let let = 5;          // invalid: 'let' is a keyword
```

**Interview Angle:** 💤 Low
- Rarely asked alone, but can come as "Is `$name` a valid variable name?" (Yes.)
- **Common confusion:** Forgetting that JavaScript is **case-sensitive**.

---

### 6. Data Types

**Simple Definition:**
A data type tells what kind of value we have. JavaScript has:

**Primitive (simple) types:** `string`, `number`, `boolean`, `undefined`, `null`, `bigint`, `symbol`
**Non-primitive:** `object` (this includes arrays and functions)

**Code Example:**
```js
typeof "hello";     // "string"
typeof 42;          // "number"
typeof true;        // "boolean"
typeof undefined;   // "undefined"
typeof null;        // "object"  <-- famous bug!
typeof [1, 2];      // "object"
typeof function(){} // "function"
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** `typeof null` gives `"object"`. This is an old bug in JavaScript that was never fixed. Also, `typeof []` is `"object"`; use `Array.isArray([])` to check for arrays.

---

### 7. Primitive vs Reference Types

**Simple Definition:**
- **Primitive** values (numbers, strings, booleans...) are stored **by value**. When you copy one, you get a separate copy.
- **Reference** values (objects, arrays, functions) are stored **by address**. When you copy one, both variables point to the **same** thing.

Think: primitive = photocopy of a paper. Reference = two people sharing the same Google Doc link.

**Code Example:**
```js
let a = 10;
let b = a;
b = 20;
console.log(a); // 10  (not affected)

let obj1 = { name: "Sam" };
let obj2 = obj1;
obj2.name = "Ravi";
console.log(obj1.name); // "Ravi"  (affected!)
```

**Interview Angle:** 🔥 Very High
- Very commonly asked with "output questions".
- **Common confusion:** Thinking `let obj2 = obj1` makes a new object. It does not. It only copies the address.

---

### 8. Operators

**Simple Definition:**
Operators are symbols that do work on values.
- **Arithmetic:** `+ - * / % **`
- **Assignment:** `= += -= *=`
- **Comparison:** `> < >= <= == === !=  !==`
- **Logical:** `&&` (and), `||` (or), `!` (not)
- **Others:** `++`, `--`, `typeof`, ternary `? :`

**Code Example:**
```js
let x = 10, y = 3;
console.log(x + y);   // 13
console.log(x % y);   // 1  (remainder)
console.log(x ** 2);  // 100 (power)
console.log(x > 5 && y < 5); // true
let result = x > 5 ? "big" : "small"; // "big"
```

**Interview Angle:** ⭐ High
- **Common confusion:** `+` adds numbers but joins strings: `"5" + 3` gives `"53"`, while `"5" - 3` gives `2`.

---

### 9. Type Conversion

**Simple Definition:**
Type conversion means **you** change a value from one type to another on purpose, using built-in helpers.

**Code Example:**
```js
Number("42");      // 42
Number("abc");     // NaN
String(100);       // "100"
Boolean(0);        // false
parseInt("10px");  // 10
parseFloat("3.5kg");// 3.5
```

**Interview Angle:** ⭐ High
- Often asked together with coercion (next topic).
- **Common confusion:** `Number("")` is `0`, and `Number(null)` is `0`, but `Number(undefined)` is `NaN`.

---

### 10. Type Coercion

**Simple Definition:**
Type coercion means **JavaScript automatically** changes the type of a value for you when you mix types. It happens silently, so it can surprise you.

**Code Example:**
```js
console.log("5" + 2);   // "52"  (number became string)
console.log("5" - 2);   // 3     (string became number)
console.log(true + 1);  // 2     (true became 1)
console.log([] + {});   // "[object Object]"
```

**Interview Angle:** 🔥 Very High
- Interviewers love output questions here.
- Rule of thumb: `+` prefers **strings**. `- * /` prefer **numbers**.
- **Difference from conversion:** conversion = you do it; coercion = JavaScript does it automatically.

---

### 11. == vs ===

**Simple Definition:**
- `==` (loose equality) compares values **after** changing their types.
- `===` (strict equality) compares value **and** type. No changing.

Always prefer `===`.

**Code Example:**
```js
console.log(5 == "5");   // true
console.log(5 === "5");  // false
console.log(null == undefined);  // true
console.log(null === undefined); // false
console.log(0 == false); // true
console.log(0 === false);// false
```

**Interview Angle:** 🔥 Very High (almost always asked)
- **Common confusion:** `NaN === NaN` is `false`. Use `Number.isNaN(value)` to check for NaN.

---

### 12. Truthy and Falsy Values

**Simple Definition:**
When JavaScript needs a true/false answer (like inside `if`), every value is treated as either "truthy" (counts as true) or "falsy" (counts as false).

**The only falsy values:** `false`, `0`, `-0`, `0n`, `""` (empty string), `null`, `undefined`, `NaN`.
**Everything else is truthy**, including `"0"`, `"false"`, `[]`, `{}`.

**Code Example:**
```js
if ("hello") console.log("truthy");  // runs
if (0) console.log("nope");          // does not run
if ([]) console.log("empty array is truthy"); // runs
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** An empty array `[]` and empty object `{}` are **truthy**. Also `"0"` (string) is truthy.

---

### 13. null vs undefined

**Simple Definition:**
- `undefined` = "a value was never given". JavaScript sets it automatically.
- `null` = "empty on purpose". **You** set it to say "nothing here".

**Code Example:**
```js
let a;
console.log(a);      // undefined

let b = null;
console.log(b);      // null

console.log(null == undefined);  // true
console.log(null === undefined); // false
console.log(typeof undefined);   // "undefined"
console.log(typeof null);        // "object"
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** Saying they are the same. They are similar but different in type.

---

### 14. NaN and Infinity

**Simple Definition:**
- `NaN` means "Not a Number". You get it when a math operation makes no sense (like `"abc" * 2`). Its type is still `number`.
- `Infinity` is a number bigger than any number. You get it by dividing by zero.

**Code Example:**
```js
console.log("abc" * 2);   // NaN
console.log(typeof NaN);  // "number"
console.log(NaN === NaN); // false (weird!)
console.log(Number.isNaN(NaN)); // true
console.log(10 / 0);      // Infinity
console.log(-10 / 0);     // -Infinity
```

**Interview Angle:** ⭐ High
- **Common confusion:** `NaN` is not equal to itself. Use `Number.isNaN()`. The older `isNaN("hello")` returns `true` because it converts first, which can mislead you.

---

### 15. Conditional Statements

**Simple Definition:**
Conditions let your code **make decisions**: "If this is true, do that; otherwise do something else."
Types: `if`, `else if`, `else`, `switch`, and the ternary `? :`.

**Code Example:**
```js
let marks = 72;

if (marks >= 80) {
  console.log("Grade A");
} else if (marks >= 60) {
  console.log("Grade B");
} else {
  console.log("Grade C");
}

// switch
let day = 2;
switch (day) {
  case 1: console.log("Mon"); break;
  case 2: console.log("Tue"); break;
  default: console.log("Other");
}
```

**Interview Angle:** 🙂 Medium
- **Common confusion:** Forgetting `break` in `switch`. Without it, code "falls through" and runs the next cases too.

---

### 16. Loops: for, while, do...while

**Simple Definition:**
A loop repeats code again and again.
- `for` – use when you know how many times.
- `while` – repeat as long as a condition is true.
- `do...while` – runs **at least once**, then checks the condition.

**Code Example:**
```js
for (let i = 1; i <= 3; i++) {
  console.log(i);          // 1, 2, 3
}

let n = 3;
while (n > 0) {
  console.log(n);          // 3, 2, 1
  n--;
}

let k = 10;
do {
  console.log(k);          // prints 10 once
} while (k < 5);
```

**Interview Angle:** 🙂 Medium
- **Common confusion:** Infinite loops (forgetting to change the counter). Also: `do...while` always runs once, even if the condition is false.

---

### 17. break and continue

**Simple Definition:**
- `break` = stop the loop completely.
- `continue` = skip this round only, and go to the next round.

**Code Example:**
```js
for (let i = 1; i <= 5; i++) {
  if (i === 3) continue;  // skip 3
  if (i === 5) break;     // stop at 5
  console.log(i);         // 1, 2, 4
}
```

**Interview Angle:** 🙂 Medium
- **Common confusion:** `break` and `continue` do **not** work inside `forEach`. (Use a normal `for` loop or `some()`/`every()`.)

---

### 18. Functions and Function Declarations

**Simple Definition:**
A function is a **reusable block of code** with a name. You write it once and use it many times. A *function declaration* is the normal way to write one using the `function` keyword.

**Code Example:**
```js
function greet(name) {
  return "Hello, " + name;
}

console.log(greet("Asha")); // Hello, Asha
console.log(greet("Ravi")); // Hello, Ravi
```

**Interview Angle:** 🔥 Very High
- Key fact: function declarations are **hoisted**, so you can call them before they are written.
```js
sayHi();            // works!
function sayHi() { console.log("Hi"); }
```

---

### 19. Function Expressions

**Simple Definition:**
A function expression means you create a function and **store it in a variable**. The function can be nameless.

**Code Example:**
```js
const add = function (a, b) {
  return a + b;
};
console.log(add(2, 3)); // 5
```

**Interview Angle:** ⭐ High
- Difference from declaration: function expressions are **not** fully hoisted. Calling them before the line gives an error.
```js
// hello();   // ERROR if hello is const/let
const hello = function () { console.log("Hello"); };
```

---

### 20. Arrow Functions

**Simple Definition:**
Arrow functions are a **shorter way** to write functions using `=>`. They are great for small functions. They also behave differently with `this` (see topic 63).

**Code Example:**
```js
const add = (a, b) => a + b;        // one line, auto return
const square = x => x * x;          // one parameter, no brackets needed
const greet = () => "Hello";        // no parameters

const full = (a, b) => {            // multi-line needs return
  const sum = a + b;
  return sum;
};
```

**Interview Angle:** 🔥 Very High
- Key differences from normal functions: no own `this`, no `arguments`, cannot be used with `new`.
- **Common confusion:** Returning an object needs brackets: `() => ({ name: "Sam" })`.

---

### 21. Parameters, Arguments and Return Values

**Simple Definition:**
- **Parameters** = the names in the function definition (empty slots).
- **Arguments** = the real values you pass when calling.
- **Return** = the value the function gives back. If there is no `return`, you get `undefined`.

**Code Example:**
```js
function multiply(a, b) {   // a, b = parameters
  return a * b;
}
let result = multiply(4, 5); // 4, 5 = arguments
console.log(result);         // 20

function noReturn() { }
console.log(noReturn());     // undefined
```

**Interview Angle:** ⭐ High
- **Common confusion:** Mixing up parameter vs argument. Also: code written after `return` never runs.

---

### 22. Default Parameters

**Simple Definition:**
You can give a parameter a **backup value**. It is used when no argument (or `undefined`) is passed.

**Code Example:**
```js
function greet(name = "Guest") {
  return "Hello, " + name;
}
console.log(greet());         // Hello, Guest
console.log(greet("Asha"));   // Hello, Asha
console.log(greet(null));     // Hello, null  (null does NOT trigger default)
```

**Interview Angle:** 🙂 Medium
- **Common confusion:** Only `undefined` triggers the default. `null`, `0` and `""` do not.

---

### 23. Rest Parameters

**Simple Definition:**
Rest (`...`) collects **many extra arguments into one array**. It is written in the function definition, and it must be the last parameter.

**Code Example:**
```js
function sum(...numbers) {
  return numbers.reduce((total, n) => total + n, 0);
}
console.log(sum(1, 2, 3, 4)); // 10
```

**Interview Angle:** ⭐ High
- Usually asked with spread: *Rest gathers things together; spread spreads things out.*

---

### 24. Spread Syntax

**Simple Definition:**
Spread (`...`) **opens up** an array or object and puts its items out one by one. Used for copying, merging, and passing items to functions.

**Code Example:**
```js
const a = [1, 2];
const b = [3, 4];
const merged = [...a, ...b];        // [1, 2, 3, 4]
const copy = [...a];                // new array

const user = { name: "Sam" };
const updated = { ...user, age: 20 }; // { name: "Sam", age: 20 }

console.log(Math.max(...merged));   // 4
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** Same `...` symbol, two jobs. In a **function definition** it is *rest*; when **using/calling** it is *spread*.
- Spread makes only a **shallow copy** (see topic 50).

---

### 25. Template Literals

**Simple Definition:**
Template literals use **backticks** (`` ` ``) instead of quotes. They let you put variables inside a string using `${ }` and write text on multiple lines easily.

**Code Example:**
```js
const name = "Asha";
const age = 22;

console.log(`My name is ${name} and I am ${age} years old.`);
console.log(`Next year I will be ${age + 1}.`);

const text = `Line 1
Line 2`;   // multi-line string
```

**Interview Angle:** 🙂 Medium
- **Common confusion:** Using normal quotes `'${name}'` will not work. You must use backticks.

---

# Level 2: Arrays, Objects and Essential Methods

### 26. Arrays and Array Indexing

**Simple Definition:**
An array is a **list** that stores many values in one variable. Each item has a position number called an **index**. Counting starts from **0**, not 1.

**Code Example:**
```js
const fruits = ["apple", "banana", "mango"];
console.log(fruits[0]);      // "apple"
console.log(fruits[2]);      // "mango"
console.log(fruits.length);  // 3
console.log(fruits[5]);      // undefined (no such item)
console.log(fruits[fruits.length - 1]); // last item
console.log(fruits.at(-1));  // "mango" (also last item)
```

**Interview Angle:** ⭐ High
- **Common confusion:** `typeof []` is `"object"`. Use `Array.isArray()` to check.

---

### 27. Adding, Removing and Updating Array Elements

**Simple Definition:**
You can change an array after creating it: add items, remove items, or replace items by using their index.

**Code Example:**
```js
const nums = [1, 2, 3];
nums[1] = 20;          // update -> [1, 20, 3]
nums.push(4);          // add at end -> [1, 20, 3, 4]
nums.pop();            // remove from end -> [1, 20, 3]
nums.splice(1, 1);     // remove 1 item at index 1 -> [1, 3]
```

**Interview Angle:** 🙂 Medium
- **Common confusion:** Even if the array is `const`, you can still change its items.

---

### 28. Array Destructuring

**Simple Definition:**
Destructuring is a short way to **take items out of an array** and store them in separate variables in one line.

**Code Example:**
```js
const colors = ["red", "green", "blue"];
const [first, second] = colors;
console.log(first, second);  // red green

const [a, , c] = colors;     // skip the middle one
console.log(a, c);           // red blue

const [x = 0, y = 0] = [5];  // default values
console.log(x, y);           // 5 0

let p = 1, q = 2;
[p, q] = [q, p];             // swap values
```

**Interview Angle:** ⭐ High
- Commonly used for swapping variables.
- **Common confusion:** In arrays, **order matters**. In objects, **names** matter.

---

### 29. Array Methods: push, pop, shift, unshift

**Simple Definition:**
These four add or remove items at the ends of an array:
- `push` – add at the **end**
- `pop` – remove from the **end**
- `shift` – remove from the **start**
- `unshift` – add at the **start**

**Code Example:**
```js
const arr = [2, 3];
arr.push(4);     // [2, 3, 4]
arr.pop();       // [2, 3]
arr.unshift(1);  // [1, 2, 3]
arr.shift();     // [2, 3]
```

**Interview Angle:** ⭐ High
- They **change the original array** (mutating).
- `push` and `unshift` return the **new length**; `pop` and `shift` return the **removed item**.
- `shift`/`unshift` are slower for big arrays because every item moves.

---

### 30. slice() vs splice()

**Simple Definition:**
- `slice(start, end)` – **copies** a part of the array. Original is **not** changed. The end index is **not included**.
- `splice(start, deleteCount, ...newItems)` – **removes/adds** items in the original array. Original **is changed**.

**Code Example:**
```js
const arr = [1, 2, 3, 4, 5];

console.log(arr.slice(1, 3)); // [2, 3]
console.log(arr);             // [1, 2, 3, 4, 5]  (unchanged)

arr.splice(1, 2);             // remove 2 items from index 1
console.log(arr);             // [1, 4, 5]

arr.splice(1, 0, "x");        // add "x" at index 1
console.log(arr);             // [1, "x", 4, 5]
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** The names look similar. Remember: **sp**lice = **sp**oils the original. Slice = safe.

---

### 31. map()

**Simple Definition:**
`map()` goes through every item, does something to each one, and returns a **new array** of the same length. It does not change the original.

**Code Example:**
```js
const nums = [1, 2, 3];
const doubled = nums.map(n => n * 2);
console.log(doubled); // [2, 4, 6]
console.log(nums);    // [1, 2, 3]
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** Forgetting to `return` inside map (when using `{ }`) gives an array of `undefined`.

---

### 32. filter()

**Simple Definition:**
`filter()` keeps **only the items that pass a test** and returns them in a new array.

**Code Example:**
```js
const ages = [12, 18, 25, 9];
const adults = ages.filter(age => age >= 18);
console.log(adults); // [18, 25]
```

**Interview Angle:** 🔥 Very High
- The new array can be shorter than the original (or empty `[]`).
- **Common confusion:** `filter` returns an **array** even if only one item matches. To get a single item use `find()`.

---

### 33. reduce()

**Simple Definition:**
`reduce()` goes through all items and **combines them into one single value** (a total, an object, an array...). You keep a "running result" called the accumulator.

**Code Example:**
```js
const nums = [1, 2, 3, 4];
const total = nums.reduce((sum, n) => sum + n, 0);
console.log(total); // 10

// count how many times each word appears
const words = ["a", "b", "a"];
const count = words.reduce((obj, w) => {
  obj[w] = (obj[w] || 0) + 1;
  return obj;
}, {});
console.log(count); // { a: 2, b: 1 }
```

**Interview Angle:** 🔥 Very High
- The **second argument (starting value, `0` here)** is important. Without it, the first item is used as the start, and an empty array will throw an error.
- Most beginners find it hard, so it is a favourite of interviewers.

---

### 34. find() and findIndex()

**Simple Definition:**
- `find()` returns the **first item** that matches. If none, `undefined`.
- `findIndex()` returns the **position** of the first match. If none, `-1`.

**Code Example:**
```js
const users = [{ id: 1, name: "A" }, { id: 2, name: "B" }];
console.log(users.find(u => u.id === 2));      // { id: 2, name: "B" }
console.log(users.findIndex(u => u.id === 2)); // 1
console.log(users.find(u => u.id === 9));      // undefined
```

**Interview Angle:** ⭐ High
- **Common confusion:** `find` stops at the first match. `filter` checks everything.

---

### 35. some() and every()

**Simple Definition:**
- `some()` → is **at least one** item passing the test? (true/false)
- `every()` → do **all** items pass the test? (true/false)

**Code Example:**
```js
const nums = [2, 4, 5];
console.log(nums.some(n => n % 2 !== 0));  // true  (5 is odd)
console.log(nums.every(n => n % 2 === 0)); // false (5 is odd)
console.log([].every(n => n > 5));         // true  (empty array!)
```

**Interview Angle:** 🙂 Medium
- **Common confusion:** `every()` on an empty array returns `true`; `some()` on an empty array returns `false`.

---

### 36. includes(), indexOf() and join()

**Simple Definition:**
- `includes(x)` – does the array contain x? Gives true/false.
- `indexOf(x)` – gives the position of x, or `-1` if not found.
- `join(separator)` – joins all items into one **string**.

**Code Example:**
```js
const fruits = ["apple", "banana"];
console.log(fruits.includes("apple"));  // true
console.log(fruits.indexOf("banana"));  // 1
console.log(fruits.indexOf("grape"));   // -1
console.log(fruits.join(" - "));        // "apple - banana"
console.log([NaN].includes(NaN));       // true
console.log([NaN].indexOf(NaN));        // -1
```

**Interview Angle:** ⭐ High
- **Common confusion:** `includes` can find `NaN`, `indexOf` cannot.

---

### 37. sort() and reverse()

**Simple Definition:**
- `sort()` arranges items in order. By default it sorts as **text (strings)**, not as numbers!
- `reverse()` flips the order.
Both **change the original array**.

**Code Example:**
```js
const nums = [10, 9, 1, 100];
nums.sort();
console.log(nums);   // [1, 10, 100, 9]  (wrong for numbers!)

nums.sort((a, b) => a - b);
console.log(nums);   // [1, 9, 10, 100]  (small to big)

nums.sort((a, b) => b - a);
console.log(nums);   // [100, 10, 9, 1]  (big to small)

[1, 2, 3].reverse(); // [3, 2, 1]
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** Default `sort()` on numbers gives a surprising result. Always pass `(a, b) => a - b`.
- Newer methods `toSorted()` and `toReversed()` give a new array without changing the original.

---

### 38. Chaining Array Methods

**Simple Definition:**
Chaining means calling one method after another, where each one works on the result of the previous. It makes code short and readable.

**Code Example:**
```js
const prices = [100, 200, 300, 400];

const result = prices
  .filter(p => p > 150)     // [200, 300, 400]
  .map(p => p * 0.9)        // [180, 270, 360]
  .reduce((sum, p) => sum + p, 0);

console.log(result); // 810
```

**Interview Angle:** ⭐ High
- **Common confusion:** You can chain only methods that **return an array** (`map`, `filter`, `sort`...). You cannot chain after `forEach` (it returns `undefined`).

---

### 39. forEach() vs map()

**Simple Definition:**
- `forEach()` – just **does something** for each item (like printing). Returns **nothing** (`undefined`).
- `map()` – **creates a new array** from the results.

**Code Example:**
```js
const nums = [1, 2, 3];

nums.forEach(n => console.log(n));   // prints 1 2 3

const squares = nums.map(n => n * n);
console.log(squares);                // [1, 4, 9]
```

**Interview Angle:** 🔥 Very High
- Rule: **Need a new array? Use `map`. Just doing an action? Use `forEach`.**
- `forEach` cannot be stopped with `break`.

---

### 40. Objects and Properties

**Simple Definition:**
An object stores data as **key–value pairs**, like a real-world item with details. Each detail is called a **property**.

**Code Example:**
```js
const person = {
  name: "Asha",
  age: 22,
  isStudent: true
};
console.log(person.name);  // "Asha"
console.log(person.age);   // 22
```

**Interview Angle:** ⭐ High
- **Common confusion:** Object keys are always strings (or symbols), even if you write numbers.

---

### 41. Dot Notation vs Bracket Notation

**Simple Definition:**
Two ways to read a property:
- **Dot:** `obj.name` – simple, when you know the name.
- **Bracket:** `obj["name"]` – needed when the key is stored in a variable, has spaces, or special characters.

**Code Example:**
```js
const user = { name: "Sam", "favorite color": "blue" };

console.log(user.name);               // "Sam"
console.log(user["favorite color"]);  // "blue"

const key = "name";
console.log(user[key]);               // "Sam"
console.log(user.key);                // undefined (looks for a property called "key")
```

**Interview Angle:** ⭐ High
- **Common confusion:** `user.key` and `user[key]` are NOT the same thing.

---

### 42. Adding, Updating and Deleting Properties

**Simple Definition:**
Objects can be changed after creation. Assign to add or update. Use `delete` to remove.

**Code Example:**
```js
const car = { brand: "Tata" };
car.color = "red";       // add
car.brand = "Honda";     // update
delete car.color;        // remove
console.log(car);        // { brand: "Honda" }
console.log("brand" in car);       // true
console.log(car.hasOwnProperty("brand")); // true
```

**Interview Angle:** 🙂 Medium
- **Common confusion:** `const` objects can still be changed this way.

---

### 43. Object Methods and Method Shorthand

**Simple Definition:**
When a property holds a **function**, it is called a **method**. A shorter way to write it is the *method shorthand*.

**Code Example:**
```js
const person = {
  name: "Asha",
  sayHi: function () {         // normal way
    return "Hi " + this.name;
  },
  sayBye() {                   // shorthand
    return "Bye " + this.name;
  }
};
console.log(person.sayHi());   // Hi Asha
console.log(person.sayBye());  // Bye Asha
```

**Interview Angle:** ⭐ High
- **Common confusion:** Don't use arrow functions for object methods when you need `this`. Arrow functions don't have their own `this`.

---

### 44. Object Destructuring

**Simple Definition:**
Take out properties from an object into variables using **the same names** as the keys.

**Code Example:**
```js
const user = { name: "Asha", age: 22, city: "Pune" };

const { name, age } = user;
console.log(name, age);          // Asha 22

const { city: town } = user;     // rename
console.log(town);               // Pune

const { country = "India" } = user; // default value
console.log(country);            // India

function show({ name, age }) {   // in function parameters
  console.log(name, age);
}
show(user);
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** Names must match the keys. Order does not matter.

---

### 45. Shorthand Properties and Computed Property Names

**Simple Definition:**
- **Shorthand:** If the variable name equals the key name, write it once.
- **Computed names:** Use `[ ]` to build a key name from a variable or expression.

**Code Example:**
```js
const name = "Sam";
const age = 20;
const user = { name, age };      // same as { name: name, age: age }

const field = "email";
const data = { [field]: "a@b.com", ["id" + 1]: 101 };
console.log(data); // { email: "a@b.com", id1: 101 }
```

**Interview Angle:** 🙂 Medium
- Often shows up in React-style code, e.g. `setForm({ ...form, [e.target.name]: e.target.value })`.

---

### 46. Object.keys(), Object.values(), Object.entries()

**Simple Definition:**
Three helpers to turn an object into an array:
- `Object.keys(obj)` → all **keys**
- `Object.values(obj)` → all **values**
- `Object.entries(obj)` → pairs of `[key, value]`

**Code Example:**
```js
const person = { name: "Asha", age: 22 };

console.log(Object.keys(person));    // ["name", "age"]
console.log(Object.values(person));  // ["Asha", 22]
console.log(Object.entries(person)); // [["name","Asha"],["age",22]]

for (const [key, value] of Object.entries(person)) {
  console.log(key, value);
}
```

**Interview Angle:** 🔥 Very High
- Used to loop over objects. You cannot use `map` directly on an object, so convert it first.

---

### 47. Object.assign() and Object Spread

**Simple Definition:**
Both **copy/merge** objects into a new or existing object. Spread (`...`) is the modern, easier way.

**Code Example:**
```js
const a = { x: 1 };
const b = { y: 2 };

const merged1 = Object.assign({}, a, b); // { x: 1, y: 2 }
const merged2 = { ...a, ...b };          // { x: 1, y: 2 }

const updated = { ...a, x: 99 };         // later values win
console.log(updated);                    // { x: 99 }
```

**Interview Angle:** ⭐ High
- **Common confusion:** `Object.assign(a, b)` **changes `a`**. Use `{}` as the first argument to avoid that.
- Both make **shallow copies** only.

---

### 48. Optional Chaining (?.)

**Simple Definition:**
`?.` lets you safely read a deep property. If something on the way is `null` or `undefined`, it **stops and gives `undefined`** instead of crashing.

**Code Example:**
```js
const user = { name: "Sam" };

// console.log(user.address.city);  // ERROR: cannot read 'city' of undefined
console.log(user.address?.city);    // undefined (no error)
console.log(user.greet?.());        // undefined (method may not exist)
console.log(user.list?.[0]);        // undefined
```

**Interview Angle:** ⭐ High
- **Common confusion:** It only protects against `null`/`undefined`, not other errors.

---

### 49. Nullish Coalescing (??) vs ||

**Simple Definition:**
Both give a backup value.
- `||` uses the backup if the left side is **any falsy value** (`0`, `""`, `false`, ...).
- `??` uses the backup **only if the left side is `null` or `undefined`**.

**Code Example:**
```js
const count = 0;
console.log(count || 10);  // 10  (0 is falsy, so backup used — maybe wrong!)
console.log(count ?? 10);  // 0   (0 is a real value, so kept)

const name = "";
console.log(name || "Guest"); // "Guest"
console.log(name ?? "Guest"); // ""
```

**Interview Angle:** ⭐ High
- Use `??` when `0`, `""` or `false` are valid values.

---

### 50. Shallow Copy vs Deep Copy

**Simple Definition:**
- **Shallow copy:** copies only the **top layer**. Inner objects are still shared with the original.
- **Deep copy:** copies **everything**, including inner objects. Nothing is shared.

**Code Example:**
```js
const original = { name: "Sam", address: { city: "Pune" } };

const shallow = { ...original };
shallow.address.city = "Delhi";
console.log(original.address.city); // "Delhi"  (original also changed!)

const deep = structuredClone(original);
deep.address.city = "Mumbai";
console.log(original.address.city); // "Delhi"  (safe)
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** Thinking spread `{...obj}` or `[...arr]` makes a deep copy. It does not.

---

### 51. Reference Sharing and Mutation

**Simple Definition:**
*Mutation* means changing the original data. Because objects and arrays are shared by reference, changing one variable can change another one you did not expect.

**Code Example:**
```js
const a = [1, 2, 3];
const b = a;        // same array, not a copy
b.push(4);
console.log(a);     // [1, 2, 3, 4]

function addItem(list) {
  list.push("new");   // changes the original!
}
const myList = ["x"];
addItem(myList);
console.log(myList);  // ["x", "new"]
```

**Interview Angle:** 🔥 Very High
- Frequent in output questions and in React bugs.
- Fix: make a copy first (`[...a]`, `{...obj}`) and change the copy.

---

### 52. structuredClone() and JSON-Based Cloning Limitations

**Simple Definition:**
Two common ways to make a deep copy:
1. `structuredClone(obj)` – modern and built in. Best choice.
2. `JSON.parse(JSON.stringify(obj))` – old trick, but it loses some data.

**Code Example:**
```js
const data = {
  name: "Sam",
  date: new Date(),
  fn: () => "hi",
  nothing: undefined
};

const viaJSON = JSON.parse(JSON.stringify(data));
console.log(viaJSON);
// { name: "Sam", date: "2026-..." (now a STRING), }
// fn and undefined are LOST

const viaClone = structuredClone({ name: "Sam", date: new Date() });
console.log(viaClone.date instanceof Date); // true

// structuredClone cannot copy functions (throws an error)
```

**Interview Angle:** ⭐ High
- JSON method problems: loses functions, `undefined`, and `Symbol`; turns `Date` into a string; fails on circular references.
- `structuredClone` keeps dates, Maps, Sets, but cannot copy functions.

---

# Level 3: Scope, Hoisting and Execution

### 53. Global, Function and Block Scope

**Simple Definition:**
Scope means **where a variable can be used**.
- **Global scope:** written outside everything. Usable anywhere.
- **Function scope:** created inside a function. Usable only inside it.
- **Block scope:** created inside `{ }` (like `if` or `for`). `let` and `const` stay inside; `var` ignores blocks.

**Code Example:**
```js
let globalVar = "I am global";

function test() {
  let inside = "I am inside the function";
  console.log(globalVar); // works
}
// console.log(inside);   // ERROR

if (true) {
  let a = 1;
  var b = 2;
}
// console.log(a);        // ERROR
console.log(b);           // 2  (var leaks out of the block)
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** `var` does not respect block scope. `let` and `const` do.

---

### 54. Lexical Scope

**Simple Definition:**
"Lexical" means *where you wrote the code*. An inner function can use variables of the outer function **because of where it is written**, not where it is called.

**Code Example:**
```js
function outer() {
  let message = "Hello";
  function inner() {
    console.log(message); // can see outer's variable
  }
  inner();
}
outer(); // Hello
```

**Interview Angle:** ⭐ High
- Core idea behind closures.
- **Common confusion:** Scope is decided by where the function is **written**, not where it is **called**.

---

### 55. Scope Chain

**Simple Definition:**
When JavaScript looks for a variable, it first checks the current scope. If not found, it goes **one level outward**, again and again, until the global scope. If still not found, you get an error. This path is the scope chain.

**Code Example:**
```js
let a = "global";

function one() {
  let b = "one";
  function two() {
    let c = "two";
    console.log(a, b, c); // finds all three by going outward
  }
  two();
}
one();
```

**Interview Angle:** ⭐ High
- **Common confusion:** The chain only goes **outward**, never inward. An outer function cannot see an inner function's variables.

---

### 56. Hoisting

**Simple Definition:**
Before running code, JavaScript quietly "lifts" declarations to the top of their scope. So you can sometimes use things before the line where they are written.
- `function` declarations: fully hoisted (can call early).
- `var`: hoisted but value is `undefined` until its line runs.
- `let` / `const`: hoisted but **cannot be used** before the line (error).

**Code Example:**
```js
console.log(x);   // undefined (not an error)
var x = 5;

sayHi();          // works
function sayHi() { console.log("Hi"); }

// console.log(y); // ERROR
let y = 10;
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** Hoisting does not move your code. Only the *declaration* is known early; the *value* stays where you wrote it.

---

### 57. Temporal Dead Zone (TDZ)

**Simple Definition:**
The TDZ is the "danger area" between the start of a scope and the line where a `let`/`const` is declared. Using the variable in this area causes an error.

**Code Example:**
```js
{
  // TDZ starts here for 'name'
  // console.log(name);  // ReferenceError
  let name = "Asha";     // TDZ ends here
  console.log(name);     // works
}
```

**Interview Angle:** ⭐ High
- **Common confusion:** People say `let` is "not hoisted". In truth it **is** hoisted, but stays unusable inside the TDZ.

---

### 58. Execution Context

**Simple Definition:**
An execution context is the **work area** JavaScript creates to run code. It holds the variables and tells which `this` to use. There is one **global** context at the start, and a new **function** context is created every time a function is called.

Each context has two phases:
1. **Creation phase:** variables and functions are set up (hoisting happens here).
2. **Execution phase:** code runs line by line.

**Code Example:**
```js
var n = 2;                 // global context
function square(num) {     // new context made when called
  return num * num;
}
var result = square(n);
```

**Interview Angle:** ⭐ High
- **Common confusion:** Not knowing that hoisting happens in the *creation phase*.

---

### 59. Call Stack

**Simple Definition:**
The call stack is a **to-do pile** of function calls. When a function is called, it is put on top. When it finishes, it is removed. JavaScript always works on the top one. Last in, first out.

**Code Example:**
```js
function a() { b(); }
function b() { c(); }
function c() { console.log("done"); }
a();
// Stack: a -> b -> c, then c finishes, b finishes, a finishes
```

**Interview Angle:** ⭐ High
- A function that keeps calling itself forever causes **"Maximum call stack size exceeded"** (stack overflow).

---

### 60. Lexical Environment

**Simple Definition:**
A lexical environment is a **box that stores variables of a scope**, plus a link to the box of the outer scope. This link is how the scope chain and closures work.

**Code Example:**
```js
function outer() {
  let x = 1;           // stored in outer's environment
  function inner() {
    console.log(x);    // inner's environment links to outer's
  }
  inner();
}
```

**Interview Angle:** 💤 Low–Medium
- Usually asked together with closures: *"A closure is a function plus its lexical environment."*

---

### 61. this Keyword

**Simple Definition:**
`this` means **"who is calling me / who owns this code right now"**. Its value is not fixed. It depends on **how the function is called**.

**Code Example:**
```js
const person = {
  name: "Asha",
  show() {
    console.log(this.name);
  }
};
person.show();   // "Asha"  (this = person, the object before the dot)
```

**Interview Angle:** 🔥 Very High
- Easy rule: look at the left side of the dot at call time. `person.show()` → `this` is `person`.
- **Common confusion:** Thinking `this` depends on where the function is *written*. (That is true only for arrow functions.)

---

### 62. this in Global and Regular Functions

**Simple Definition:**
- In the global area: `this` is `window` (browser).
- In a plain function call: `this` is `window` (or `undefined` in strict mode).
- In an object method: `this` is the object.
- If you pull a method out of an object, it **loses** its `this`.

**Code Example:**
```js
function show() {
  console.log(this);
}
show();   // window (or undefined in strict mode)

const user = {
  name: "Sam",
  hello() { console.log(this.name); }
};
user.hello();            // "Sam"

const fn = user.hello;
fn();                    // undefined (this lost!)
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** Assigning a method to a variable and calling it loses `this`. This is a famous bug.

---

### 63. this in Arrow Functions

**Simple Definition:**
Arrow functions do **not** have their own `this`. They borrow `this` from the place where they were **written** (the outer code).

**Code Example:**
```js
const person = {
  name: "Asha",
  regular() {
    setTimeout(function () {
      console.log(this.name);   // undefined (this is window)
    }, 100);
  },
  arrow() {
    setTimeout(() => {
      console.log(this.name);   // "Asha" (borrowed from arrow())
    }, 100);
  }
};
person.regular();
person.arrow();
```

**Interview Angle:** 🔥 Very High
- Arrow functions are great inside callbacks, but bad as **object methods**.
```js
const obj = { name: "Sam", hi: () => console.log(this.name) };
obj.hi();  // undefined (arrow does not use obj as this)
```

---

### 64. call(), apply() and bind()

**Simple Definition:**
Three tools to **choose what `this` is** for a function.
- `call(thisValue, a, b)` – runs the function right now, arguments one by one.
- `apply(thisValue, [a, b])` – runs right now, arguments in an **array**.
- `bind(thisValue)` – does **not** run now. Returns a **new function** with `this` fixed.

**Code Example:**
```js
function intro(city, country) {
  console.log(`${this.name} from ${city}, ${country}`);
}
const person = { name: "Asha" };

intro.call(person, "Pune", "India");     // runs now
intro.apply(person, ["Pune", "India"]);  // runs now
const later = intro.bind(person, "Pune", "India");
later();                                 // runs when you call it
```

**Interview Angle:** 🔥 Very High
- Memory trick: **A**pply = **A**rray. **B**ind = **B**ack later.

---

### 65. Function Borrowing

**Simple Definition:**
Function borrowing means **using a method of one object on another object**, using `call` or `apply`.

**Code Example:**
```js
const person1 = {
  name: "Asha",
  greet() { return "Hi, I am " + this.name; }
};
const person2 = { name: "Ravi" };

console.log(person1.greet.call(person2)); // "Hi, I am Ravi"

// Borrowing array method for array-like data
function listArgs() {
  return Array.prototype.slice.call(arguments);
}
```

**Interview Angle:** 🙂 Medium
- Often a follow-up to `call/apply/bind`.

---

### 66. Closures

**Simple Definition:**
A closure happens when an inner function **remembers the variables of its outer function**, even after the outer function has finished running. Like a backpack that carries the variables with it.

**Code Example:**
```js
function counter() {
  let count = 0;
  return function () {
    count++;
    return count;
  };
}

const c1 = counter();
console.log(c1()); // 1
console.log(c1()); // 2
console.log(c1()); // 3  (remembers count)

const c2 = counter();
console.log(c2()); // 1  (separate backpack)
```

**Interview Angle:** 🔥 Very High (one of the top questions)
- Famous trap:
```js
for (var i = 1; i <= 3; i++) {
  setTimeout(() => console.log(i), 100);
}
// prints 4 4 4  (var shares one i)
// Fix: use let instead of var -> prints 1 2 3
```

---

### 67. Practical Applications of Closures

**Simple Definition:**
Where closures are used in real life:
1. **Private data** (hide variables from outside)
2. **Counters** and "remember something" logic
3. **Function factories**
4. **Callbacks and event handlers**
5. **Debounce, throttle, memoization**

**Code Example:**
```js
// 1. Private data
function bankAccount() {
  let balance = 0;               // cannot be touched from outside
  return {
    deposit(x) { balance += x; },
    getBalance() { return balance; }
  };
}
const acc = bankAccount();
acc.deposit(100);
console.log(acc.getBalance());   // 100
console.log(acc.balance);        // undefined

// 2. Function factory
function multiplier(n) {
  return x => x * n;
}
const double = multiplier(2);
console.log(double(5));          // 10
```

**Interview Angle:** ⭐ High
- Always give one real example after the definition.

---

### 68. IIFE (Immediately Invoked Function Expression)

**Simple Definition:**
An IIFE is a function that **runs immediately** the moment it is created. It is wrapped in brackets and followed by `()`. It is used to create a private area and avoid polluting global variables.

**Code Example:**
```js
(function () {
  let secret = "hidden";
  console.log("Runs right away!");
})();

(() => console.log("Arrow IIFE"))();
```

**Interview Angle:** 🙂 Medium
- **Common confusion:** The extra brackets around the function are needed; without them it's a syntax error.

---

### 69. First-Class Functions

**Simple Definition:**
In JavaScript, functions are treated like **normal values**. You can store them in variables, pass them to other functions, and return them from functions.

**Code Example:**
```js
const sayHi = function () { return "Hi"; };      // stored in variable

function run(fn) { return fn(); }                // passed as argument
console.log(run(sayHi));                         // "Hi"

function make() { return () => "Made!"; }        // returned from function
console.log(make()());                           // "Made!"
```

**Interview Angle:** ⭐ High
- Simple answer: *"Functions can be used like any other value."*

---

### 70. Higher-Order Functions

**Simple Definition:**
A higher-order function is a function that **takes another function as input, or returns a function** (or both). `map`, `filter`, `reduce` are all higher-order functions.

**Code Example:**
```js
function repeat(times, action) {
  for (let i = 0; i < times; i++) action(i);
}
repeat(3, i => console.log("Round", i));

[1, 2, 3].map(n => n * 2);   // map is higher-order
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** The *function you pass in* is the "callback". The function that *receives* it is the "higher-order function".

---

### 71. Callback Functions

**Simple Definition:**
A callback is a function you **give to another function** so that it can be called **later**, when the work is done or an event happens.

**Code Example:**
```js
function doTask(name, callback) {
  console.log("Doing " + name);
  callback();
}
doTask("homework", () => console.log("Finished!"));

setTimeout(() => console.log("After 1 sec"), 1000); // callback
```

**Interview Angle:** ⭐ High
- **Common confusion:** Pass the function itself (`callback`), don't call it (`callback()`), unless you want it to run right now.

---

### 72. Pure Functions vs Impure Functions

**Simple Definition:**
- **Pure:** same input always gives same output, and it changes nothing outside.
- **Impure:** depends on or changes something outside (global variables, time, random, API, DOM).

**Code Example:**
```js
// Pure
function add(a, b) { return a + b; }

// Impure
let total = 0;
function addToTotal(x) { total += x; }   // changes outside variable

function randomNum() { return Math.random(); }  // different each time
```

**Interview Angle:** ⭐ High
- Very common in React interviews. Pure = easy to test and predict.

---

### 73. Side Effects

**Simple Definition:**
A side effect is when a function **does something besides returning a value**, such as changing a global variable, changing its input, printing, saving data, or calling an API.

**Code Example:**
```js
let count = 0;
function increase() {
  count++;                      // side effect: changes outside variable
  console.log("Increased");     // side effect: printing
}

function addItem(arr) {
  arr.push(1);                  // side effect: changes the input array
}
```

**Interview Angle:** ⭐ High
- Side effects are not always bad; just keep them controlled.

---

### 74. Recursion

**Simple Definition:**
Recursion is when a function **calls itself** to solve a smaller piece of the same problem. It must have a **base case** (a stopping point), or it will never end.

**Code Example:**
```js
function factorial(n) {
  if (n <= 1) return 1;          // base case
  return n * factorial(n - 1);   // calls itself
}
console.log(factorial(5)); // 120

function countdown(n) {
  if (n === 0) return;
  console.log(n);
  countdown(n - 1);
}
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** Forgetting the base case → "Maximum call stack size exceeded".
- Popular problems: factorial, fibonacci, sum of array, flatten array.

---

# Level 4: DOM and Browser JavaScript

### 75. DOM Fundamentals

**Simple Definition:**
DOM stands for **Document Object Model**. When the browser loads a page, it turns the HTML into a **tree of objects**. JavaScript can use this tree to read, change, add or delete anything on the page.

**Code Example:**
```js
console.log(document.title);              // page title
document.body.style.background = "lightblue";
```

**Interview Angle:** ⭐ High
- **Common confusion:** The DOM is **not** your HTML file. It is the browser's live copy, which JavaScript can change.

---

### 76. Selecting Elements: querySelector() and getElementById()

**Simple Definition:**
These find elements on the page so you can work with them.
- `getElementById("id")` – finds one element by its id.
- `querySelector("css selector")` – finds the **first** match.
- `querySelectorAll("css selector")` – finds **all** matches.

**Code Example:**
```js
const title = document.getElementById("title");
const firstBtn = document.querySelector(".btn");
const allBtns = document.querySelectorAll(".btn");

allBtns.forEach(btn => console.log(btn.innerText));
```

**Interview Angle:** ⭐ High
- **Common confusion:** `querySelector` needs `#` for id and `.` for class: `"#title"`, `".btn"`. `getElementById` does **not** use `#`.
- If nothing is found, you get `null`.

---

### 77. Traversing the DOM

**Simple Definition:**
Traversing means **moving around** the DOM tree: going to the parent, children, or neighbours of an element.

**Code Example:**
```js
const item = document.querySelector("li");

item.parentElement;          // the parent
item.children;               // child elements
item.nextElementSibling;     // next neighbour
item.previousElementSibling; // previous neighbour
item.closest(".list");       // nearest parent that matches
```

**Interview Angle:** 🙂 Medium
- **Common confusion:** `children` gives only elements; `childNodes` also includes text and line breaks.

---

### 78. Changing Text, HTML and Attributes

**Simple Definition:**
- `textContent` / `innerText` – change plain text.
- `innerHTML` – change content including HTML tags.
- `setAttribute()` / `getAttribute()` – work with attributes like `src`, `href`.

**Code Example:**
```js
const box = document.querySelector("#box");
box.textContent = "New text";
box.innerHTML = "<b>Bold text</b>";

const img = document.querySelector("img");
img.setAttribute("src", "cat.png");
console.log(img.getAttribute("alt"));
```

**Interview Angle:** ⭐ High
- **Common confusion:** `innerHTML` with user input is **unsafe** (can allow attacks called XSS). Use `textContent` for plain text.

---

### 79. Manipulating CSS and Classes

**Simple Definition:**
You can change style directly, or better, **add/remove CSS classes**.

**Code Example:**
```js
const box = document.querySelector("#box");

box.style.color = "red";            // inline style
box.style.backgroundColor = "yellow"; // camelCase, not background-color

box.classList.add("active");
box.classList.remove("active");
box.classList.toggle("dark");       // add if missing, remove if present
console.log(box.classList.contains("dark"));
```

**Interview Angle:** 🙂 Medium
- **Common confusion:** In JS, CSS names use camelCase (`backgroundColor`).

---

### 80. Creating and Removing Elements

**Simple Definition:**
You can build new elements with JavaScript and add them to the page, or remove existing ones.

**Code Example:**
```js
const li = document.createElement("li");
li.textContent = "New item";
document.querySelector("ul").appendChild(li);   // add at end

document.querySelector("ul").prepend(li);       // add at start

li.remove();                                    // delete it
```

**Interview Angle:** ⭐ High
- **Common confusion:** `createElement` only makes the element in memory. It will not show until you add it to the page.

---

### 81. Event Handling

**Simple Definition:**
An event is something that happens on the page (click, key press, mouse move, form submit). Event handling means **running code when the event happens**.

**Code Example:**
```js
const btn = document.querySelector("#btn");

btn.addEventListener("click", function () {
  console.log("Button clicked!");
});

// remove a listener (needs the same function reference)
function handle() { console.log("hi"); }
btn.addEventListener("click", handle);
btn.removeEventListener("click", handle);
```

**Interview Angle:** 🔥 Very High
- Prefer `addEventListener` over `onclick`, because it allows many handlers on one element.

---

### 82. Event Object

**Simple Definition:**
When an event happens, the browser gives your function an **event object** with details: what was clicked, which key was pressed, mouse position, etc.

**Code Example:**
```js
document.addEventListener("click", function (event) {
  console.log(event.type);       // "click"
  console.log(event.target);     // element that was clicked
  console.log(event.clientX, event.clientY); // mouse position
});

input.addEventListener("keydown", e => console.log(e.key));
```

**Interview Angle:** ⭐ High
- **Common confusion:** `event.target` = the element that was really clicked; `event.currentTarget` = the element that has the listener.

---

### 83. Event Bubbling and Capturing

**Simple Definition:**
When you click an inner element, the event doesn't stop there.
- **Bubbling (default):** event travels **upward** from the clicked element to its parents.
- **Capturing:** event travels **downward** from the top to the clicked element first.

**Code Example:**
```html
<div id="parent"><button id="child">Click</button></div>
<script>
  parent.addEventListener("click", () => console.log("parent"));
  child.addEventListener("click", () => console.log("child"));
  // Click button prints: child, then parent (bubbling)

  // To use capturing, pass true:
  parent.addEventListener("click", () => console.log("parent capture"), true);
</script>
```

**Interview Angle:** 🔥 Very High
- Order: capturing (down) → target → bubbling (up).

---

### 84. Event Delegation

**Simple Definition:**
Instead of adding a listener on **every** child, add **one listener on the parent** and use bubbling to find which child was clicked. This is faster and also works for elements added later.

**Code Example:**
```js
document.querySelector("ul").addEventListener("click", function (e) {
  if (e.target.tagName === "LI") {
    console.log("Clicked:", e.target.textContent);
  }
});
```

**Interview Angle:** 🔥 Very High
- Benefits: less memory, works for dynamically added items.
- **Common confusion:** It works only because of bubbling.

---

### 85. preventDefault() vs stopPropagation()

**Simple Definition:**
- `preventDefault()` – stops the **browser's normal action** (e.g., form submit reload, link opening).
- `stopPropagation()` – stops the event from **travelling to parent elements**.

**Code Example:**
```js
form.addEventListener("submit", e => {
  e.preventDefault();       // page will not reload
  console.log("Handled by JS");
});

child.addEventListener("click", e => {
  e.stopPropagation();      // parent's click will not run
});
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** They do two different jobs. One stops the default action, the other stops bubbling.

---

### 86. Form Events and Form Validation

**Simple Definition:**
Forms have events like `submit`, `input`, `change`. **Validation** means checking that what the user typed is correct before using it.

**Code Example:**
```js
const form = document.querySelector("form");
const email = document.querySelector("#email");

form.addEventListener("submit", e => {
  e.preventDefault();
  if (email.value.trim() === "") {
    alert("Email is required");
    return;
  }
  console.log("Form OK");
});

email.addEventListener("input", () => console.log(email.value));
```

**Interview Angle:** 🙂 Medium
- **Common confusion:** Always validate on the server too; browser checks can be bypassed.

---

### 87. Keyboard and Mouse Events

**Simple Definition:**
- **Mouse:** `click`, `dblclick`, `mouseover`, `mouseout`, `mousemove`
- **Keyboard:** `keydown`, `keyup` (old `keypress` is outdated)

**Code Example:**
```js
document.addEventListener("keydown", e => {
  if (e.key === "Enter") console.log("Enter pressed");
});

box.addEventListener("mouseover", () => box.style.background = "pink");
box.addEventListener("mouseout", () => box.style.background = "");
```

**Interview Angle:** 🙂 Medium
- Use `event.key` (like `"Enter"`), the old `keyCode` is outdated.

---

### 88. Browser Events and the DOMContentLoaded Event

**Simple Definition:**
- `DOMContentLoaded` – fires when the HTML is fully read and the DOM is ready (images may still be loading).
- `load` – fires when **everything** (images, styles) has loaded.

**Code Example:**
```js
document.addEventListener("DOMContentLoaded", () => {
  console.log("DOM is ready");
});

window.addEventListener("load", () => {
  console.log("Everything loaded");
});
```

**Interview Angle:** ⭐ High
- **Common confusion:** `DOMContentLoaded` is earlier than `load`.
- If your script is at the end of `<body>` or uses `defer`, you may not need it.

---

### 89. Timers: setTimeout() and setInterval()

**Simple Definition:**
- `setTimeout(fn, ms)` – runs a function **once** after a delay.
- `setInterval(fn, ms)` – runs a function **again and again** every few milliseconds.
- Use `clearTimeout` / `clearInterval` to stop them.

**Code Example:**
```js
const t = setTimeout(() => console.log("Once after 2s"), 2000);
clearTimeout(t);   // cancel it

let n = 0;
const id = setInterval(() => {
  n++;
  console.log(n);
  if (n === 3) clearInterval(id);
}, 1000);
```

**Interview Angle:** 🔥 Very High
- `setTimeout(fn, 0)` does **not** run instantly. It runs after the current code finishes.
- **Common confusion:** The delay is the *minimum* wait, not exact.

---

### 90. Debouncing

**Simple Definition:**
Debouncing means: **wait until the user stops** doing something for a short time, then run the function once. Example: search box → call the API only after the user stops typing.

**Code Example:**
```js
function debounce(fn, delay) {
  let timer;
  return function (...args) {
    clearTimeout(timer);                        // cancel previous
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}

const search = debounce(text => console.log("Searching", text), 500);
input.addEventListener("input", e => search(e.target.value));
```

**Interview Angle:** 🔥 Very High
- Uses closures. Often asked as a coding question.

---

### 91. Throttling

**Simple Definition:**
Throttling means: **run the function at most once in a fixed time**, no matter how many times the event happens. Example: scroll or resize events.

**Code Example:**
```js
function throttle(fn, limit) {
  let waiting = false;
  return function (...args) {
    if (waiting) return;
    fn.apply(this, args);
    waiting = true;
    setTimeout(() => (waiting = false), limit);
  };
}

window.addEventListener("scroll", throttle(() => console.log("scroll"), 1000));
```

**Interview Angle:** 🔥 Very High
- **Difference (easy trick):**
  - Debounce = *wait until they stop*, then run once.
  - Throttle = *run regularly*, but not more than once per time limit.

---

### 92. Browser Storage: Local Storage and Session Storage

**Simple Definition:**
Places in the browser to **save small data** as text.
- `localStorage` – stays even after closing the browser.
- `sessionStorage` – cleared when the tab is closed.

**Code Example:**
```js
localStorage.setItem("theme", "dark");
console.log(localStorage.getItem("theme")); // "dark"
localStorage.removeItem("theme");
localStorage.clear();

// Saving an object: convert to text first
const user = { name: "Asha" };
localStorage.setItem("user", JSON.stringify(user));
const saved = JSON.parse(localStorage.getItem("user"));
```

**Interview Angle:** ⭐ High
- Stores **only strings**; use `JSON.stringify` and `JSON.parse` for objects.
- **Common confusion:** Don't store passwords or tokens carelessly; any script on the page can read it.

---

### 93. Cookies — Basics

**Simple Definition:**
Cookies are tiny pieces of data stored in the browser and **sent to the server with every request**. They are used for login sessions and remembering users.

**Code Example:**
```js
document.cookie = "username=Asha; max-age=3600; path=/";
console.log(document.cookie);   // "username=Asha"
```

**Interview Angle:** ⭐ High

| | Cookies | localStorage |
|---|---|---|
| Size | ~4 KB | ~5 MB |
| Sent to server | Yes, every request | No |
| Expiry | Can be set | Never expires |

- **Common confusion:** `HttpOnly` cookies cannot be read by JavaScript (safer for login tokens).

---

### 94. JSON: JSON.stringify() and JSON.parse()

**Simple Definition:**
JSON is a **text format for data** that looks like a JavaScript object.
- `JSON.stringify(obj)` – object → text (string)
- `JSON.parse(text)` – text → object

**Code Example:**
```js
const user = { name: "Asha", age: 22 };

const text = JSON.stringify(user);
console.log(text);            // '{"name":"Asha","age":22}'
console.log(typeof text);     // "string"

const obj = JSON.parse(text);
console.log(obj.name);        // "Asha"
```

**Interview Angle:** 🔥 Very High
- JSON keys must use **double quotes**. No functions or `undefined`.
- **Common confusion:** `JSON.parse` on invalid text throws an error; wrap it in `try...catch`.

---

### 95. ES Modules: import and export

**Simple Definition:**
Modules let you **split code into many files** and share things between them using `export` and `import`.

**Code Example:**
```js
// math.js
export const PI = 3.14;
export function add(a, b) { return a + b; }
export default function multiply(a, b) { return a * b; }

// app.js
import multiply, { PI, add } from "./math.js";
console.log(add(2, 3), PI, multiply(2, 3));
```
```html
<script type="module" src="app.js"></script>
```

**Interview Angle:** ⭐ High
- **Named export** (`{ }` needed on import, many per file) vs **default export** (one per file, any name).
- **Common confusion:** Forgetting `type="module"` in the script tag.

---

# Level 5: Asynchronous JavaScript

### 96. Synchronous vs Asynchronous JavaScript

**Simple Definition:**
- **Synchronous:** tasks run **one after another**. Each one waits for the previous one to finish.
- **Asynchronous:** slow tasks (like loading data) are **started and left to finish later**, so the rest of the code keeps running.

Think: synchronous = standing in a queue. Asynchronous = ordering food and getting a token, then doing other work until it's ready.

**Code Example:**
```js
console.log("1");
setTimeout(() => console.log("2"), 1000);
console.log("3");
// Output: 1, 3, 2
```

**Interview Angle:** 🔥 Very High
- JavaScript has **one thread** (does one thing at a time) but can still handle async tasks with the help of the browser and the event loop.

---

### 97. Blocking vs Non-Blocking Operations

**Simple Definition:**
- **Blocking:** the code **freezes everything** until it finishes (page stops responding).
- **Non-blocking:** the work happens in the background; other code continues.

**Code Example:**
```js
// Blocking: freezes the page for a few seconds
const start = Date.now();
while (Date.now() - start < 3000) { }

// Non-blocking: page stays smooth
setTimeout(() => console.log("Done"), 3000);
```

**Interview Angle:** ⭐ High
- **Common confusion:** Heavy loops block the page even in async code, since JavaScript only does one thing at a time.

---

### 98. Callback-Based Asynchronous Code

**Simple Definition:**
The oldest way to handle async work: pass a function (callback) that will run **when the task finishes**.

**Code Example:**
```js
function getUser(callback) {
  setTimeout(() => {
    callback({ name: "Asha" });
  }, 1000);
}

getUser(user => console.log(user.name)); // after 1s: "Asha"
```

**Interview Angle:** ⭐ High
- Leads to the next topic, callback hell.

---

### 99. Callback Hell

**Simple Definition:**
When many async tasks depend on each other, callbacks get **nested inside callbacks** again and again. The code becomes shaped like a pyramid and is hard to read and fix.

**Code Example:**
```js
getUser(function (user) {
  getOrders(user.id, function (orders) {
    getDetails(orders[0], function (details) {
      console.log(details);
      // and it keeps going deeper...
    });
  });
});
```

**Interview Angle:** ⭐ High
- Solution: use **Promises** or **async/await**.

---

### 100. Promises

**Simple Definition:**
A Promise is an object that says: *"I promise to give you a result later."* The result can be **success** or **failure**. It is a cleaner way to handle async work than callbacks.

**Code Example:**
```js
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    const ok = true;
    if (ok) resolve("Data received");
    else reject("Something went wrong");
  }, 1000);
});

promise
  .then(data => console.log(data))
  .catch(err => console.log(err));
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** `resolve` = success. `reject` = failure.

---

### 101. Promise States

**Simple Definition:**
A promise is always in one of three states:
1. **Pending** – still waiting.
2. **Fulfilled** – finished successfully (resolved).
3. **Rejected** – finished with an error.

Once it changes from pending, it **never changes again**.

**Code Example:**
```js
const p = new Promise(resolve => setTimeout(() => resolve("ok"), 1000));
console.log(p);               // Promise { <pending> }
p.then(() => console.log(p)); // Promise { "ok" } (fulfilled)
```

**Interview Angle:** ⭐ High
- **Common confusion:** Once settled (fulfilled/rejected), a promise cannot be changed.

---

### 102. .then(), .catch() and .finally()

**Simple Definition:**
- `.then(fn)` – runs when the promise **succeeds**.
- `.catch(fn)` – runs when it **fails**.
- `.finally(fn)` – runs **always**, success or failure (good for cleanup, like hiding a loader).

**Code Example:**
```js
fetch("https://api.example.com/data")
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => console.log("Error:", err))
  .finally(() => console.log("Done, hide loader"));
```

**Interview Angle:** ⭐ High
- `finally` does not receive any value.

---

### 103. Promise Chaining

**Simple Definition:**
Each `.then()` returns a **new promise**, so you can connect many steps one after another. The value you `return` goes to the next `.then()`.

**Code Example:**
```js
Promise.resolve(2)
  .then(n => n * 2)       // 4
  .then(n => n + 1)       // 5
  .then(n => console.log(n)); // 5
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** If you forget to `return` inside `.then()`, the next step gets `undefined`.

---

### 104. Promise Error Handling

**Simple Definition:**
Errors in a promise chain **skip all `.then()`** and go to the nearest `.catch()`. One `.catch()` at the end can handle errors from the whole chain.

**Code Example:**
```js
Promise.resolve(1)
  .then(() => { throw new Error("Oops"); })
  .then(() => console.log("skipped"))
  .catch(err => {
    console.log(err.message);   // "Oops"
    return "recovered";
  })
  .then(v => console.log(v));   // "recovered"
```

**Interview Angle:** ⭐ High
- **Common confusion:** After a `.catch()` the chain **continues** normally.
- Unhandled rejections show a console error.

---

### 105. Promise.all()

**Simple Definition:**
Runs **many promises at the same time** and waits for **all** to succeed. Gives an array of results in the same order. If **any one fails**, the whole thing fails.

**Code Example:**
```js
const p1 = Promise.resolve(1);
const p2 = new Promise(res => setTimeout(() => res(2), 500));
const p3 = Promise.resolve(3);

Promise.all([p1, p2, p3])
  .then(results => console.log(results)) // [1, 2, 3]
  .catch(err => console.log(err));
```

**Interview Angle:** 🔥 Very High
- Use when all results are needed. **Fail-fast** behaviour is the key point.

---

### 106. Promise.allSettled()

**Simple Definition:**
Waits for **all** promises to finish, whether they succeed or fail. Never fails. Gives a report for each one.

**Code Example:**
```js
Promise.allSettled([
  Promise.resolve("ok"),
  Promise.reject("error")
]).then(results => console.log(results));
// [
//   { status: "fulfilled", value: "ok" },
//   { status: "rejected", reason: "error" }
// ]
```

**Interview Angle:** ⭐ High
- Use when you want results of everything, even if some fail.

---

### 107. Promise.race()

**Simple Definition:**
Returns the result of the **first promise that finishes** (success **or** failure). The rest are ignored.

**Code Example:**
```js
const slow = new Promise(res => setTimeout(() => res("slow"), 2000));
const fast = new Promise(res => setTimeout(() => res("fast"), 500));

Promise.race([slow, fast]).then(v => console.log(v)); // "fast"
```

**Interview Angle:** ⭐ High
- Common use: add a **timeout** to a request.

---

### 108. Promise.any()

**Simple Definition:**
Returns the **first promise that succeeds**. Failures are ignored. If **all** fail, it fails with an `AggregateError`.

**Code Example:**
```js
Promise.any([
  Promise.reject("fail 1"),
  new Promise(res => setTimeout(() => res("success"), 500)),
  Promise.reject("fail 2")
]).then(v => console.log(v)); // "success"
```

**Interview Angle:** ⭐ High

| Method | Waits for | Fails when |
|---|---|---|
| `all` | all to succeed | any one fails |
| `allSettled` | all to finish | never |
| `race` | first to finish | first one is a failure |
| `any` | first success | all fail |

---

### 109. async and await

**Simple Definition:**
A simpler way to write promise code so it **looks like normal top-to-bottom code**.
- `async` before a function → it always returns a promise.
- `await` → pause *inside that function* until a promise finishes.

**Code Example:**
```js
async function getData() {
  const res = await fetch("https://api.example.com/users");
  const data = await res.json();
  console.log(data);
}
getData();
```

**Interview Angle:** 🔥 Very High
- `await` only pauses the async function, **not the whole program**.
- **Common confusion:** `await` can only be used inside an `async` function (or at the top level of modules).

---

### 110. Error Handling with try...catch

**Simple Definition:**
`try...catch` catches errors so your program doesn't crash. Put risky code in `try`; handle the problem in `catch`. `finally` always runs.

**Code Example:**
```js
async function load() {
  try {
    const res = await fetch("https://bad-url.example");
    const data = await res.json();
    console.log(data);
  } catch (error) {
    console.log("Something went wrong:", error.message);
  } finally {
    console.log("Always runs");
  }
}
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** `fetch` does **not** throw an error for HTTP errors like 404 or 500. Check `res.ok` yourself.

---

### 111. Sequential vs Parallel Asynchronous Execution

**Simple Definition:**
- **Sequential:** one task starts **after** the previous finishes. Slower.
- **Parallel:** all tasks start **together**. Faster, when tasks don't depend on each other.

**Code Example:**
```js
const wait = (ms, v) => new Promise(r => setTimeout(() => r(v), ms));

// Sequential: ~2 seconds
async function sequential() {
  const a = await wait(1000, "A");
  const b = await wait(1000, "B");
  return [a, b];
}

// Parallel: ~1 second
async function parallel() {
  return await Promise.all([wait(1000, "A"), wait(1000, "B")]);
}
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** Writing `await` for each independent call by mistake makes your code slow.

---

### 112. Event Loop

**Simple Definition:**
The event loop is a **manager that keeps checking**: "Is the call stack empty? If yes, take the next waiting task and run it." This is how JavaScript handles async work with only one thread.

**Code Example:**
```js
console.log("Start");
setTimeout(() => console.log("Timeout"), 0);
console.log("End");
// Start, End, Timeout
```

**Interview Angle:** 🔥 Very High (top question)
- Explain simply: *"Async tasks wait in a queue. The event loop moves them to the call stack only when the stack is empty."*

---

### 113. Call Stack, Web APIs and Task Queues

**Simple Definition:**
Four parts working together:
1. **Call Stack** – where code runs, one thing at a time.
2. **Web APIs** – browser helpers that handle timers, fetch, DOM events in the background.
3. **Task Queues** – waiting lines for finished callbacks.
4. **Event Loop** – moves tasks from the queue to the stack when it is empty.

**Flow of `setTimeout`:**
`setTimeout` goes on the stack → handed to Web API (timer runs) → timer ends → callback goes to the queue → event loop pushes it to the stack when free → it runs.

**Code Example:**
```js
console.log("A");
setTimeout(() => console.log("B"), 1000);
console.log("C");
// A, C, B
```

**Interview Angle:** 🔥 Very High
- Be ready to draw/explain this flow in an interview.

---

### 114. Microtasks vs Macrotasks

**Simple Definition:**
Two waiting lines with different importance.
- **Microtask queue (VIP line):** Promise `.then/.catch`, `await`, `queueMicrotask`.
- **Macrotask queue (normal line):** `setTimeout`, `setInterval`, DOM events.

**Microtasks always run first**, before the next macrotask.

**Code Example:**
```js
setTimeout(() => console.log("timeout"), 0);   // macrotask
Promise.resolve().then(() => console.log("promise")); // microtask
console.log("sync");
// sync, promise, timeout
```

**Interview Angle:** 🔥 Very High
- Rule: **Sync code → all microtasks → one macrotask → all microtasks → ...**

---

### 115. Execution Order of Promises and Timers

**Simple Definition:**
Combine everything you learnt: normal code first, then promises (microtasks), then timers (macrotasks).

**Code Example:**
```js
console.log("1");

setTimeout(() => console.log("2"), 0);

Promise.resolve().then(() => console.log("3"));

(async () => {
  console.log("4");
  await null;
  console.log("5");
})();

console.log("6");

// Output: 1, 4, 6, 3, 5, 2
```
**Why?**
- Sync: `1`, `4`, `6` (code before `await` runs synchronously)
- Microtasks: `3`, `5`
- Macrotask: `2`

**Interview Angle:** 🔥 Very High
- Very common "predict the output" question.

---

### 116. Fetch API

**Simple Definition:**
`fetch()` is the built-in way to **request data from a server** (get data, send data). It returns a promise.

**Code Example:**
```js
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then(res => res.json())
  .then(data => console.log(data.title));

// POST request
fetch("https://jsonplaceholder.typicode.com/posts", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ title: "Hello" })
});
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** `res.json()` is also a promise, so you need another `.then` or `await`.

---

### 117. HTTP Request and Response Basics

**Simple Definition:**
- **Request:** the browser **asks** the server for something.
- **Response:** the server **answers**.

Common request types (methods): `GET` (read), `POST` (create), `PUT/PATCH` (update), `DELETE` (remove).
A request has: URL, method, headers, and sometimes a body. A response has: status code, headers, and body.

**Code Example:**
```js
const res = await fetch("https://api.example.com/users");
console.log(res.status);   // 200
console.log(res.ok);       // true
```

**Interview Angle:** ⭐ High
- Know the four methods and what they do.

---

### 118. Handling API Responses and JSON

**Simple Definition:**
Data from APIs usually comes as JSON text. You must convert it with `res.json()`, check that it worked, and then use the data.

**Code Example:**
```js
async function getUsers() {
  const res = await fetch("https://jsonplaceholder.typicode.com/users");
  if (!res.ok) throw new Error("Request failed: " + res.status);
  const users = await res.json();
  users.forEach(u => console.log(u.name));
}
```

**Interview Angle:** ⭐ High
- Always check `res.ok` before reading data.

---

### 119. HTTP Status Codes and Network Errors

**Simple Definition:**
Status codes are numbers the server sends to tell what happened.

| Code | Meaning |
|---|---|
| 200 | OK (success) |
| 201 | Created |
| 400 | Bad request (your mistake) |
| 401 | Not logged in |
| 403 | Not allowed |
| 404 | Not found |
| 500 | Server error |

**Network error** = the request couldn't reach the server at all (no internet, wrong domain). Only this kind makes `fetch` throw an error.

**Code Example:**
```js
try {
  const res = await fetch("https://api.example.com/missing");
  if (!res.ok) console.log("HTTP error:", res.status);  // 404 handled here
} catch (e) {
  console.log("Network error:", e.message);
}
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** `fetch` does **not** reject on 404/500.

---

### 120. AbortController and Request Cancellation

**Simple Definition:**
`AbortController` lets you **cancel** a request that is not needed anymore (for example, the user left the page or typed a new search).

**Code Example:**
```js
const controller = new AbortController();

fetch("https://api.example.com/slow", { signal: controller.signal })
  .then(res => res.json())
  .catch(err => {
    if (err.name === "AbortError") console.log("Request cancelled");
  });

controller.abort();  // cancels the request
```

**Interview Angle:** 🙂 Medium
- Common in React cleanup and search-as-you-type features.

---

### 121. Race Conditions in Asynchronous Code

**Simple Definition:**
A race condition happens when **two async tasks finish in an unexpected order**, so an old result overwrites a newer one.

Example: you type "ab" then "abc". The request for "abc" may finish first and the slow request for "ab" shows up last, showing wrong results.

**Code Example:**
```js
let latest = 0;

async function search(text) {
  const id = ++latest;                 // number each request
  const res = await fetch(`/api?q=${text}`);
  const data = await res.json();
  if (id !== latest) return;           // ignore old responses
  console.log("Show:", data);
}
```

**Interview Angle:** ⭐ High
- Fixes: ignore old responses (as above), use `AbortController`, or use debounce.

---

# Level 6: Modern JavaScript (ES6+)

### 122. ES6 Features Overview

**Simple Definition:**
ES6 (also called ES2015) is a big update to JavaScript that made it easier and cleaner to write. Since then, a new update comes every year (ES7, ES8... "ES6+").

**Main ES6 features:**
- `let` and `const`
- Arrow functions
- Template literals
- Destructuring
- Spread and rest
- Default parameters
- Classes
- Promises
- Modules (`import` / `export`)
- `Set`, `Map`, `Symbol`
- `for...of` loop

**Code Example:**
```js
const name = "Asha";
const greet = (n = "Guest") => `Hello, ${n}`;
const [a, b] = [1, 2];
const { x, y } = { x: 10, y: 20 };
console.log(greet(name), a, b, x, y);
```

**Interview Angle:** ⭐ High
- Common question: *"What are the new features in ES6?"* Name at least 5–6 from the list above.

---

### 123. Enhanced Object Literals

**Simple Definition:**
ES6 gave shorter ways to write objects: shorthand properties, shorthand methods, and computed keys.

**Code Example:**
```js
const name = "Sam";
const key = "age";

const user = {
  name,                    // shorthand property
  [key]: 22,               // computed key
  greet() {                // shorthand method
    return "Hi " + this.name;
  }
};
console.log(user);         // { name: "Sam", age: 22, greet: f }
```

**Interview Angle:** 🙂 Medium
- Usually asked as part of the "ES6 features" question.

---

### 124. Enhanced Destructuring Patterns

**Simple Definition:**
Destructuring has extra powers: **default values, renaming, nested objects, rest, and use in function parameters**.

**Code Example:**
```js
const user = {
  id: 1,
  profile: { city: "Pune", age: 22 },
  tags: ["a", "b", "c"]
};

// nested
const { profile: { city } } = user;

// rename + default
const { id: userId, role = "student" } = user;

// rest: collect remaining
const { id, ...others } = user;

// arrays with rest
const [first, ...remaining] = user.tags;

console.log(city, userId, role, first, remaining);
// Pune 1 student a ["b","c"]
```

**Interview Angle:** ⭐ High
- **Common confusion:** In nested destructuring `{ profile: { city } }`, only `city` is created as a variable, not `profile`.

---

### 125. Set

**Simple Definition:**
A `Set` is a collection of **unique values**. It does not allow duplicates.

**Code Example:**
```js
const set = new Set([1, 2, 2, 3, 3]);
console.log(set);          // Set {1, 2, 3}
set.add(4);
set.delete(1);
console.log(set.has(2));   // true
console.log(set.size);     // 3

// Remove duplicates from an array
const unique = [...new Set([1, 1, 2, 3, 3])];
console.log(unique);       // [1, 2, 3]
```

**Interview Angle:** 🔥 Very High
- Most famous use: **remove duplicates** from an array.
- **Common confusion:** `Set` uses `.size`, arrays use `.length`.

---

### 126. Map

**Simple Definition:**
A `Map` stores **key–value pairs**, like an object, but the **key can be anything** (object, number, function), and it remembers insertion order.

**Code Example:**
```js
const map = new Map();
map.set("name", "Asha");
map.set(1, "one");
map.set({ id: 1 }, "object key");

console.log(map.get("name"));  // "Asha"
console.log(map.has(1));       // true
console.log(map.size);         // 3
map.delete(1);

for (const [key, value] of map) {
  console.log(key, value);
}
```

**Interview Angle:** ⭐ High
- **Map vs Object:** Map keys can be any type; Map has `.size`; Map is better for frequent adding/removing; Object keys are only strings/symbols.

---

### 127. WeakSet and WeakMap — Use Cases

**Simple Definition:**
Like `Set` and `Map`, but:
- They can store **only objects** as keys/values.
- They hold items **weakly**: if nothing else uses the object, JavaScript **cleans it up automatically**.
- You can't loop over them and they have no `.size`.

**Code Example:**
```js
const cache = new WeakMap();

let user = { name: "Sam" };
cache.set(user, "some extra data");
console.log(cache.get(user));   // "some extra data"

user = null;  // the object can now be cleaned up, and the cache entry disappears too
```

**Use cases:** storing private data about an object, caching, tracking objects without causing memory leaks.

**Interview Angle:** 🙂 Medium
- **Common confusion:** You can't use strings or numbers as keys in a `WeakMap`.

---

### 128. Symbol — Basics

**Simple Definition:**
A `Symbol` is a **unique value**. Even two symbols with the same description are different. Often used as hidden or special property keys.

**Code Example:**
```js
const id1 = Symbol("id");
const id2 = Symbol("id");
console.log(id1 === id2);    // false (always unique)

const user = { name: "Sam", [id1]: 123 };
console.log(user[id1]);      // 123
console.log(Object.keys(user)); // ["name"]  (symbol is hidden)
```

**Interview Angle:** 💤 Low
- Know it as: "a unique, hidden key that never clashes with others".

---

### 129. Iterables and Iterators

**Simple Definition:**
- **Iterable:** something you can loop over with `for...of` (arrays, strings, Sets, Maps).
- **Iterator:** the "pointer" that gives items **one by one** using a `next()` method.

**Code Example:**
```js
const arr = ["a", "b"];
const iterator = arr[Symbol.iterator]();

console.log(iterator.next()); // { value: "a", done: false }
console.log(iterator.next()); // { value: "b", done: false }
console.log(iterator.next()); // { value: undefined, done: true }

for (const ch of "Hi") console.log(ch); // H, i
```

**Interview Angle:** 🙂 Medium
- **Common confusion:** A normal object `{}` is **not** iterable, so `for...of` does not work on it.

---

### 130. Generators — Basics

**Simple Definition:**
A generator is a special function that can **pause and continue later**. It is written with `function*` and gives values one at a time using `yield`.

**Code Example:**
```js
function* numbers() {
  yield 1;
  yield 2;
  yield 3;
}

const gen = numbers();
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
console.log(gen.next().value); // 3
console.log(gen.next().done);  // true

for (const n of numbers()) console.log(n);
```

**Interview Angle:** 🙂 Medium
- Know: `yield` = pause and give a value; `next()` = continue.

---

### 131. for...in vs for...of

**Simple Definition:**
- `for...in` loops over the **keys** (property names).
- `for...of` loops over the **values** of iterable things (arrays, strings, Sets, Maps).

**Code Example:**
```js
const arr = ["a", "b", "c"];

for (const i in arr) console.log(i);   // "0", "1", "2"  (keys, as strings)
for (const v of arr) console.log(v);   // "a", "b", "c"

const obj = { x: 1, y: 2 };
for (const k in obj) console.log(k, obj[k]);  // works on objects
// for (const v of obj) {}                    // ERROR: not iterable
```

**Interview Angle:** 🔥 Very High
- Memory trick: **in** = **in**dex/keys. **of** = values.
- **Common confusion:** Using `for...in` on arrays (not recommended, indexes come as strings).

---

### 132. Classes and Constructors

**Simple Definition:**
A class is a **blueprint** for creating objects of the same kind. The `constructor` is a special method that runs automatically when you create a new object with `new`.

**Code Example:**
```js
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  greet() {
    return `Hi, I am ${this.name}`;
  }
}

const p1 = new Person("Asha", 22);
console.log(p1.greet());  // Hi, I am Asha
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** Classes in JavaScript are mostly a cleaner way to write the older prototype system. Behind the scenes it's still prototypes.
- Forgetting `new` throws an error.

---

### 133. Instance vs Static Methods

**Simple Definition:**
- **Instance method:** belongs to each **object** you create. Called on the object.
- **Static method:** belongs to the **class itself**. Called on the class name.

**Code Example:**
```js
class MathHelper {
  static add(a, b) {        // static
    return a + b;
  }
  double(x) {               // instance
    return x * 2;
  }
}

console.log(MathHelper.add(2, 3));      // 5
const m = new MathHelper();
console.log(m.double(4));               // 8
// m.add(2, 3);   // ERROR: static not available on objects
```

**Interview Angle:** ⭐ High
- Example of static in JS itself: `Array.isArray()`, `Object.keys()`, `Math.max()`.

---

### 134. Inheritance with extends and super

**Simple Definition:**
Inheritance means **one class can reuse and extend another class**.
- `extends` – makes a child class from a parent class.
- `super()` – calls the parent's constructor. Must be called **before** using `this` in the child.

**Code Example:**
```js
class Animal {
  constructor(name) { this.name = name; }
  speak() { return `${this.name} makes a sound`; }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name);            // call parent constructor
    this.breed = breed;
  }
  speak() {                 // override parent method
    return `${this.name} barks`;
  }
}

const d = new Dog("Tommy", "Labrador");
console.log(d.speak());     // Tommy barks
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** Using `this` before `super()` gives an error.

---

### 135. Encapsulation and Getters/Setters

**Simple Definition:**
- **Encapsulation:** keeping data **safe inside** the class so outside code cannot change it freely. Private fields start with `#`.
- **Getter/Setter:** special methods that look like properties, used to read/change data **with rules**.

**Code Example:**
```js
class BankAccount {
  #balance = 0;                  // private

  get balance() {                // getter
    return this.#balance;
  }
  set balance(amount) {          // setter with a rule
    if (amount < 0) {
      console.log("Cannot be negative");
      return;
    }
    this.#balance = amount;
  }
}

const acc = new BankAccount();
acc.balance = 500;
console.log(acc.balance);   // 500
// console.log(acc.#balance); // ERROR: private
```

**Interview Angle:** ⭐ High
- Before `#`, developers used closures or `_name` (just a naming habit, not real privacy).

---

### 136. Prototypes

**Simple Definition:**
Every JavaScript object has a hidden link to another object called its **prototype**. If a property is missing on the object, JavaScript looks for it in the prototype. This is how objects **share methods** without copying them.

**Code Example:**
```js
function Person(name) {
  this.name = name;
}
Person.prototype.greet = function () {
  return "Hi, " + this.name;
};

const p1 = new Person("Asha");
const p2 = new Person("Ravi");
console.log(p1.greet());                       // shared method
console.log(p1.greet === p2.greet);            // true (same function)
console.log(Object.getPrototypeOf(p1) === Person.prototype); // true
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** `prototype` (a property on functions/classes) vs `__proto__` (the hidden link on objects). `p1.__proto__ === Person.prototype`.

---

### 137. Prototype Chain

**Simple Definition:**
If a property is not found on the object, JavaScript checks its prototype, then the prototype's prototype, and so on, until it reaches `null`. This path is the **prototype chain**.

**Code Example:**
```js
const arr = [1, 2];
// arr -> Array.prototype -> Object.prototype -> null

console.log(arr.hasOwnProperty("length"));          // true
console.log(arr.toString === Array.prototype.toString);// true
console.log(Object.getPrototypeOf(Object.prototype));  // null
```

**Interview Angle:** 🔥 Very High
- Explain it with the example of `arr.map()`: `map` isn't on the array itself; it's found in `Array.prototype`.

---

### 138. Prototypal Inheritance

**Simple Definition:**
One object can **inherit** from another object through the prototype chain, using the parent's methods and properties without copying them.

**Code Example:**
```js
const animal = {
  eat() { return "eating"; }
};

const dog = Object.create(animal);  // dog's prototype is animal
dog.bark = () => "woof";

console.log(dog.bark());  // "woof"   (own)
console.log(dog.eat());   // "eating" (inherited)
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** Classes (`extends`) are just a friendly way to write the same prototype-based inheritance.

---

### 139. instanceof

**Simple Definition:**
`instanceof` checks whether an object was **made from a certain class/constructor** (or its parents).

**Code Example:**
```js
class Animal {}
class Dog extends Animal {}

const d = new Dog();
console.log(d instanceof Dog);     // true
console.log(d instanceof Animal);  // true (parent)
console.log(d instanceof Array);   // false
console.log([] instanceof Array);  // true
console.log([] instanceof Object); // true
```

**Interview Angle:** 🙂 Medium
- **Common confusion:** `instanceof` does not work on primitives (`"hi" instanceof String` is `false`).

---

### 140. Built-in Object and Array Methods

**Simple Definition:**
A quick list of useful helpers JavaScript already gives you.

**Object helpers:**
```js
Object.keys(obj);        Object.values(obj);       Object.entries(obj);
Object.assign({}, obj);  Object.freeze(obj);       Object.fromEntries(pairs);
Object.hasOwn(obj, "x"); // modern way to check own property
```

**Array helpers:**
```js
arr.flat();              // flatten one level
arr.flatMap(fn);         // map + flat
arr.at(-1);              // last item
Array.from("abc");       // ["a","b","c"]
Array.of(1, 2);          // [1, 2]
arr.fill(0);             // fill with 0
arr.concat(other);       // join arrays
```

**Code Example:**
```js
const entries = [["a", 1], ["b", 2]];
console.log(Object.fromEntries(entries));  // { a: 1, b: 2 }
console.log([1, [2, [3]]].flat(Infinity)); // [1, 2, 3]
```

**Interview Angle:** ⭐ High
- Great for coding rounds: knowing `flat`, `fromEntries`, `Array.from` saves time.

---

# Level 7: Advanced JavaScript Interview Concepts

### 141. Function Execution and Scope Deep Dive

**Simple Definition:**
Every time a function is called, JavaScript makes a **fresh workspace** for it. It first sets up the variables (hoisting), then runs the lines. It looks for variables in its own workspace first, then outward (scope chain). Each call gets its **own separate** variables.

**Code Example:**
```js
var x = "global";

function outer() {
  var x = "outer";
  function inner() {
    console.log(x);   // "outer" (nearest one wins)
  }
  inner();
}
outer();

function test() {
  console.log(a);     // undefined (hoisted)
  var a = 5;
  console.log(a);     // 5
}
test();
```

**Interview Angle:** 🔥 Very High
- Output questions mixing hoisting, scope and closures are very popular.
- **Common confusion:** A local variable with the same name **hides** the outer one (shadowing).

---

### 142. Closures and Memory Management

**Simple Definition:**
A closure keeps its outer variables **alive in memory** as long as the inner function exists. This is useful, but if you keep big data in a closure and never release it, memory is wasted.

**Code Example:**
```js
function createHeavy() {
  const bigData = new Array(1000000).fill("data");
  return function () {
    return bigData.length;   // keeps bigData in memory
  };
}

let fn = createHeavy();
console.log(fn());   // 1000000
fn = null;           // now bigData can be cleaned up
```

**Interview Angle:** ⭐ High
- Say: *"Closures are not bad, but be careful to release them (set to `null`, remove event listeners) when no longer needed."*

---

### 143. Lexical this vs Dynamic this

**Simple Definition:**
- **Dynamic `this` (normal functions):** decided **when the function is called**.
- **Lexical `this` (arrow functions):** decided by **where the arrow function is written**. It never changes.

**Code Example:**
```js
const obj = {
  name: "Asha",
  normal() { return this.name; },          // dynamic this
  later() {
    return [1].map(() => this.name);       // arrow borrows this from later()
  }
};

console.log(obj.normal());   // "Asha"
console.log(obj.later());    // ["Asha"]  (arrow keeps lexical this)

const fn = obj.normal;
console.log(fn());           // undefined (dynamic: this changed)
```

**Interview Angle:** 🔥 Very High
- Quick summary: normal functions = "who calls me"; arrow functions = "who surrounds me".

---

### 144. new Keyword and Constructor Functions

**Simple Definition:**
A constructor function is a normal function used to **build objects**. When you call it with `new`, JavaScript does 4 steps:
1. Creates an empty object.
2. Links it to the function's prototype.
3. Runs the function with `this` as the new object.
4. Returns that object.

**Code Example:**
```js
function Car(brand) {
  this.brand = brand;
}
const c = new Car("Tata");
console.log(c.brand);          // "Tata"
console.log(c instanceof Car); // true

// Without new, this is wrong:
// const bad = Car("Tata");    // this is window / undefined -> bug
```

**Interview Angle:** 🔥 Very High
- Convention: constructor names start with a **capital letter**.
- Interviewers may ask you to explain the 4 steps.

---

### 145. Property Descriptors

**Simple Definition:**
Each property has hidden settings that control how it behaves:
- `value` – the data
- `writable` – can the value be changed?
- `enumerable` – does it appear in loops/`Object.keys`?
- `configurable` – can it be deleted or its settings changed?

**Code Example:**
```js
const user = { name: "Sam" };

console.log(Object.getOwnPropertyDescriptor(user, "name"));
// { value: "Sam", writable: true, enumerable: true, configurable: true }

Object.defineProperty(user, "id", {
  value: 101,
  writable: false,      // read-only
  enumerable: false     // hidden from loops
});

user.id = 5;            // silently ignored (error in strict mode)
console.log(user.id);   // 101
console.log(Object.keys(user)); // ["name"]
```

**Interview Angle:** 🙂 Medium
- Properties made with `defineProperty` default to `false` for all three settings.

---

### 146. Object Immutability: Object.freeze() and Object.seal()

**Simple Definition:**
Immutable means "cannot change".
- `Object.freeze(obj)` – cannot add, remove or change properties. Fully locked.
- `Object.seal(obj)` – cannot add or remove properties, but **can change** existing values.
- Both are **shallow**: inner objects are still changeable.

**Code Example:**
```js
const frozen = Object.freeze({ a: 1, inner: { b: 2 } });
frozen.a = 99;          // ignored
frozen.c = 3;           // ignored
frozen.inner.b = 50;    // works! (shallow)
console.log(frozen);    // { a: 1, inner: { b: 50 } }

const sealed = Object.seal({ x: 1 });
sealed.x = 2;           // allowed
sealed.y = 3;           // ignored
delete sealed.x;        // ignored
```

**Interview Angle:** ⭐ High
- **Common confusion:** `const` vs `freeze`: `const` stops re-assigning the variable; `freeze` stops changing the object.

---

### 147. Equality: Value vs Reference Comparison

**Simple Definition:**
- **Primitives** are compared by **value**: `5 === 5` is `true`.
- **Objects/arrays** are compared by **reference (address)**: two separate objects with the same content are **not equal**.

**Code Example:**
```js
console.log("a" === "a");        // true
console.log({} === {});          // false
console.log([1] === [1]);        // false

const a = { x: 1 };
const b = a;
console.log(a === b);            // true (same reference)

// Comparing content: simple trick
console.log(JSON.stringify({ x: 1 }) === JSON.stringify({ x: 1 })); // true
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** `[] == []` and `{} == {}` are both `false`.
- Also: `Object.is(NaN, NaN)` is `true`, while `NaN === NaN` is `false`.

---

### 148. Automatic Semicolon Insertion (ASI)

**Simple Definition:**
JavaScript sometimes **adds missing semicolons for you**. This usually works, but in some cases it adds them in the **wrong place** and breaks your code.

**Code Example:**
```js
function getValue() {
  return
  {
    name: "Sam"
  };
}
console.log(getValue());   // undefined! (semicolon added after 'return')

// Fixed:
function getValue2() {
  return {
    name: "Sam"
  };
}
```

**Interview Angle:** 🙂 Medium
- Rule: Always start the value on the **same line** as `return`. Using semicolons yourself avoids surprises.

---

### 149. Strict Mode

**Simple Definition:**
Strict mode is a **safer way of running JavaScript**. It turns silent mistakes into real errors. Turn it on by writing `"use strict";` at the top. (Modules and classes use it automatically.)

**Code Example:**
```js
"use strict";

// x = 10;                 // ERROR: x is not declared (normally creates a global)
// delete Object.prototype;// ERROR
function show() {
  console.log(this);       // undefined (instead of window)
}
show();
```

**Interview Angle:** ⭐ High
- Things strict mode does: no accidental globals, `this` is `undefined` in plain functions, no duplicate parameter names.

---

### 150. Error Types and Custom Errors

**Simple Definition:**
JavaScript has built-in error types:
- `SyntaxError` – code is written wrongly.
- `ReferenceError` – variable doesn't exist.
- `TypeError` – wrong type used (e.g., calling a non-function).
- `RangeError` – number out of allowed range.

You can also make **your own error** by extending `Error`.

**Code Example:**
```js
// ReferenceError
// console.log(notDefined);

// TypeError
// const n = 5; n();

class ValidationError extends Error {
  constructor(message) {
    super(message);
    this.name = "ValidationError";
  }
}

try {
  throw new ValidationError("Age must be positive");
} catch (e) {
  console.log(e.name);      // ValidationError
  console.log(e.message);   // Age must be positive
  console.log(e instanceof ValidationError); // true
}
```

**Interview Angle:** ⭐ High
- **Common confusion:** `throw` can throw anything, but always throw an `Error` object so you get a helpful message and stack.

---

### 151. Garbage Collection — Basics

**Simple Definition:**
JavaScript automatically **frees memory** of things you no longer use. The main idea: if nothing can reach an object anymore (no variable points to it), it is garbage and gets removed. This method is called **mark-and-sweep**.

**Code Example:**
```js
let user = { name: "Sam" };  // object in memory
user = null;                 // nobody points to it, so it will be cleaned up
```

**Interview Angle:** ⭐ High
- **Common confusion:** You cannot force garbage collection. You can only make sure that nothing is still pointing to the data.

---

### 152. Memory Leaks in Browser Applications

**Simple Definition:**
A memory leak is when your app **keeps memory it no longer needs**, so the page becomes slower over time.

**Common causes:**
1. Accidental global variables
2. Timers never stopped (`setInterval`)
3. Event listeners never removed
4. Closures holding big data
5. Removed DOM elements still referenced in variables

**Code Example:**
```js
// Leak: interval never cleared
const id = setInterval(() => console.log("running"), 1000);
// Fix:
clearInterval(id);

// Leak: listener never removed
function onResize() {}
window.addEventListener("resize", onResize);
// Fix:
window.removeEventListener("resize", onResize);
```

**Interview Angle:** ⭐ High
- Tool to find leaks: Chrome DevTools → Memory tab.

---

### 153. Functional Programming Concepts

**Simple Definition:**
A style of coding based on **small, simple functions** with these ideas:
- **Pure functions** (no side effects)
- **Immutability** (don't change data, make new copies)
- **First-class / higher-order functions**
- **Function composition** (join small functions)
- Avoid shared state

**Code Example:**
```js
const numbers = [1, 2, 3, 4];

// Not changing the original, making new data
const result = numbers
  .filter(n => n % 2 === 0)
  .map(n => n * 10);

console.log(result);   // [20, 40]
console.log(numbers);  // [1, 2, 3, 4] (unchanged)
```

**Interview Angle:** ⭐ High
- Easy summary: *"Write small pure functions, don't change data, and combine functions together."*

---

### 154. Currying

**Simple Definition:**
Currying turns a function that takes **many arguments at once** into a chain of functions that take **one argument at a time**.
`add(1, 2, 3)` becomes `add(1)(2)(3)`.

**Code Example:**
```js
function add(a) {
  return function (b) {
    return function (c) {
      return a + b + c;
    };
  };
}
console.log(add(1)(2)(3));   // 6

const add5 = add(5);         // reuse
console.log(add5(1)(1));     // 7

// Arrow style
const mul = a => b => a * b;
console.log(mul(3)(4));      // 12
```

**Interview Angle:** 🔥 Very High
- Uses closures. A common coding question is to write a generic `curry(fn)` function.

---

### 155. Partial Application

**Simple Definition:**
Partial application means **fixing some arguments in advance**, and getting a new function that waits for the remaining ones.

**Code Example:**
```js
function multiply(a, b) { return a * b; }

const double = multiply.bind(null, 2);   // fix a = 2
console.log(double(5));                  // 10

// Using closure
const partial = (fn, ...fixed) => (...rest) => fn(...fixed, ...rest);
const triple = partial(multiply, 3);
console.log(triple(4));                  // 12
```

**Interview Angle:** 🙂 Medium
- **Currying vs Partial:** Currying always makes one-argument-at-a-time functions. Partial application fixes *any number* of arguments at once.

---

### 156. Memoization

**Simple Definition:**
Memoization means **remembering the result** of a function for given inputs, so if called again with the same input, it gives the saved answer instead of calculating again. It saves time.

**Code Example:**
```js
function memoize(fn) {
  const cache = {};
  return function (n) {
    if (n in cache) {
      console.log("From cache");
      return cache[n];
    }
    const result = fn(n);
    cache[n] = result;
    return result;
  };
}

const square = memoize(n => n * n);
console.log(square(5));   // 25 (calculated)
console.log(square(5));   // "From cache" 25
```

**Interview Angle:** 🔥 Very High
- Uses closures + objects/Map. Works only for **pure functions**.
- Popular with Fibonacci.

---

### 157. Composition and Function Pipelining

**Simple Definition:**
Joining small functions so the **output of one becomes the input of the next**.
- **compose:** runs right to left.
- **pipe:** runs left to right.

**Code Example:**
```js
const add2 = x => x + 2;
const double = x => x * 2;

const pipe = (...fns) => x => fns.reduce((v, fn) => fn(v), x);
const compose = (...fns) => x => fns.reduceRight((v, fn) => fn(v), x);

console.log(pipe(add2, double)(5));     // (5+2)*2 = 14
console.log(compose(add2, double)(5));  // (5*2)+2 = 12
```

**Interview Angle:** ⭐ High
- **Common confusion:** The order of `pipe` vs `compose`.

---

### 158. Polyfills and How They Work

**Simple Definition:**
A polyfill is **your own code that adds a modern feature** to old browsers that don't have it. It first checks if the feature exists. If not, it adds it.

**Code Example:**
```js
// Polyfill for Array.prototype.map
if (!Array.prototype.myMap) {
  Array.prototype.myMap = function (callback) {
    const result = [];
    for (let i = 0; i < this.length; i++) {
      result.push(callback(this[i], i, this));
    }
    return result;
  };
}

console.log([1, 2, 3].myMap(n => n * 2));  // [2, 4, 6]
```

**Interview Angle:** 🔥 Very High
- Common to be asked to write polyfills for `map`, `filter`, `reduce`, `bind`, `Promise.all`.

---

### 159. CommonJS vs ES Modules

**Simple Definition:**
Two systems for sharing code between files.

| | CommonJS | ES Modules |
|---|---|---|
| Syntax | `require()` / `module.exports` | `import` / `export` |
| Used in | Node.js (older) | Browsers + modern Node.js |
| Loading | Synchronous (runs when reached) | Static (analysed before running) |

**Code Example:**
```js
// CommonJS
const fs = require("fs");
module.exports = { add };

// ES Module
import fs from "fs";
export { add };
```

**Interview Angle:** ⭐ High
- **Common confusion:** You can't mix `require` and `import` casually in the same file.

---

### 160. Dynamic import()

**Simple Definition:**
Normal `import` loads at the start. **Dynamic `import()` loads a file only when you need it**, and returns a promise. It makes pages load faster (lazy loading).

**Code Example:**
```js
button.addEventListener("click", async () => {
  const module = await import("./heavy.js");
  module.doWork();
});

// or
import("./math.js").then(m => console.log(m.add(2, 3)));
```

**Interview Angle:** 🙂 Medium
- Remember: **returns a Promise**; used for lazy loading and code splitting.

---

# Level 8: JavaScript Coding and Interview Practice

> For this level, each topic explains **what the problem type is**, the **easy way to think**, and **solved examples**. Try to solve it yourself first, then read the answer.

### 161. String Manipulation Problems

**Simple Definition:**
Problems where you **change or check text**. Remember: strings **cannot be changed in place**; every method gives a new string.

**Common methods:** `split`, `join`, `slice`, `toUpperCase`, `trim`, `replace`, `includes`, `charAt`.

**Code Example:**
```js
// 1. Reverse a string
const reverse = s => s.split("").reverse().join("");
console.log(reverse("hello"));  // "olleh"

// 2. Check palindrome
const isPalindrome = s => s === reverse(s);
console.log(isPalindrome("madam")); // true

// 3. Count vowels
const countVowels = s => (s.match(/[aeiou]/gi) || []).length;
console.log(countVowels("Education")); // 5

// 4. Capitalize each word
const capitalize = s => s.split(" ").map(w => w[0].toUpperCase() + w.slice(1)).join(" ");
console.log(capitalize("hello big world")); // "Hello Big World"
```

**Interview Angle:** 🔥 Very High
- Classic: reverse, palindrome, anagram, vowel count, first non-repeating character.

---

### 162. Array Coding Problems

**Simple Definition:**
Problems where you find, change or rearrange items in arrays. Think: *"Can `map`, `filter`, `reduce` or a simple loop solve this?"*

**Code Example:**
```js
// 1. Largest number
const max = arr => Math.max(...arr);
console.log(max([3, 9, 2])); // 9

// 2. Second largest
function secondLargest(arr) {
  const unique = [...new Set(arr)].sort((a, b) => b - a);
  return unique[1];
}
console.log(secondLargest([5, 1, 9, 9, 3])); // 5

// 3. Sum of array
console.log([1, 2, 3].reduce((s, n) => s + n, 0)); // 6

// 4. Rotate array by k
function rotate(arr, k) {
  k = k % arr.length;
  return [...arr.slice(-k), ...arr.slice(0, -k)];
}
console.log(rotate([1, 2, 3, 4, 5], 2)); // [4, 5, 1, 2, 3]
```

**Interview Angle:** 🔥 Very High
- Always think about **empty arrays** and **duplicates** (edge cases).

---

### 163. Object Manipulation Problems

**Simple Definition:**
Problems where you read, change, group, or count data in objects. Useful tools: `Object.keys/values/entries`, `reduce`, destructuring.

**Code Example:**
```js
// 1. Group people by city
const people = [
  { name: "A", city: "Pune" },
  { name: "B", city: "Delhi" },
  { name: "C", city: "Pune" }
];
const grouped = people.reduce((acc, p) => {
  (acc[p.city] ||= []).push(p.name);
  return acc;
}, {});
console.log(grouped); // { Pune: ["A","C"], Delhi: ["B"] }

// 2. Swap keys and values
const swap = obj => Object.fromEntries(Object.entries(obj).map(([k, v]) => [v, k]));
console.log(swap({ a: 1, b: 2 })); // { "1": "a", "2": "b" }

// 3. Count properties
console.log(Object.keys({ x: 1, y: 2 }).length); // 2
```

**Interview Angle:** ⭐ High
- "Group by" and "count by" with `reduce` are very common.

---

### 164. Frequency Counter Problems

**Simple Definition:**
Count **how many times** each item appears, using an object or Map. This one trick solves many problems (anagrams, duplicates, most common item).

**Code Example:**
```js
function frequency(arr) {
  const count = {};
  for (const item of arr) {
    count[item] = (count[item] || 0) + 1;
  }
  return count;
}
console.log(frequency(["a", "b", "a", "c", "a"])); // { a: 3, b: 1, c: 1 }

// Anagram check
function isAnagram(a, b) {
  if (a.length !== b.length) return false;
  const count = {};
  for (const ch of a) count[ch] = (count[ch] || 0) + 1;
  for (const ch of b) {
    if (!count[ch]) return false;
    count[ch]--;
  }
  return true;
}
console.log(isAnagram("listen", "silent")); // true

// First non-repeating character
function firstUnique(s) {
  const c = frequency(s.split(""));
  return s.split("").find(ch => c[ch] === 1);
}
console.log(firstUnique("aabbcd")); // "c"
```

**Interview Angle:** 🔥 Very High
- Pattern to remember: **loop once → count → loop again → decide**.

---

### 165. Remove Duplicates from Arrays

**Simple Definition:**
Keep only the first copy of each item.

**Code Example:**
```js
const arr = [1, 2, 2, 3, 3, 3];

// 1. Using Set (best, shortest)
console.log([...new Set(arr)]);                         // [1, 2, 3]

// 2. Using filter
console.log(arr.filter((v, i) => arr.indexOf(v) === i)); // [1, 2, 3]

// 3. Using reduce
console.log(arr.reduce((acc, v) => acc.includes(v) ? acc : [...acc, v], []));

// Duplicate objects by id
const users = [{ id: 1 }, { id: 2 }, { id: 1 }];
const uniqueUsers = [...new Map(users.map(u => [u.id, u])).values()];
console.log(uniqueUsers); // [{id:1},{id:2}]
```

**Interview Angle:** 🔥 Very High
- Interviewers often ask for **at least 2–3 ways**.

---

### 166. Flatten an Array

**Simple Definition:**
Turn a **nested array** (arrays inside arrays) into a **single flat array**.

**Code Example:**
```js
const nested = [1, [2, [3, [4]]]];

// 1. Built-in
console.log(nested.flat(Infinity));   // [1, 2, 3, 4]

// 2. Recursion
function flatten(arr) {
  let result = [];
  for (const item of arr) {
    if (Array.isArray(item)) {
      result = result.concat(flatten(item));
    } else {
      result.push(item);
    }
  }
  return result;
}
console.log(flatten(nested));         // [1, 2, 3, 4]

// 3. Using reduce
const flat2 = arr => arr.reduce(
  (acc, v) => acc.concat(Array.isArray(v) ? flat2(v) : v), []
);
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** `flat()` goes only **one level** by default. Use `Infinity` for all levels.

---

### 167. Find Missing and Duplicate Numbers

**Simple Definition:**
Given numbers from 1 to n with one missing or repeated, find it.

**Code Example:**
```js
// Missing number (numbers 1..n, one missing)
function findMissing(arr) {
  const n = arr.length + 1;
  const expected = (n * (n + 1)) / 2;        // sum of 1..n
  const actual = arr.reduce((s, v) => s + v, 0);
  return expected - actual;
}
console.log(findMissing([1, 2, 4, 5])); // 3

// Find duplicates
function findDuplicates(arr) {
  const seen = new Set(), dups = new Set();
  for (const n of arr) {
    if (seen.has(n)) dups.add(n);
    seen.add(n);
  }
  return [...dups];
}
console.log(findDuplicates([1, 2, 3, 2, 4, 1])); // [2, 1]
```

**Interview Angle:** ⭐ High
- The "sum formula" `n(n+1)/2` is the trick to remember.

---

### 168. Two Sum and Related Problems

**Simple Definition:**
**Two Sum:** Given an array and a target number, find two numbers that add up to the target.

**Easy way to think:** For each number, ask *"Have I already seen the number I need (target − current)?"* Store seen numbers in an object/Map.

**Code Example:**
```js
function twoSum(nums, target) {
  const seen = {};                       // number -> index
  for (let i = 0; i < nums.length; i++) {
    const need = target - nums[i];
    if (need in seen) return [seen[need], i];
    seen[nums[i]] = i;
  }
  return [];
}
console.log(twoSum([2, 7, 11, 15], 9)); // [0, 1]
```

**Related problems:** three sum, pair with given difference, check if two items add up (same idea).

**Interview Angle:** 🔥 Very High (most famous coding question)
- First say the **slow way** (two loops, O(n²)), then show the **fast way** (one loop with Map, O(n)).

---

### 169. Sorting and Searching Basics

**Simple Definition:**
- **Sorting:** arrange items in order.
- **Searching:** find an item.
  - **Linear search:** check one by one.
  - **Binary search:** works only on a **sorted** array; check the middle and throw away half each time. Very fast.

**Code Example:**
```js
// Linear search
const linear = (arr, t) => arr.indexOf(t);

// Binary search
function binarySearch(arr, target) {
  let low = 0, high = arr.length - 1;
  while (low <= high) {
    const mid = Math.floor((low + high) / 2);
    if (arr[mid] === target) return mid;
    if (arr[mid] < target) low = mid + 1;
    else high = mid - 1;
  }
  return -1;
}
console.log(binarySearch([1, 3, 5, 7, 9], 7)); // 3

// Bubble sort (simple)
function bubbleSort(arr) {
  const a = [...arr];
  for (let i = 0; i < a.length; i++) {
    for (let j = 0; j < a.length - i - 1; j++) {
      if (a[j] > a[j + 1]) [a[j], a[j + 1]] = [a[j + 1], a[j]];
    }
  }
  return a;
}
console.log(bubbleSort([5, 2, 8, 1])); // [1, 2, 5, 8]
```

**Interview Angle:** ⭐ High
- Binary search time: O(log n). Bubble sort: O(n²).
- **Common confusion:** Binary search only works if the array is sorted.

---

### 170. map(), filter() and reduce() Coding Challenges

**Simple Definition:**
Practice using the three main array methods to solve small problems.

**Code Example:**
```js
const students = [
  { name: "A", marks: 80 },
  { name: "B", marks: 45 },
  { name: "C", marks: 92 }
];

// map: get only names
console.log(students.map(s => s.name));              // ["A","B","C"]

// filter: students who passed (>= 50)
console.log(students.filter(s => s.marks >= 50));    // A and C

// reduce: total marks
console.log(students.reduce((sum, s) => sum + s.marks, 0)); // 217

// Find the topper using reduce
const topper = students.reduce((best, s) => s.marks > best.marks ? s : best);
console.log(topper.name);   // "C"

// Chain: names of passed students in capital letters
console.log(
  students.filter(s => s.marks >= 50).map(s => s.name.toUpperCase())
); // ["A","C"]
```

**Interview Angle:** 🔥 Very High
- Also be ready to **write your own** `map`, `filter`, `reduce` (polyfills).

---

### 171. Closures-Based Coding Questions

**Simple Definition:**
Questions where a function must **remember something** between calls.

**Code Example:**
```js
// 1. Counter with increment/decrement
function createCounter() {
  let count = 0;
  return {
    inc: () => ++count,
    dec: () => --count,
    get: () => count
  };
}
const c = createCounter();
c.inc(); c.inc(); c.dec();
console.log(c.get()); // 1

// 2. Run a function only once
function once(fn) {
  let done = false, result;
  return function (...args) {
    if (!done) {
      result = fn(...args);
      done = true;
    }
    return result;
  };
}
const init = once(() => console.log("Initialized"));
init(); init();   // prints only once

// 3. Fix the loop problem
for (let i = 1; i <= 3; i++) {
  setTimeout(() => console.log(i), 100);   // 1 2 3
}
```

**Interview Angle:** 🔥 Very High
- Other common ones: `add(1)(2)(3)`, `memoize`, a function that remembers its call count.

---

### 172. Implement Debounce and Throttle

**Simple Definition:**
Write your own versions (revision of topics 90 and 91, with a complete answer).

**Code Example:**
```js
function debounce(fn, delay) {
  let timer;
  return function (...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}

function throttle(fn, limit) {
  let lastCall = 0;
  return function (...args) {
    const now = Date.now();
    if (now - lastCall >= limit) {
      lastCall = now;
      fn.apply(this, args);
    }
  };
}
```

**Interview Angle:** 🔥 Very High
- Tell the interviewer the real examples: debounce for search box, throttle for scroll/resize.
- Mention: both use **closures** to keep `timer` / `lastCall`.

---

### 173. Implement a Simplified Promise.all()

**Simple Definition:**
Write your own version of `Promise.all`. It should return a promise that gives all results in order, or fails as soon as one fails.

**Code Example:**
```js
function myPromiseAll(promises) {
  return new Promise((resolve, reject) => {
    const results = [];
    let completed = 0;

    if (promises.length === 0) return resolve([]);

    promises.forEach((p, index) => {
      Promise.resolve(p)                 // handles normal values too
        .then(value => {
          results[index] = value;        // keep original order
          completed++;
          if (completed === promises.length) resolve(results);
        })
        .catch(reject);                  // fail fast
    });
  });
}

myPromiseAll([Promise.resolve(1), 2, new Promise(r => setTimeout(() => r(3), 500))])
  .then(console.log);   // [1, 2, 3]
```

**Interview Angle:** 🔥 Very High
- Key points to mention: keep results **in order** (use index), count completed ones, **reject immediately** on first error, handle empty array.

---

### 174. Output-Based Questions on Hoisting, Scope and Closures

**Simple Definition:**
Questions that ask *"What will this print?"* Go slowly, step by step.

**Code Example:**
```js
// Q1
console.log(a);
var a = 10;
// Answer: undefined (var is hoisted, value is not)

// Q2
// console.log(b);
let b = 5;
// Answer: ReferenceError (Temporal Dead Zone)

// Q3
var x = 1;
function test() {
  console.log(x);
  var x = 2;
}
test();
// Answer: undefined (local x is hoisted inside the function)

// Q4
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 0);
}
// Answer: 3 3 3

// Q5
for (let j = 0; j < 3; j++) {
  setTimeout(() => console.log(j), 0);
}
// Answer: 0 1 2

// Q6
function outer() {
  let count = 0;
  return () => ++count;
}
const f = outer();
f(); f();
console.log(f());
// Answer: 3
```

**Interview Angle:** 🔥 Very High
- Steps to solve: (1) hoist declarations, (2) check scope, (3) run line by line, (4) remember `var` vs `let` in loops.

---

### 175. Event Loop Output Questions

**Simple Definition:**
Questions with `setTimeout`, promises and normal code mixed. Use the rule: **sync code → microtasks (promises) → macrotasks (timers)**.

**Code Example:**
```js
// Q1
console.log("A");
setTimeout(() => console.log("B"), 0);
Promise.resolve().then(() => console.log("C"));
console.log("D");
// Answer: A, D, C, B

// Q2
setTimeout(() => console.log("1"), 0);
Promise.resolve()
  .then(() => console.log("2"))
  .then(() => console.log("3"));
console.log("4");
// Answer: 4, 2, 3, 1

// Q3
async function run() {
  console.log("x");
  await Promise.resolve();
  console.log("y");
}
run();
console.log("z");
// Answer: x, z, y
```

**Interview Angle:** 🔥 Very High
- **Common confusion:** Code written after `await` goes into the microtask queue, so it runs *after* the remaining normal code.

---

### 176. Predict the Output of this, Promises and Type Coercion

**Simple Definition:**
Mixed practice for the trickiest topics.

**Code Example:**
```js
// this
const obj = {
  name: "Sam",
  regular() { return this.name; }
};
console.log(obj.regular());       // "Sam"
const fn = obj.regular;
// console.log(fn());              // undefined (this is lost)

// Promises
Promise.resolve(1)
  .then(v => v + 1)
  .then(v => { throw new Error("fail"); })
  .catch(() => 10)
  .then(v => console.log(v));      // 10

// Type coercion
console.log(1 + "2");              // "12"
console.log("3" - 1);              // 2
console.log(true + true);          // 2
console.log([] + []);              // "" (empty string)
console.log([] == false);          // true
console.log(null == 0);            // false
console.log(null >= 0);            // true (weird!)
console.log("b" + "a" + +"a" + "a"); // "baNaNa"
console.log(0.1 + 0.2 === 0.3);    // false (decimal precision issue)
console.log(typeof NaN);           // "number"
```

**Interview Angle:** 🔥 Very High
- For `0.1 + 0.2`, the answer is `0.30000000000000004`. To compare, use: `Math.abs(a - b) < Number.EPSILON`.

---

### 177. Time and Space Complexity Basics

**Simple Definition:**
It tells **how your code slows down or uses more memory** when the input gets bigger. It is written using **Big O** notation.
- **Time complexity:** how many steps.
- **Space complexity:** how much extra memory.

| Big O | Name | Example |
|---|---|---|
| O(1) | Constant | Access `arr[0]` |
| O(log n) | Logarithmic | Binary search |
| O(n) | Linear | One loop through array |
| O(n log n) | Linearithmic | Good sorting (`sort()`) |
| O(n²) | Quadratic | Loop inside a loop |

**Code Example:**
```js
// O(1) time
const first = arr => arr[0];

// O(n) time
function sum(arr) {
  let total = 0;
  for (const n of arr) total += n;   // runs n times
  return total;
}

// O(n²) time
function allPairs(arr) {
  for (let i = 0; i < arr.length; i++)
    for (let j = 0; j < arr.length; j++)
      console.log(arr[i], arr[j]);
}

// O(n) space (new array of the same size)
const doubled = arr => arr.map(n => n * 2);
```

**Interview Angle:** ⭐ High
- After solving a problem, interviewers often ask: *"What is the time and space complexity?"*
- Quick rule: one loop → O(n), loop inside loop → O(n²), halving each time → O(log n).

---

### 178. Debugging and Reading Unfamiliar Code

**Simple Definition:**
Debugging means **finding and fixing mistakes**. Reading unfamiliar code means understanding code that you did not write.

**Steps for debugging:**
1. Read the **error message** carefully (it tells the file and line number).
2. Use `console.log()` to see values.
3. Use `debugger;` or DevTools breakpoints to pause and look step by step.
4. Make the problem smaller until you find the exact line.
5. Check common mistakes: typo, `undefined`, wrong type, async timing, `this` problem.

**Steps for reading unfamiliar code:**
1. Find the **starting point** (where code begins).
2. Read the function names and what goes in / comes out.
3. Run it with a small example and print values.
4. Draw a small diagram if needed.

**Code Example:**
```js
function average(numbers) {
  let total = 0;
  for (let i = 0; i <= numbers.length; i++) {   // BUG: should be <
    total += numbers[i];                         // adds undefined at the end
  }
  console.log("total:", total);                  // helps spot NaN
  return total / numbers.length;
}
console.log(average([2, 4, 6]));   // NaN

// Fix: i < numbers.length
// Also try: console.table(data), console.error(), debugger;
```

**Interview Angle:** ⭐ High
- Interviewers want to see your **thinking process**: speak out loud, check edge cases (empty input, `null`, wrong types), and test with small examples.

---

# Quick Revision: Top Topics Asked in Interviews

1. `var` vs `let` vs `const` (4)
2. `==` vs `===` and type coercion (10, 11)
3. Hoisting and Temporal Dead Zone (56, 57)
4. `this` keyword, `call/apply/bind` (61–64)
5. Closures (66)
6. `map`, `filter`, `reduce` (31–33)
7. Shallow vs deep copy (50)
8. Event bubbling, capturing, delegation (83, 84)
9. Debounce vs throttle (90, 91)
10. Promises, `async/await`, `Promise.all` (100–110)
11. Event loop, microtasks vs macrotasks (112–115)
12. Prototype and prototype chain (136, 137)
13. Currying, memoization, polyfills (154, 156, 158)

**Good luck with your preparation!**
