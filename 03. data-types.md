# JavaScript Data Types

## Table of Contents
- [Introduction to Data Types](#introduction-to-data-types)
- [Primitive Data Types](#primitive-data-types)
- [Reference Data Types](#reference-data-types)
- [Type Checking](#type-checking)
- [Type Conversion](#type-conversion)
- [Summary](#summary)

---

## Introduction to Data Types

JavaScript variables can hold different types of data values. Understanding these types is crucial for writing effective code.

### Two Main Categories:

1. **Primitive Types** - Stored directly in memory, immutable
2. **Reference Types** - Stored as references, mutable

---

## Primitive Data Types

Primitive types are stored in **Stack Memory** and are accessed directly by their value.

### 1. String - Textual Data
```javascript
// Different ways to create strings
let singleQuotes = 'Hello World';
let doubleQuotes = "Hello World";
let backticks = `Hello World`;  // Template literals (ES6)

// String operations
let firstName = "John";
let lastName = "Doe";
let fullName = firstName + " " + lastName; // String concatenation

console.log(fullName); // "John Doe"
```

### 2. Number - Numeric Values
```javascript
// Integer numbers
let age = 25;
let temperature = -5;

// Decimal numbers (floating point)
let price = 19.99;
let pi = 3.14159;

// Special numeric values
let infinity = Infinity;
let negativeInfinity = -Infinity;
let notANumber = NaN; // Not a Number

console.log(10 + 5);  // 15
console.log(10 / 3);  // 3.3333333333333335
```

### 3. Boolean - Logical Values
```javascript
let isLoggedIn = true;
let hasPermission = false;
let isGreater = 10 > 5; // true

// Boolean in conditions
if (isLoggedIn) {
    console.log("User is logged in");
} else {
    console.log("Please log in");
}
```

### 4. Undefined - Uninitialized Variable
```javascript
let notAssigned;
let emptyVariable;

console.log(notAssigned); // undefined
console.log(emptyVariable); // undefined

// Variables declared but not initialized are undefined
let score;
console.log(score); // undefined
```

### 5. Null - Intentional Absence of Value
```javascript
let emptyValue = null;
let noData = null;

console.log(emptyValue); // null

// Null represents "no value" intentionally set
let userPreference = null; // User hasn't set preference yet
```

### 6. BigInt - Large Integers
```javascript
// Regular number limit
let maxSafeInteger = 9007199254740991;

// BigInt for larger numbers
let bigNumber = 9007199254740992n;
let anotherBigInt = BigInt("12345678901234567890");

console.log(bigNumber); // 9007199254740992n
```

### 7. Symbol - Unique Identifiers
```javascript
// Create unique symbols
let id1 = Symbol("id");
let id2 = Symbol("id");

console.log(id1 === id2); // false - each Symbol is unique
```

---

## Reference Data Types

Reference types are stored in **Heap Memory** and accessed by reference.

### 1. Object - Key-Value Collections
```javascript
// Creating objects
let person = {
    name: "John",
    age: 30,
    isStudent: false
};

// Accessing object properties
console.log(person.name); // "John"
console.log(person["age"]); // 30
```

### 2. Array - Ordered Lists
```javascript
// Creating arrays
let numbers = [1, 2, 3, 4, 5];
let mixedArray = [1, "hello", true, null];

// Accessing array elements
console.log(numbers[0]); // 1
console.log(mixedArray[1]); // "hello"
```

### 3. Function - Reusable Code Blocks
```javascript
// Function declaration
function greet() {
    return "Hello World!";
}

// Function expression
let calculateSum = function(a, b) {
    return a + b;
};

console.log(greet()); // "Hello World!"
console.log(calculateSum(5, 3)); // 8
```

### 4. Date - Date and Time
```javascript
// Current date and time
let currentDate = new Date();
let specificDate = new Date("2023-12-25");

console.log(currentDate); // Current date and time
console.log(specificDate); // Christmas 2023
```

---

## Type Checking

### typeof Operator
```javascript
// Checking primitive types
console.log(typeof "hello");        // "string"
console.log(typeof 42);            // "number"
console.log(typeof true);          // "boolean"
console.log(typeof undefined);     // "undefined"
console.log(typeof null);          // "object" (historical bug)
console.log(typeof 123n);          // "bigint"
console.log(typeof Symbol("id"));  // "symbol"

// Checking reference types
console.log(typeof {});            // "object"
console.log(typeof []);            // "object"
console.log(typeof function() {}); // "function"
console.log(typeof new Date());    // "object"
```

### Checking for null and Arrays
```javascript
// Proper null check
let value = null;
console.log(value === null); // true

// Array check
let arr = [1, 2, 3];
console.log(Array.isArray(arr)); // true
console.log(typeof arr); // "object"
```

---

## Type Conversion

### Explicit Type Conversion
```javascript
// String conversion
let num = 123;
let str = String(num);
console.log(str); // "123"
console.log(typeof str); // "string"

// Number conversion
let numericString = "456";
let convertedNum = Number(numericString);
console.log(convertedNum); // 456
console.log(typeof convertedNum); // "number"

// Boolean conversion
let truthyValue = Boolean(1); // true
let falsyValue = Boolean(0); // false
```

### Implicit Type Conversion (Coercion)
```javascript
// String coercion
let result1 = "5" + 1; // "51" - number converted to string
let result2 = "5" - 1; // 4 - string converted to number

// Boolean coercion
if ("hello") { // "hello" coerced to true
    console.log("This will run");
}

if (0) { // 0 coerced to false
    console.log("This won't run");
}
```

### Truthy and Falsy Values
```javascript
// Falsy values (become false in boolean context)
false
0
"" (empty string)
null
undefined
NaN

// Truthy values (become true in boolean context)
true
1 (any non-zero number)
"hello" (any non-empty string)
[] (empty array)
{} (empty object)
```

---

## Memory Management

### Primitive Types (Stack)
```javascript
let a = 10;
let b = a; // b gets a copy of the value

a = 20;
console.log(a); // 20
console.log(b); // 10 - unchanged
```

### Reference Types (Heap)
```javascript
let obj1 = { name: "John" };
let obj2 = obj1; // obj2 references the same object

obj1.name = "Jane";
console.log(obj1.name); // "Jane"
console.log(obj2.name); // "Jane" - both changed
```

---

## Summary

### Primitive Types Quick Reference -

| Type | Description | Example | typeof |
|------|-------------|---------|--------|
| **String** | Text data | `"hello"` | `"string"` |
| **Number** | Numeric values | `42`, `3.14` | `"number"` |
| **Boolean** | True/False | `true`, `false` | `"boolean"` |
| **Undefined** | Uninitialized | `undefined` | `"undefined"` |
| **Null** | No value | `null` | `"object"` |
| **BigInt** | Large integers | `123n` | `"bigint"` |
| **Symbol** | Unique IDs | `Symbol()` | `"symbol"` |

### Reference Types Quick Reference -

| Type | Description | Example |
|------|-------------|---------|
| **Object** | Key-value pairs | `{key: "value"}` |
| **Array** | Ordered lists | `[1, 2, 3]` |
| **Function** | Reusable code | `function() {}` |
| **Date** | Date/time | `new Date()` |

### Key Points to Remember:

1. **Primitives** are immutable and compared by value
2. **References** are mutable and compared by reference
3. Use `typeof` to check types (except for `null` and arrays)
4. Understand type conversion for effective programming
5. Choose the right data type for your needs
