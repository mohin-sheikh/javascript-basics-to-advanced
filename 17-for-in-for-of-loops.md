# JavaScript For...in and For...of Loops

## Table of Contents
- [Introduction](#introduction)
- [For...in Loop](#forin-loop)
- [For...of Loop](#forof-loop)
- [Key Differences](#key-differences)
- [When to Use Each](#when-to-use-each)
- [Summary](#summary)

---

## Introduction

JavaScript provides two special loops for different types of collections →
- **For...in** - for object properties
- **For...of** - for iterable values

---

## For...in Loop

### Definition
The **for...in** loop iterates over the enumerable properties of an object.

### Syntax
```javascript
for (key in object) {
    // code to execute
}
```

### Basic Example
```javascript
const person = {
    name: "John",
    age: 30,
    city: "New York"
};

for (let key in person) {
    console.log(key + ": " + person[key]);
}
// Output:
// name: John
// age: 30
// city: New York
```

### With Arrays (Not Recommended)
```javascript
const colors = ["red", "green", "blue"];

for (let index in colors) {
    console.log(index + ": " + colors[index]);
}
// Output:
// 0: red
// 1: green
// 2: blue
```

---

## For...of Loop

### Definition
The **for...of** loop iterates over the values of iterable objects (arrays, strings, etc.).

### Syntax
```javascript
for (value of iterable) {
    // code to execute
}
```

### Basic Example
```javascript
const fruits = ["apple", "banana", "orange"];

for (let fruit of fruits) {
    console.log(fruit);
}
// Output →
// apple
// banana
// orange
```

### With Strings
```javascript
const message = "Hello";

for (let char of message) {
    console.log(char);
}
// Output →
// H
// e
// l
// l
// o
```

---

## Key Differences

### For...in vs For...of

| Aspect | For...in | For...of |
|--------|----------|----------|
| **Iterates over** | Object properties | Iterable values |
| **Returns** | Keys/indexes | Values |
| **Use with Objects** | ✅ Yes | ❌ No |
| **Use with Arrays** | ❌ Not recommended | ✅ Yes |
| **Use with Strings** | ❌ No | ✅ Yes |

### Comparison Example
```javascript
const array = ["a", "b", "c"];

// For...in (gets indexes)
for (let index in array) {
    console.log(index); // 0, 1, 2
}

// For...of (gets values)
for (let value of array) {
    console.log(value); // a, b, c
}
```

---

## When to Use Each

### Use For...in for →
- Object properties
- When you need keys
- Object iteration

```javascript
const car = {
    brand: "Toyota",
    model: "Camry",
    year: 2020
};

for (let property in car) {
    console.log(property); // brand, model, year
}
```

### Use For...of for →
- Array values
- String characters
- Any iterable object
- When you need values

```javascript
const numbers = [1, 2, 3, 4, 5];

for (let number of numbers) {
    console.log(number); // 1, 2, 3, 4, 5
}
```

---

## Summary

### Quick Reference

#### For...in Loop
```javascript
// For objects
for (let key in object) {
    console.log(key, object[key]);
}
```

#### For...of Loop
```javascript
// For arrays, strings
for (let value of iterable) {
    console.log(value);
}
```

### Simple Rules
1. **Use for...in** for objects
2. **Use for...of** for arrays and strings
3. **Avoid for...in** with arrays
4. **for...of** doesn't work with plain objects

### Remember
- **for...in** → properties/keys
- **for...of** → values

---