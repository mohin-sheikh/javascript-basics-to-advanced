# JavaScript Variables Declaration and Scoping

## Table of Contents
- [Variable Declaration](#variable-declaration)
- [Scope in JavaScript](#scope-in-javascript)
- [Variable Comparison](#variable-comparison)
- [Best Practices](#best-practices)

---

## Variable Declaration

JavaScript provides three ways to declare variables, each with different behaviors and use cases.

### var (ES1 - Function Scoped)
```javascript
// Declaration
var score;

// Initialization
score = 100;

// Redeclaration allowed in same scope
var score = 200;

// Reassignment allowed
score = 300;

console.log(score); // 300
```

### let (ES6 - Block Scoped)
```javascript
// Declaration
let count;

// Initialization
count = 5;

// Reassignment allowed
count = 10;

// Cannot redeclare in same scope
// let count = 15; // Error: Identifier 'count' has already been declared

console.log(count); // 10
```

### const (ES6 - Block Scoped)
```javascript
// Must be initialized during declaration
const PI = 3.14159;
const MAX_USERS = 100;

// Cannot be reassigned
// PI = 3.14; // Error: Assignment to constant variable

// Cannot be redeclared
// const PI = 3.2; // Error: Identifier 'PI' has already been declared

console.log(PI); // 3.14159
```

---

## Scope in JavaScript

Scope defines where variables can be accessed in your code.

### Global Scope
Variables declared outside any block or function
```javascript
// Global variables
var globalVar = "I'm global with var";
let globalLet = "I'm global with let";
const globalConst = "I'm global with const";

// All three are accessible from anywhere
console.log(globalVar); // Works
console.log(globalLet); // Works
console.log(globalConst); // Works
```

### Block Scope (Introduced in ES6)
Variables declared with let and const are block-scoped
```javascript
// Block scope example with if statement
if (true) {
    var insideVar = "I'm var inside block";
    let insideLet = "I'm let inside block";
    const insideConst = "I'm const inside block";
    
    console.log(insideVar); // Works
    console.log(insideLet); // Works
    console.log(insideConst); // Works
}

console.log(insideVar); // Works - var is accessible outside block
// console.log(insideLet); // Error: insideLet is not defined
// console.log(insideConst); // Error: insideConst is not defined
```

### Function Scope vs Block Scope Comparison
```javascript
// Function scope demonstration
function demonstrateFunctionScope() {
    if (true) {
        var functionScoped = "I'm function scoped (var)";
        let blockScoped = "I'm block scoped (let)";
    }
    console.log(functionScoped); // Works - var is function scoped
    // console.log(blockScoped); // Error - let is block scoped
}

// Block scope demonstration with loops
for (let i = 0; i < 3; i++) {
    // i is only accessible inside this block
    console.log(i); // Works: 0, 1, 2
}
// console.log(i); // Error: i is not defined

for (var j = 0; j < 3; j++) {
    console.log(j); // Works: 0, 1, 2
}
console.log(j); // Works: 3 - var is accessible outside loop
```

### Practical Scope Examples
```javascript
// Example 1: Simple block
{
    var a = 10;
    let b = 20;
    const c = 30;
}
console.log(a); // 10 - var is accessible
// console.log(b); // Error
// console.log(c); // Error

// Example 2: Multiple blocks
let x = 100; // Global let

{
    let x = 200; // Different variable, same name
    console.log(x); // 200
}

console.log(x); // 100 - global x unchanged

// Example 3: const in blocks
const version = "1.0";

{
    const version = "2.0"; // Different constant, same name
    console.log(version); // "2.0"
}

console.log(version); // "1.0" - global version unchanged
```

---

## Variable Comparison

### Declaration Comparison Table

| Feature | var | let | const |
|---------|-----|-----|-------|
| **Scope** | Function | Block | Block |
| **Redeclaration** | Allowed | Not allowed | Not allowed |
| **Reassignment** | Allowed | Allowed | Not allowed |
| **Initialization** | Optional | Optional | Required |

### Scope Behavior Examples
```javascript
// Demonstrating different scoping behaviors

// Global level
var global1 = "global var";
let global2 = "global let";
const global3 = "global const";

// Block level demonstration
if (true) {
    var blockVar = "block var";
    let blockLet = "block let";
    const blockConst = "block const";
    
    console.log(global1); // Accessible
    console.log(global2); // Accessible
    console.log(global3); // Accessible
}

console.log(blockVar); // Accessible - var leaks out
// console.log(blockLet); // Error - let is block scoped
// console.log(blockConst); // Error - const is block scoped
```

### Temporal Dead Zone (TDZ)
```javascript
// var - hoisted and initialized with undefined
console.log(hoistedVar); // undefined
var hoistedVar = "I'm hoisted";

// let/const - hoisted but not initialized (TDZ)
// console.log(hoistedLet); // Error: Cannot access before initialization
let hoistedLet = "I'm in TDZ";

// console.log(hoistedConst); // Error: Cannot access before initialization
const hoistedConst = "I'm in TDZ";
```

---

## Best Practices

### 1. Prefer const by Default
```javascript
// Use const for values that shouldn't change
const API_KEY = "abc123";
const MAX_FILE_SIZE = 1024;
const DEFAULT_TIMEOUT = 5000;

// If you need to reassign, use let
let userCount = 0;
userCount = 5; // Reassignment needed

// Avoid var in modern JavaScript
// var oldVariable = "avoid this"; // Not recommended
```

### 2. Meaningful Variable Names
```javascript
// Good naming
const userName = "John";
let itemCount = 5;
const isActive = true;

// Avoid single letters (except in loops)
// let x = 5; // Not descriptive
let score = 5; // Descriptive
```

### 3. Scope Management
```javascript
// Keep variables in smallest possible scope
function calculateTotal(price, quantity) {
    // taxRate is only needed inside this calculation
    const taxRate = 0.08;
    let subtotal = price * quantity;
    let tax = subtotal * taxRate;
    return subtotal + tax;
}

// taxRate is not accessible outside, which is good
```

### 4. Avoid Global Pollution
```javascript
// Instead of many global variables
// var config1 = value1;
// var config2 = value2;

// Use a single global object if needed
const AppConfig = {
    theme: "dark",
    language: "en",
    version: "1.0.0"
};
```

### 5. Declaration Guidelines
```javascript
// Declare variables at the top of their scope
function processData(input) {
    // Declare all variables first
    let result;
    let isValid;
    const MAX_LENGTH = 100;
    
    // Then use them
    isValid = input.length <= MAX_LENGTH;
    
    if (isValid) {
        result = input.toUpperCase();
    }
    
    return result;
}
```

## Summary

- **Use `const`** for values that don't change
- **Use `let`** for values that need reassignment
- **Avoid `var`** in modern JavaScript
- **Block scope** (`let`/`const`) helps prevent bugs
- **Keep variables** in the smallest scope needed
- **Initialize variables** when you declare them