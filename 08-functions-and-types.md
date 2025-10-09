# JavaScript Functions - Complete Guide

## Table of Contents
- [What are Functions?](#what-are-functions)
- [Function Declaration](#function-declaration)
- [Function Expression](#function-expression)
- [Arrow Functions](#arrow-functions)
- [Immediately Invoked Function Expressions (IIFE)](#immediately-invoked-function-expressions-iife)
- [Function Parameters and Arguments](#function-parameters-and-arguments)
- [Return Statement](#return-statement)
- [Function Scope](#function-scope)
- [Summary](#summary)

---

## What are Functions?

**Functions** are reusable blocks of code that perform specific tasks.

### Simple Definition
Functions are like machines that take input, process it, and return output.

```javascript
// Simple function example
function greet() {
    console.log("Hello, World!");
}

// Using the function
greet(); // "Hello, World!"
```

### Why Use Functions?
- **Reusability** → Write once, use multiple times
- **Organization** → Break code into logical pieces
- **Maintainability** → Easier to fix and update
- **Testing** → Test individual pieces of code

---

## Function Declaration

### Definition
A function that's declared using the `function` keyword.

```javascript
// Function declaration
function sayHello() {
    console.log("Hello!");
}

// Calling the function
sayHello(); // "Hello!"
```

### Function with Parameters
```javascript
function greet(name) {
    console.log("Hello, " + name + "!");
}

greet("John"); // "Hello, John!"
greet("Sarah"); // "Hello, Sarah!"
```

### Function with Return Value
```javascript
function add(a, b) {
    return a + b;
}

let result = add(5, 3);
console.log(result); // 8
```

### Characteristics
- **Hoisted** → Can be called before declaration
- **Named** → Has a function name
- **Reusable** → Can be called multiple times

---

## Function Expression

### Definition
A function stored in a variable.

```javascript
// Function expression
const sayHello = function() {
    console.log("Hello!");
};

sayHello(); // "Hello!"
```

### Function Expression with Parameters
```javascript
const multiply = function(a, b) {
    return a * b;
};

let result = multiply(4, 5);
console.log(result); // 20
```

### Characteristics
- **Not hoisted** → Cannot be called before declaration
- **Can be anonymous** → No function name required
- **Flexible** → Can be assigned to different variables

---

## Arrow Functions

### Definition
A shorter syntax for writing functions (introduced in ES6).

```javascript
// Arrow function
const greet = () => {
    console.log("Hello!");
};

greet(); // "Hello!"
```

### Arrow Function Variations

#### Single Parameter (No parentheses needed)
```javascript
const square = x => {
    return x * x;
};

console.log(square(5)); // 25
```

#### Single Expression (Implicit return)
```javascript
const square = x => x * x;
console.log(square(5)); // 25

const add = (a, b) => a + b;
console.log(add(2, 3)); // 5
```

#### Multiple Parameters
```javascript
const multiply = (a, b) => {
    return a * b;
};

console.log(multiply(4, 5)); // 20
```

#### No Parameters
```javascript
const sayHello = () => {
    console.log("Hello!");
};

sayHello(); // "Hello!"
```

### Characteristics
- **Shorter syntax** → More concise than regular functions
- **No `this` binding** → `this` refers to surrounding context
- **Implicit return** → Single expressions return automatically
- **Not hoisted** → Cannot be called before declaration

---

## Immediately Invoked Function Expressions (IIFE)

### Definition
A function that runs immediately after it's defined.

```javascript
// IIFE syntax
(function() {
    console.log("This runs immediately!");
})();

// With parameters
(function(name) {
    console.log("Hello, " + name + "!");
})("John");
```

### Arrow Function IIFE
```javascript
(() => {
    console.log("Arrow IIFE running!");
})();
```

### Use Cases
- **Create private scope** → Variables inside aren't accessible outside
- **Avoid global pollution** → Keep variables contained
- **Initialization code** → Run setup code immediately

```javascript
// Creating private variables
const counter = (function() {
    let count = 0;
    
    return {
        increment: function() {
            count++;
            return count;
        },
        getCount: function() {
            return count;
        }
    };
})();

console.log(counter.increment()); // 1
console.log(counter.increment()); // 2
console.log(counter.getCount()); // 2
```

---

## Function Parameters and Arguments

### Parameters vs Arguments
- **Parameters** → Variables in function definition
- **Arguments** → Actual values passed to function

```javascript
// Parameters: a and b
function multiply(a, b) {
    return a * b;
}

// Arguments: 4 and 5
let result = multiply(4, 5);
```

### Default Parameters
```javascript
function greet(name = "Guest") {
    console.log("Hello, " + name + "!");
}

greet("John"); // "Hello, John!"
greet(); // "Hello, Guest!"
```

### Rest Parameters
```javascript
function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
}

console.log(sum(1, 2, 3)); // 6
console.log(sum(1, 2, 3, 4, 5)); // 15
```

---

## Return Statement

### Definition
Specifies the value that a function returns.

```javascript
function add(a, b) {
    return a + b; // Returns the sum
}

let result = add(2, 3); // result = 5
```

### Functions Without Return
```javascript
function logMessage(message) {
    console.log(message);
    // No return statement
}

let result = logMessage("Hello");
console.log(result); // undefined
```

### Multiple Return Points
```javascript
function checkNumber(num) {
    if (num > 0) {
        return "Positive";
    } else if (num < 0) {
        return "Negative";
    } else {
        return "Zero";
    }
}

console.log(checkNumber(5)); // "Positive"
console.log(checkNumber(-3)); // "Negative"
console.log(checkNumber(0)); // "Zero"
```

---

## Function Scope

### Local Scope
Variables declared inside a function are local to that function.

```javascript
function myFunction() {
    let localVar = "I'm local";
    console.log(localVar); // Works
}

myFunction();
// console.log(localVar); // Error: localVar is not defined
```

### Global Scope
Variables declared outside functions are global.

```javascript
let globalVar = "I'm global";

function showGlobal() {
    console.log(globalVar); // Works
}

showGlobal(); // "I'm global"
console.log(globalVar); // "I'm global"
```

### Block Scope in Functions
```javascript
function demonstrateScope() {
    if (true) {
        let blockScoped = "I'm block scoped";
        var functionScoped = "I'm function scoped";
    }
    
    // console.log(blockScoped); // Error
    console.log(functionScoped); // Works
}
```

---

## Practical Examples

### Example 1 → Calculator Functions
```javascript
// Function declarations
function add(a, b) {
    return a + b;
}

function subtract(a, b) {
    return a - b;
}

// Function expressions
const multiply = function(a, b) {
    return a * b;
};

// Arrow functions
const divide = (a, b) => a / b;

// Usage
console.log(add(10, 5)); // 15
console.log(subtract(10, 5)); // 5
console.log(multiply(10, 5)); // 50
console.log(divide(10, 5)); // 2
```

### Example 2: User Management
```javascript
// Function with default parameters
function createUser(name, age = 18, isActive = true) {
    return {
        name: name,
        age: age,
        isActive: isActive,
        createdAt: new Date()
    };
}

// Arrow function with implicit return
const formatUser = user => `${user.name} (${user.age})`;

// Usage
let user1 = createUser("John", 25);
let user2 = createUser("Sarah"); // Uses default age

console.log(formatUser(user1)); // "John (25)"
console.log(formatUser(user2)); // "Sarah (18)"
```

### Example 3: Array Processing
```javascript
// Function declaration for complex logic
function processNumbers(numbers) {
    if (!Array.isArray(numbers)) {
        return "Invalid input";
    }
    
    return numbers
        .filter(num => num > 0) // Keep positive numbers
        .map(num => num * 2)    // Double each number
        .reduce((sum, num) => sum + num, 0); // Sum all numbers
}

// Arrow function for simple operations
const quickAdd = (a, b, c) => a + b + c;

// Usage
let numbers = [1, -2, 3, -4, 5];
console.log(processNumbers(numbers)); // 18 (1*2 + 3*2 + 5*2)
console.log(quickAdd(1, 2, 3)); // 6
```

---

## Summary

### Function Types Comparison

| Type | Syntax | Hoisted | `this` Binding | Use Case |
|------|--------|---------|----------------|----------|
| **Declaration** | `function name() {}` | ✅ Yes | ✅ Yes | General purpose |
| **Expression** | `const name = function() {}` | ❌ No | ✅ Yes | Flexible assignment |
| **Arrow** | `const name = () => {}` | ❌ No | ❌ No | Callbacks, short functions |
| **IIFE** | `(function() {})()` | ❌ No | ✅ Yes | Immediate execution |

### Key Concepts

#### Parameters vs Arguments
```javascript
// Parameters (a, b)
function multiply(a, b) {
    return a * b;
}

// Arguments (5, 3)
let result = multiply(5, 3);
```

#### Return Values
```javascript
function withReturn() {
    return "Hello"; // Returns value
}

function withoutReturn() {
    console.log("Hello"); // Returns undefined
}
```

#### Scope Rules
```javascript
let global = "I'm global";

function testScope() {
    let local = "I'm local";
    console.log(global); // ✅ Works
    console.log(local);  // ✅ Works
}

testScope();
console.log(global); // ✅ Works
// console.log(local); // ❌ Error
```

### Best Practices
1. Use **function declarations** for main logic
2. Use **arrow functions** for callbacks and short functions
3. Use **default parameters** for optional values
4. Use **meaningful names** that describe what the function does
5. Keep functions **small and focused** on one task
6. Use **return statements** consistently
7. Document complex functions with comments

### Common Patterns
```javascript
// Function that returns a value
function calculate(a, b) {
    return a * b;
}

// Function that performs an action
function logMessage(message) {
    console.log(message);
}

// Function that returns multiple values (as object)
function getUser() {
    return {
        name: "John",
        age: 30
    };
}

// Higher-order function (takes or returns functions)
function createMultiplier(multiplier) {
    return function(number) {
        return number * multiplier;
    };
}
```

---