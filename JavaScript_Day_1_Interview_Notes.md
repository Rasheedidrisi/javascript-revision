# JavaScript Day 1 — Interview Notes

> **Goal:** Understand the fundamentals, revise quickly, and explain each concept in simple interview language.

## 1. Variables: `var`, `let`, and `const`

A variable is a named place to keep a value.

```js
let age = 19;
age = 20; // Reassignment: changing the value
```

- **Reassignment:** Giving an existing variable a new value.
- **Redeclaration:** Declaring a variable with the same name again in the same scope.
- `var`: can be reassigned and redeclared in the same scope.
- `let`: can be reassigned, but cannot be redeclared in the same scope.
- `const`: cannot be reassigned or redeclared in the same scope. It must receive a value when declared.

```js
var a = 1;
var a = 2; // Allowed

let b = 1;
b = 2;     // Allowed
// let b = 3; // Error in the same scope

const c = 1;
// c = 2;   // Error
```

### Important: `const` and mutation

`const` stops you from assigning a completely new value to the variable. It does **not** stop you from changing the contents of an object or array.

```js
const user = { name: "Rasheed" };
user.name = "Ali"; // Allowed: changes a property

const numbers = [10, 20];
numbers.push(30);  // Allowed: changes the array

// user = {};      // Error: reassignment
```

## 2. Hoisting

**Interview answer:** “Hoisting is JavaScript’s behaviour of processing declarations before it runs the code. What happens when you access a name early depends on how it was declared.”

```js
console.log(a); // undefined
var a = 10;
```

With `var`, the declaration is set up early, and before the assignment the value is `undefined`.

For `let` and `const`, trying to access the variable before its declaration is initialized causes a `ReferenceError`.

## 3. Declaration vs. initialization

- **Declaration:** Creating a variable name.
- **Initialization:** Giving that variable its first value.
- **Reassignment:** Giving it another value later.

```js
let score;      // Declaration
score = 50;     // Initialization
score = 80;     // Reassignment
```

## 4. TDZ (Temporal Dead Zone)

**Interview answer:** “TDZ is the time after entering a scope but before a `let` or `const` variable has been initialized. Accessing the variable during this time causes a `ReferenceError`.”

```js
// TDZ for age is in effect here
// console.log(age); // ReferenceError
let age = 19;
console.log(age); // 19
```

Easy reminder: with `let` and `const`, do not use the variable before its declaration is reached.

## 5. Loose equality (`==`) vs. strict equality (`===`)

- `==` compares values and may convert types before comparing.
- `===` compares both value and type without converting one type to another.

```js
console.log(5 == "5");  // true
console.log(5 === "5"); // false
```

Do not say `==` always converts a string to a number. The conversion depends on the types being compared.

## 6. Truthy and falsy values — high-priority interview topic

JavaScript treats values as either **truthy** or **falsy** when it needs a true/false decision, such as inside an `if`.

### Falsy values to remember

These are the main falsy values:

- `false`
- `0`, `-0`, `0n`
- `""` (empty string)
- `null`
- `undefined`
- `NaN`

Almost every other value is truthy, including `"0"`, `"false"`, `[]`, and `{}`.

```js
if ("hello") {
  console.log("Runs"); // Runs
}

if (0) {
  console.log("Does not run");
}

console.log(Boolean(0));       // false
console.log(Boolean(1));       // true
console.log(Boolean(""));      // false
console.log(Boolean("hello")); // true
console.log(Boolean([]));      // true
console.log(Boolean({}));      // true
```

**Important correction:** `0` and `1` are numbers, not Boolean values. When converted to Boolean, `0` becomes `false` and `1` becomes `true`.

```js
console.log(0 == false);  // true
console.log(1 == true);   // true
console.log(0 === false); // false
console.log(1 === true);  // false
```

## 7. `undefined` vs. `null`

- `undefined`: a value is missing or has not been assigned.
- `null`: a value is deliberately set to mean “nothing here.”

```js
let a;
let b = null;

console.log(a); // undefined
console.log(b); // null
```

## 8. `NaN`

`NaN` means “Not a Number.” It appears when a numeric operation cannot produce a valid number.

```js
console.log(Number("hello")); // NaN
console.log(Number.isNaN(Number("hello"))); // true
```

A surprising rule: `NaN === NaN` is `false`. Use `Number.isNaN(value)` to check for `NaN`.

## 9. `||` vs. `??`

- `||` uses the right side when the left side is any falsy value.
- `??` uses the right side only when the left side is `null` or `undefined`.

```js
console.log(0 || 10);  // 10
console.log(0 ?? 10);  // 0
console.log(null ?? "Default"); // "Default"
```

Use `??` when `0`, `false`, or `""` can be valid values and you only want a fallback for missing values.

## 10. Optional chaining (`?.`)

Optional chaining safely checks a property when an earlier part might be `null` or `undefined`.

```js
const user = {};
console.log(user.address?.city); // undefined
```

Without `?.`, trying to read `city` from a missing `address` would cause an error.

## 11. `includes()` — checking whether a character exists

```js
const ch = "a";
console.log("aeiou".includes(ch)); // true

const other = "b";
console.log("aeiou".includes(other)); // false
```

`"aeiou".includes(ch)` checks whether the value in `ch` is found inside the string `"aeiou"`. It can be used to check whether a character is a vowel.

## 12. Primitive values vs. objects and arrays

- Primitive values include strings, numbers, booleans, `undefined`, `null`, `bigint`, and symbols.
- Objects and arrays can contain properties or items that can be changed.

```js
let x = 10;
let y = x;
y = 20;
console.log(x); // 10

const first = { score: 10 };
const second = first;
second.score = 20;
console.log(first.score); // 20
```

In the second example, both variables refer to the same object, so changing it through `second` is visible through `first`.

---

## Section A — Topics to revise first

Based on today's practice, give these extra attention:

1. **Truthy and falsy:** especially `0`, `1`, `""`, `"0"`, `[]`, and `{}`.
2. **`==` vs. `===`:** explain why `5 == "5"` is `true`, but `5 === "5"` is `false`.
3. **Hoisting and TDZ:** remember `var` gives `undefined` before assignment, while early access to `let`/`const` causes `ReferenceError`.
4. **Declaration, initialization, reassignment, redeclaration:** do not mix these four terms.
5. **`const` and mutation:** changing an object's property is allowed; assigning a new object to the same `const` variable is not.
6. **Boolean conversion:** `Boolean(0)` is `false`; `Boolean(1)` is `true`. But `0` and `1` themselves are numbers.
7. **`includes()`:** understand that it returns `true` if the searched text/character is present and `false` otherwise.

## Section B — High-frequency interview questions

### Q1. What are truthy and falsy values?
“Truthy values behave like `true` in a condition, and falsy values behave like `false`. For example, `0` is falsy, while `"0"` is truthy.”

### Q2. What is the difference between `==` and `===`?
“`==` allows type conversion before comparing. `===` checks both value and type without type conversion.”

### Q3. What is hoisting?
“JavaScript processes declarations before running the code. The result of using a variable early depends on whether it was declared with `var`, `let`, or `const`.”

### Q4. What is initialization?
“Initialization means giving a variable its first value.”

### Q5. What is TDZ?
“TDZ is the period before a `let` or `const` variable is initialized, when trying to access it causes a `ReferenceError`.”

### Q6. Can a `const` object be changed?
“Yes. `const` prevents assigning a new object to the variable, but its existing properties can still be changed.”

### Q7. What is the difference between `undefined` and `null`?
“`undefined` usually means no value has been assigned; `null` is used to deliberately represent no value.”

### Q8. What is the difference between `||` and `??`?
“`||` uses the fallback for any falsy value. `??` uses it only for `null` or `undefined`.”

---

## Section C — Code practice (try before checking answers)

Write the code yourself first. Then compare your output.

1. Print the numbers from 1 to 10.
2. Check whether a number is even or odd.
3. Find the square of a number.
4. Find the sum of the numbers from 1 to 10.
5. Find the factorial of a number.
6. Count the vowels in a string.
7. Predict the output of each snippet below.

### Output prediction

```js
console.log(0 == false);
console.log(0 === false);
console.log(Boolean("0"));
console.log(Boolean(""));
console.log([] == false);
console.log([] === false);
```

```js
console.log(5 == "5");
console.log(5 === "5");
console.log(0 || 7);
console.log(0 ?? 7);
```

```js
console.log(a);
var a = 10;
```

```js
console.log(b);
let b = 10;
```

### Answer key

```text
0 == false       -> true
0 === false      -> false
Boolean("0")     -> true
Boolean("")      -> false
[] == false      -> true
[] === false     -> false

5 == "5"         -> true
5 === "5"        -> false
0 || 7           -> 7
0 ?? 7            -> 0

console.log(a) before `var a = 10` -> undefined
console.log(b) before `let b = 10` -> ReferenceError
```

For the coding exercises, test your own solution in the browser console or Node.js. Focus on explaining your logic out loud, not just getting the output.

## Day 1 final checklist

- [ ] I can explain `var`, `let`, and `const`.
- [ ] I can tell reassignment from redeclaration.
- [ ] I can explain hoisting, initialization, and TDZ.
- [ ] I can identify common truthy and falsy values.
- [ ] I can explain `==` vs. `===`.
- [ ] I understand `undefined`, `null`, and `NaN`.
- [ ] I can explain `||`, `??`, optional chaining, and `includes()`.
- [ ] I have solved the coding questions without copying the answers.
