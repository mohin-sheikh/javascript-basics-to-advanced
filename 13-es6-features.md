# ES6+ Features

## Table of Contents
- [Introduction to ES6+](#introduction-to-es6)
- [Variable Declarations](#variable-declarations)
- [Arrow Functions](#arrow-functions)
- [Template Literals](#template-literals)
- [Destructuring](#destructuring)
- [Enhanced Object Literals](#enhanced-object-literals)
- [Spread and Rest Operators](#spread-and-rest-operators)
- [Default Parameters](#default-parameters)
- [Modules](#modules)
- [Promises](#promises)
- [Classes](#classes)
- [New Data Structures](#new-data-structures)
- [String and Array Methods](#string-and-array-methods)
- [Summary](#summary)

---

## Introduction to ES6+

ES6 (ECMAScript 2015) was a major update to JavaScript that introduced many new features making JavaScript more powerful and easier to work with.

### What is ES6+?
- **ES6**: ECMAScript 2015 - Major JavaScript update
- **ES6+**: ES6 and all subsequent versions (ES7, ES8, etc.)
- **Modern JavaScript**: Code written using ES6+ features

---

## Variable Declarations

### `let` and `const`
**Replaced `var` for better variable scoping**

```javascript
// let - for variables that change
let count = 0;
count = 1; // Allowed

// const - for constants
const PI = 3.14159;
// PI = 3.14; // Error: Assignment to constant
```

**Detailed Explanation**: See [`02-variables-and-scope.md`](02-variables-and-scope.md)

---

## Arrow Functions

### Shorter function syntax
```javascript
// Traditional function
function add(a, b) {
    return a + b;
}

// Arrow function
const add = (a, b) => a + b;
```

### Key Features:
- Shorter syntax
- No `this` binding
- Implicit return for single expressions

**Detailed Explanation**: See [`08-functions-and-types.md`](08-functions-and-types.md)

---

## Template Literals

### String interpolation and multi-line strings
```javascript
// Traditional strings
let message = "Hello " + name + "!";

// Template literals
let message = `Hello ${name}!`;

// Multi-line strings
let html = `
  <div>
    <h1>${title}</h1>
  </div>
`;
```

**Detailed Explanation**: See [`04-template-literals-operators.md`](04-template-literals-operators.md)

---

## Destructuring

### Extract values from arrays and objects

#### Array Destructuring
```javascript
const numbers = [1, 2, 3];
const [first, second] = numbers;
console.log(first); // 1
```

#### Object Destructuring
```javascript
const person = { name: "John", age: 30 };
const { name, age } = person;
console.log(name); // "John"
```

### Use Cases:
- Function parameters
- Extracting data from API responses
- Swapping variables

---

## Enhanced Object Literals

### Shorter object syntax
```javascript
// ES5
var obj = {
    name: name,
    age: age,
    sayHello: function() {
        return "Hello";
    }
};

// ES6
const obj = {
    name,        // Shorthand for name: name
    age,         // Shorthand for age: age
    sayHello() { // Method shorthand
        return "Hello";
    }
};
```

---

## Spread and Rest Operators

### Spread Operator (`...`)
```javascript
// Copy arrays
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5]; // [1, 2, 3, 4, 5]

// Copy objects
const obj1 = { a: 1, b: 2 };
const obj2 = { ...obj1, c: 3 }; // { a: 1, b: 2, c: 3 }
```

### Rest Operator (`...`)
```javascript
// Function parameters
function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
}
sum(1, 2, 3, 4); // 10
```

**Related**: See [`07-shallow-deep-copy.md`](07-shallow-deep-copy.md) for copying objects

---

## Default Parameters

### Set default values for function parameters
```javascript
// ES5
function greet(name) {
    name = name || 'Guest';
    return "Hello " + name;
}

// ES6
function greet(name = 'Guest') {
    return `Hello ${name}`;
}

greet(); // "Hello Guest"
```

**Detailed Explanation**: See [`08-functions-and-types.md`](08-functions-and-types.md)

---

## Modules

### Export and import code between files

#### Exporting
```javascript
// Named exports
export const PI = 3.14159;
export function calculateArea(radius) {
    return PI * radius * radius;
}

// Default export
export default class Calculator {
    // class code
}
```

#### Importing
```javascript
// Named imports
import { PI, calculateArea } from './math.js';

// Default import
import Calculator from './calculator.js';

// Import everything
import * as math from './math.js';
```

---

## Promises

### Handle asynchronous operations
```javascript
const fetchData = new Promise((resolve, reject) => {
    // Async operation
    if (success) {
        resolve(data);
    } else {
        reject(error);
    }
});

fetchData
    .then(data => console.log(data))
    .catch(error => console.log(error));
```

**Detailed Explanation**: See [`12-promises-complete-guide.md`](12-promises-complete-guide.md)

---

## Classes

### Object-oriented programming syntax
```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
    
    greet() {
        return `Hello, I'm ${this.name}`;
    }
    
    // Static method
    static species() {
        return "Homo sapiens";
    }
}

class Student extends Person {
    constructor(name, age, grade) {
        super(name, age);
        this.grade = grade;
    }
}
```

---

## New Data Structures

### Map
```javascript
const map = new Map();
map.set('name', 'John');
map.set('age', 30);
console.log(map.get('name')); // "John"
```

### Set
```javascript
const set = new Set([1, 2, 3, 3, 4]);
console.log([...set]); // [1, 2, 3, 4] (no duplicates)
```

### Symbol
```javascript
const uniqueKey = Symbol('description');
const obj = {
    [uniqueKey]: 'unique value'
};
```

---

## String and Array Methods

### New String Methods
```javascript
// includes()
"Hello".includes("ell"); // true

// startsWith() / endsWith()
"Hello".startsWith("He"); // true

// repeat()
"Hello".repeat(3); // "HelloHelloHello"
```

### New Array Methods
```javascript
// find() and findIndex()
[1, 5, 10].find(x => x > 3); // 5

// includes()
[1, 2, 3].includes(2); // true

// Array.from()
Array.from("hello"); // ['h', 'e', 'l', 'l', 'o']
```

**Detailed Explanation**: See [`05-string-methods.md`](05-string-methods.md) and [`09-arrays-and-methods.md`](09-arrays-and-methods.md)

---

## Additional ES7+ Features

### ES7 (2016)
```javascript
// Exponentiation operator
2 ** 3; // 8 (instead of Math.pow(2, 3))

// Array.includes()
[1, 2, 3].includes(2); // true
```

### ES8 (2017)
```javascript
// Async/Await
async function fetchData() {
    const data = await apiCall();
    return data;
}

// Object.values() / Object.entries()
Object.values({a: 1, b: 2}); // [1, 2]
Object.entries({a: 1, b: 2}); // [['a', 1], ['b', 2]]
```

### ES9 (2018)
```javascript
// Rest/Spread for objects
const { a, ...rest } = { a: 1, b: 2, c: 3 };
// rest = { b: 2, c: 3 }

// Promise.finally()
promise
    .then(...)
    .catch(...)
    .finally(() => console.log('Done'));
```

### ES10 (2019)
```javascript
// Array.flat() and Array.flatMap()
[1, [2, [3]]].flat(2); // [1, 2, 3]

// Object.fromEntries()
Object.fromEntries([['a', 1], ['b', 2]]); // {a: 1, b: 2}

// String.trimStart() and String.trimEnd()
"  hello  ".trimStart(); // "hello  "
```

---

## Summary

### Most Used ES6+ Features:

| Feature | Purpose | File Reference |
|---------|---------|----------------|
| `let/const` | Better variable scoping | [`02-variables-and-scope.md`](02-variables-and-scope.md) |
| **Arrow Functions** | Shorter function syntax | [`08-functions-and-types.md`](08-functions-and-types.md) |
| **Template Literals** | String interpolation | [`04-template-literals-operators.md`](04-template-literals-operators.md) |
| **Destructuring** | Extract values easily | - |
| **Spread/Rest** | Copy and combine data | [`07-shallow-deep-copy.md`](07-shallow-deep-copy.md) |
| **Modules** | Code organization | - |
| **Promises** | Async operations | [`12-promises-complete-guide.md`](12-promises-complete-guide.md) |
| **Classes** | OOP syntax | - |

### Why Use ES6+?
1. **Cleaner Code** - Less boilerplate
2. **Better Readability** - More expressive syntax
3. **Enhanced Features** - More built-in functionality
4. **Modern Standards** - Industry best practices
5. **Better Tooling** - Improved developer experience

### Browser Support
- All modern browsers support ES6+
- Use Babel to transpile for older browsers
- Node.js has excellent ES6+ support

---