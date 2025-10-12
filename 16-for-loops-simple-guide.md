# JavaScript For Loops
## Table of Contents
- [What are Loops?](#what-are-loops)
- [Basic For Loop](#basic-for-loop)
- [Looping Through Arrays](#looping-through-arrays)
- [Common Loop Patterns](#common-loop-patterns)
- [Loop Control](#loop-control)
- [Summary](#summary)

---

## What are Loops?

### Definition
**Loops** are used to execute the same block of code multiple times.

### Simple Definition
Loops let you repeat actions without writing the same code over and over.

### Why Use Loops?
- Repeat actions
- Process lists of data
- Automate repetitive tasks

---

## Basic For Loop

### Syntax
```javascript
for (initialization; condition; increment) {
    // code to repeat
}
```

### Simple Example
```javascript
// Print numbers 1 to 5
for (let i = 1; i <= 5; i++) {
    console.log(i);
}
// Output: 1, 2, 3, 4, 5
```

### How It Works
```javascript
for (let i = 0; i < 3; i++) {
    console.log("Hello " + i);
}
// Output:
// Hello 0
// Hello 1
// Hello 2
```

### Step-by-Step Breakdown
```javascript
// Step 1: let i = 0 (initialize counter)
// Step 2: i < 3 (check condition)
// Step 3: Execute code inside loop
// Step 4: i++ (increment counter)
// Step 5: Repeat from step 2 until condition is false
```

---

## Looping Through Arrays

### Basic Array Looping
```javascript
const fruits = ["apple", "banana", "orange"];

for (let i = 0; i < fruits.length; i++) {
    console.log(fruits[i]);
}
// Output:
// apple
// banana
// orange
```

### Array with Index
```javascript
const colors = ["red", "green", "blue"];

for (let i = 0; i < colors.length; i++) {
    console.log(i + ": " + colors[i]);
}
// Output:
// 0: red
// 1: green
// 2: blue
```

### Modifying Array Elements
```javascript
const numbers = [1, 2, 3, 4, 5];

for (let i = 0; i < numbers.length; i++) {
    numbers[i] = numbers[i] * 2;
}

console.log(numbers); // [2, 4, 6, 8, 10]
```

---

## Common Loop Patterns

### Count Down
```javascript
// Count from 10 to 1
for (let i = 10; i >= 1; i--) {
    console.log(i);
}
// Output: 10, 9, 8, 7, 6, 5, 4, 3, 2, 1
```

### Even Numbers
```javascript
// Print even numbers from 2 to 10
for (let i = 2; i <= 10; i += 2) {
    console.log(i);
}
// Output: 2, 4, 6, 8, 10
```

### Multiplication Table
```javascript
// 5 times table
for (let i = 1; i <= 10; i++) {
    console.log(`5 × ${i} = ${5 * i}`);
}
// Output:
// 5 × 1 = 5
// 5 × 2 = 10
// 5 × 3 = 15
// ... up to 50
```

### String Characters
```javascript
const word = "hello";

for (let i = 0; i < word.length; i++) {
    console.log(word[i]);
}
// Output:
// h
// e
// l
// l
// o
```

---

## Loop Control

### Break Statement
```javascript
// Stop loop when condition is met
for (let i = 1; i <= 10; i++) {
    if (i === 5) {
        break; // Stop the loop
    }
    console.log(i);
}
// Output: 1, 2, 3, 4
```

### Continue Statement
```javascript
// Skip specific iterations
for (let i = 1; i <= 5; i++) {
    if (i === 3) {
        continue; // Skip this iteration
    }
    console.log(i);
}
// Output: 1, 2, 4, 5
```

### Practical Example: Search in Array
```javascript
const numbers = [10, 20, 30, 40, 50];
let found = false;

for (let i = 0; i < numbers.length; i++) {
    if (numbers[i] === 30) {
        console.log("Found 30 at position " + i);
        found = true;
        break; // Stop searching
    }
}

if (!found) {
    console.log("30 not found in array");
}
```

---

## Practical Examples

### Example 1: Calculate Sum
```javascript
const numbers = [1, 2, 3, 4, 5];
let sum = 0;

for (let i = 0; i < numbers.length; i++) {
    sum += numbers[i];
}

console.log("Sum: " + sum); // Sum: 15
```

### Example 2: Find Maximum
```javascript
const scores = [85, 92, 78, 96, 88];
let maxScore = scores[0];

for (let i = 1; i < scores.length; i++) {
    if (scores[i] > maxScore) {
        maxScore = scores[i];
    }
}

console.log("Highest score: " + maxScore); // Highest score: 96
```

### Example 3: Create New Array
```javascript
const original = [1, 2, 3, 4, 5];
const doubled = [];

for (let i = 0; i < original.length; i++) {
    doubled.push(original[i] * 2);
}

console.log(doubled); // [2, 4, 6, 8, 10]
```

### Example 4: Simple Pattern
```javascript
// Create a triangle pattern
for (let i = 1; i <= 5; i++) {
    let line = "";
    for (let j = 1; j <= i; j++) {
        line += "* ";
    }
    console.log(line);
}
// Output:
// * 
// * * 
// * * * 
// * * * * 
// * * * * *
```

---

## Summary

### Basic For Loop Structure
```javascript
for (let i = 0; i < 5; i++) {
    // Code to repeat 5 times
}
```

### Key Components
- **Initialization** → `let i = 0` (start counter)
- **Condition** → `i < 5` (when to stop)
- **Increment** → `i++` (how to count)

### Common Variations
```javascript
// Count up
for (let i = 0; i < 10; i++) {}

// Count down
for (let i = 10; i > 0; i--) {}

// Skip numbers
for (let i = 0; i < 20; i += 2) {}
```

### Loop Control Statements
- `break` - Stop the entire loop
- `continue` - Skip current iteration

### When to Use For Loops
- When you know how many times to repeat
- When looping through arrays by index
- When you need the index number
- For mathematical sequences

### Quick Tips
1. Start index at 0 for arrays
2. Use `array.length` for array loops
3. Be careful with loop conditions to avoid infinite loops
4. Use meaningful variable names for better readability

---