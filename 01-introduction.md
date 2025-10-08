## Introduction

```javascript
/**
 * JavaScript is a dynamic programming language where many operations
 * that are fixed at compile time in other languages are performed at runtime.
 * This makes it flexible and powerful for web development.
 */
```

---

## 1. Data Types

### 🔹 Primitive Data Types
*(Stored in Stack Memory - sequential storage)*

| Type | Description | Examples |
|------|-------------|----------|
| **String** | Textual data | `'Hello'`, `"World"`, `` `Template` `` |
| **Number** | Numeric values | `42`, `3.14`, `-5` |
| **Boolean** | Logical values | `true`, `false` |
| **Null** | Intentional absence | `null` |
| **Undefined** | Unassigned variable | `undefined` |

**Example Code:**
```javascript
// String
let singleQuotes = 'Hello World';
let doubleQuotes = "Hello World";
let backticks = `Hello World`;  // ES6 Template Literals

// Number
let integer = 42;
let decimal = 3.14;
let negative = -5;

// Boolean
let isTrue = true;
let isFalse = false;

// Null & Undefined
let emptyValue = null;
let notAssigned;
console.log(notAssigned);  // Output: undefined
```

### Reference Data Types
*(Stored in Heap Memory - non-sequential storage)*

| Type | Description | Example |
|------|-------------|---------|
| **Object** | Key-value pairs | `{name: "John", age: 30}` |
| **Array** | Ordered list | `[1, 2, 3, "hello"]` |
| **Function** | Reusable code | `function greet() { return "Hello!" }` |
| **Date** | Specific moment | `new Date()` |

**Example Code:**
```javascript
// Object
let person = {
    name: "John",
    age: 30,
    isStudent: false
};

// Array
let numbers = [1, 2, 3, 4, 5];
let mixedArray = [1, "hello", true, null];

// Function
function greet() {
    return "Hello!";
}

// Date
let currentDate = new Date();
```

---

## 2. Keywords

> **Keywords** are reserved words that have special meaning in JavaScript. They cannot be used as variable names or identifiers.

**Common Keywords:**
- `let`, `const`, `var`
- `if`, `else`, `switch`, `case`
- `for`, `while`, `do`
- `function`, `return`
- `class`, `extends`, `super`

---

## 3. Variable Declaration

### Comparison Table

| Feature | `var` | `let` | `const` |
|---------|-------|-------|---------|
| **Scope** | Function | Block | Block |
| **Redeclaration** | ✅ Allowed | ❌ Not allowed | ❌ Not allowed |
| **Reassignment** | ✅ Allowed | ✅ Allowed | ❌ Not allowed |
| **Hoisting** | ✅ (with undefined) | ✅ (Temporal Dead Zone) | ✅ (Temporal Dead Zone) |

### Detailed Examples

```javascript
// 🟡 var (ES1) - Function scoped
var score;              // Declaration
score = 100;            // Initialization
var score = 200;        // ✅ Redeclaration allowed
score = 300;            // ✅ Reassignment allowed

// 🟢 let (ES6) - Block scoped
let count;              // Declaration
count = 5;              // Initialization
// let count = 10;      // ❌ Error: Cannot redeclare
count = 10;             // ✅ Reassignment allowed

// 🔵 const (ES6) - Block scoped
const pi = 3.14;        // Declaration and initialization
// pi = 3.14159;        // ❌ Error: Cannot reassign
// const pi = 3.2;      // ❌ Error: Cannot redeclare
```

---

## 4. Scope

**Scope** defines the accessibility of variables, functions, and objects within the code.

```javascript
// 🌍 Global Scope - accessible everywhere
let globalVar = "I'm global";

{
    // 📦 Block Scope - accessible only within braces
    let blockVar = "I'm block scoped";
    console.log(blockVar);  // ✅ Works
    console.log(globalVar); // ✅ Works
}

// console.log(blockVar);  // ❌ Error: blockVar is not defined
console.log(globalVar);     // ✅ Works
```

---

## ⚙️ 5. Operators

### Arithmetic Operators

| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `+` | Addition | `5 + 3` | `8` |
| `-` | Subtraction | `5 - 3` | `2` |
| `*` | Multiplication | `5 * 3` | `15` |
| `/` | Division | `15 / 3` | `5` |
| `%` | Modulus | `15 % 4` | `3` |
| `++` | Increment | `x++` | `x + 1` |
| `--` | Decrement | `x--` | `x - 1` |

### Assignment Operators

| Operator | Example | Equivalent |
|----------|---------|------------|
| `=` | `x = 10` | `x = 10` |
| `+=` | `x += 5` | `x = x + 5` |
| `-=` | `x -= 3` | `x = x - 3` |
| `*=` | `x *= 2` | `x = x * 2` |
| `/=` | `x /= 4` | `x = x / 4` |
| `%=` | `x %= 4` | `x = x % 4` |

### Comparison Operators

| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `==` | Loose equality | `5 == "5"` | `true` |
| `===` | Strict equality | `5 === "5"` | `false` |
| `!=` | Loose inequality | `5 != "5"` | `false` |
| `!==` | Strict inequality | `5 !== "5"` | `true` |
| `>` | Greater than | `10 > 5` | `true` |
| `<` | Less than | `10 < 5` | `false` |
| `>=` | Greater than or equal | `10 >= 10` | `true` |
| `<=` | Less than or equal | `10 <= 5` | `false` |

### Logical Operators

| Operator | Description | Example | Result |
|----------|-------------|---------|--------|
| `&&` | AND | `true && false` | `false` |
| `\|\|` | OR | `true \|\| false` | `true` |
| `!` | NOT | `!true` | `false` |

**Code Examples:**
```javascript
// Arithmetic
let sum = 5 + 3;        // 8
let remainder = 15 % 4; // 3

// Assignment
let x = 10;
x += 5;                 // 15
x *= 2;                 // 30

// Comparison
console.log(5 === "5"); // false
console.log(10 > 5);    // true

// Logical
console.log(true && false); // false
console.log(true || false); // true
```

---

## 6. Naming Conventions

### 🐫 Camel Case (Most Common)
```javascript
let firstName = "John";
let totalAmount = 100;
let isUserLoggedIn = true;
```

### 🏛️ Pascal Case (Constructors/Classes)
```javascript
function Person() { }
class UserAccount { }
class DatabaseConnection { }
```

### Snake Case (Less Common)
```javascript
let first_name = "John";
let total_amount = 100;
let is_user_logged_in = true;
```

### ❌ What to Avoid
```javascript
// Don't use reserved keywords
// let let = 5;        // ❌ Error
// let function = 10;  // ❌ Error

// Don't start with numbers
// let 1stPlace = "first";  // ❌ Error

// Use meaningful names
let a = 5;              // ❌ Bad
let userAge = 25;       // ✅ Good
```

---

## 7. Comments

### Single Line Comments
```javascript
// This is a single line comment
let name = "John";  // Inline comment after code
```

### Multi-line Comments
```javascript
/*
 * This is a multi-line comment
 * Useful for longer explanations
 * or commenting out blocks of code
 */

/**
 * JSDoc style comments
 * @param {string} name - The name to greet
 * @returns {string} Greeting message
 */
function greet(name) {
    return `Hello, ${name}!`;
}
```

---

## Summary

| Concept | Key Points |
|---------|------------|
| **Data Types** | Primitives (Stack) vs Reference (Heap) |
| **Variables** | Use `const` by default, `let` when needed, avoid `var` |
| **Scope** | Global, Function, Block scope understanding |
| **Operators** | Arithmetic, Assignment, Comparison, Logical |
| **Naming** | CamelCase for variables, PascalCase for classes |

---