# JavaScript Arrays Complete Guide

## Table of Contents
- [What are Arrays?](#what-are-arrays)
- [Creating Arrays](#creating-arrays)
- [Basic Array Operations](#basic-array-operations)
- [Methods that CHANGE Original Array](#methods-that-change-original-array)
- [Methods that DON'T Change Original Array](#methods-that-dont-change-original-array)
- [Search and Find Methods](#search-and-find-methods)
- [Iteration Methods](#iteration-methods)
- [Summary](#summary)

---

## What are Arrays?

**Arrays** are ordered collections of items stored in a single variable.

### Simple Definition
Arrays are like lists that can hold multiple values in a specific order.

```javascript
// Array of numbers
let numbers = [1, 2, 3, 4, 5];

// Array of strings
let fruits = ["apple", "banana", "orange"];

// Mixed array
let mixed = [1, "hello", true, null];
```

### Array Characteristics
- **Ordered** → Items have specific positions (indexes)
- **Indexed** → First item is at index 0, second at index 1, etc.
- **Dynamic** → Can grow or shrink in size
- **Can hold any data type** → Numbers, strings, objects, even other arrays

---

## Creating Arrays

### 1. Array Literal (Most Common)
```javascript
let fruits = ["apple", "banana", "orange"];
let empty = [];
```

### 2. Using Array Constructor
```javascript
let numbers = new Array(1, 2, 3);
let emptyArray = new Array();
```

### 3. Array with Specific Length
```javascript
let fixedLength = new Array(5); // Creates array with 5 empty slots
```

---

## Basic Array Operations

### Accessing Elements
```javascript
let fruits = ["apple", "banana", "orange"];

console.log(fruits[0]); // "apple" (first element)
console.log(fruits[1]); // "banana" (second element)
console.log(fruits[2]); // "orange" (third element)
console.log(fruits[3]); // undefined (doesn't exist)
```

### Array Length
```javascript
let fruits = ["apple", "banana", "orange"];
console.log(fruits.length); // 3
```

### Modifying Elements
```javascript
let fruits = ["apple", "banana", "orange"];

fruits[1] = "grape"; // Change second element
console.log(fruits); // ["apple", "grape", "orange"]
```

---

## Methods that CHANGE Original Array

### 1. push() - Add to End
**Adds one or more elements to the end of array**
```javascript
let fruits = ["apple", "banana"];
fruits.push("orange");
console.log(fruits); // ["apple", "banana", "orange"]

// Add multiple items
fruits.push("grape", "mango");
console.log(fruits); // ["apple", "banana", "orange", "grape", "mango"]
```

### 2. pop() - Remove from End
**Removes and returns the last element**
```javascript
let fruits = ["apple", "banana", "orange"];
let lastFruit = fruits.pop();
console.log(lastFruit); // "orange"
console.log(fruits); // ["apple", "banana"]
```

### 3. unshift() - Add to Start
**Adds one or more elements to the beginning**
```javascript
let fruits = ["banana", "orange"];
fruits.unshift("apple");
console.log(fruits); // ["apple", "banana", "orange"]
```

### 4. shift() - Remove from Start
**Removes and returns the first element**
```javascript
let fruits = ["apple", "banana", "orange"];
let firstFruit = fruits.shift();
console.log(firstFruit); // "apple"
console.log(fruits); // ["banana", "orange"]
```

### 5. splice() - Add/Remove Elements
**Adds/removes elements at specific position**
```javascript
let fruits = ["apple", "banana", "orange"];

// Remove 1 element at index 1
fruits.splice(1, 1);
console.log(fruits); // ["apple", "orange"]

// Remove and add elements
fruits.splice(1, 1, "grape", "mango");
console.log(fruits); // ["apple", "grape", "mango"]
```

### 6. reverse() - Reverse Order
**Reverses the order of elements**
```javascript
let numbers = [1, 2, 3, 4, 5];
numbers.reverse();
console.log(numbers); // [5, 4, 3, 2, 1]
```

### 7. sort() - Sort Elements
**Sorts the elements**
```javascript
let fruits = ["banana", "apple", "orange"];
fruits.sort();
console.log(fruits); // ["apple", "banana", "orange"]

let numbers = [3, 1, 4, 1, 5];
numbers.sort();
console.log(numbers); // [1, 1, 3, 4, 5]
```

---

## Methods that DON'T Change Original Array

### 1. concat() - Combine Arrays
**Combines two or more arrays**
```javascript
let arr1 = [1, 2, 3];
let arr2 = [4, 5, 6];
let combined = arr1.concat(arr2);
console.log(combined); // [1, 2, 3, 4, 5, 6]
console.log(arr1); // [1, 2, 3] (unchanged)
```

### 2. slice() - Extract Portion
**Returns a portion of the array**
```javascript
let fruits = ["apple", "banana", "orange", "grape"];

let firstTwo = fruits.slice(0, 2);
console.log(firstTwo); // ["apple", "banana"]

let lastTwo = fruits.slice(2);
console.log(lastTwo); // ["orange", "grape"]

console.log(fruits); // Original unchanged
```

### 3. join() - Create String
**Joins all elements into a string**
```javascript
let fruits = ["apple", "banana", "orange"];
let result = fruits.join(", ");
console.log(result); // "apple, banana, orange"
console.log(fruits); // Original unchanged
```

### 4. toString() - Convert to String
**Converts array to string**
```javascript
let numbers = [1, 2, 3];
let string = numbers.toString();
console.log(string); // "1,2,3"
console.log(numbers); // [1, 2, 3] (unchanged)
```

---

## Search and Find Methods

### 1. indexOf() - Find Position
**Returns first index of specified element**
```javascript
let fruits = ["apple", "banana", "orange", "banana"];
console.log(fruits.indexOf("banana")); // 1
console.log(fruits.indexOf("grape")); // -1 (not found)
```

### 2. lastIndexOf() - Find Last Position
**Returns last index of specified element**
```javascript
let fruits = ["apple", "banana", "orange", "banana"];
console.log(fruits.lastIndexOf("banana")); // 3
```

### 3. includes() - Check Existence
**Checks if array contains specified element**
```javascript
let fruits = ["apple", "banana", "orange"];
console.log(fruits.includes("banana")); // true
console.log(fruits.includes("grape")); // false
```

### 4. find() - Find First Match
**Returns first element that satisfies condition**
```javascript
let numbers = [5, 12, 8, 130, 44];
let found = numbers.find(num => num > 10);
console.log(found); // 12
```

### 5. findIndex() - Find Index of First Match
**Returns index of first element that satisfies condition**
```javascript
let numbers = [5, 12, 8, 130, 44];
let index = numbers.findIndex(num => num > 10);
console.log(index); // 1
```

---

## Iteration Methods

### 1. forEach() - Execute Function
**Executes function for each element**
```javascript
let numbers = [1, 2, 3];
numbers.forEach(num => {
    console.log(num * 2);
});
// Output: 2, 4, 6
```

### 2. map() - Create New Array
**Creates new array with results of function**
```javascript
let numbers = [1, 2, 3];
let doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6]
console.log(numbers); // [1, 2, 3] (unchanged)
```

### 3. filter() - Filter Elements
**Creates new array with elements that pass test**
```javascript
let numbers = [1, 2, 3, 4, 5, 6];
let even = numbers.filter(num => num % 2 === 0);
console.log(even); // [2, 4, 6]
console.log(numbers); // [1, 2, 3, 4, 5, 6] (unchanged)
```

### 4. reduce() - Reduce to Single Value
**Reduces array to single value**
```javascript
let numbers = [1, 2, 3, 4, 5];
let sum = numbers.reduce((total, num) => total + num, 0);
console.log(sum); // 15
```

### 5. some() - Check if Any Pass
**Checks if at least one element passes test**
```javascript
let numbers = [1, 2, 3, 4, 5];
let hasEven = numbers.some(num => num % 2 === 0);
console.log(hasEven); // true
```

### 6. every() - Check if All Pass
**Checks if all elements pass test**
```javascript
let numbers = [2, 4, 6, 8];
let allEven = numbers.every(num => num % 2 === 0);
console.log(allEven); // true
```

---

## Practical Examples

### Example 1 → Shopping Cart
```javascript
let cart = [];

// ADD items (push)
cart.push("apple");
cart.push("banana");
cart.push("orange");
console.log("Cart:", cart); // ["apple", "banana", "orange"]

// REMOVE last item (pop)
let removed = cart.pop();
console.log("Removed:", removed); // "orange"
console.log("Cart:", cart); // ["apple", "banana"]

// CHECK if item exists (includes)
console.log("Has apple?", cart.includes("apple")); // true

// GET total items (length)
console.log("Total items:", cart.length); // 2
```

### Example 2 → Student Grades
```javascript
let grades = [85, 92, 78, 90, 88];

// Calculate average (reduce)
let average = grades.reduce((sum, grade) => sum + grade, 0) / grades.length;
console.log("Average:", average); // 86.6

// Find highest grade (Math.max with spread)
let highest = Math.max(...grades);
console.log("Highest:", highest); // 92

// Filter passing grades (filter)
let passing = grades.filter(grade => grade >= 80);
console.log("Passing grades:", passing); // [85, 92, 90, 88]
```

### Example 3 → Todo List
```javascript
let todos = ["Buy groceries", "Clean room", "Study JavaScript"];

// ADD new task (unshift - add to beginning)
todos.unshift("Wake up early");
console.log("Todos:", todos);

// REMOVE completed task (splice)
todos.splice(2, 1); // Remove task at index 2
console.log("After completion:", todos);

// SEARCH task (find)
let studyTask = todos.find(todo => todo.includes("Study"));
console.log("Study task:", studyTask);

// MODIFY task (map)
let numberedTodos = todos.map((todo, index) => `${index + 1}. ${todo}`);
console.log("Numbered todos:", numberedTodos);
```

---

## Summary

### Quick Reference: Methods that CHANGE Original
| Method | Purpose | Returns |
|--------|---------|---------|
| `push()` | Add to end | New length |
| `pop()` | Remove from end | Removed element |
| `unshift()` | Add to start | New length |
| `shift()` | Remove from start | Removed element |
| `splice()` | Add/remove elements | Removed elements |
| `reverse()` | Reverse order | Reversed array |
| `sort()` | Sort elements | Sorted array |

### Quick Reference: Methods that DON'T CHANGE Original
| Method | Purpose | Returns |
|--------|---------|---------|
| `concat()` | Combine arrays | New array |
| `slice()` | Extract portion | New array |
| `join()` | Join to string | String |
| `toString()` | Convert to string | String |
| `map()` | Transform elements | New array |
| `filter()` | Filter elements | New array |
| `find()` | Find element | Element or undefined |
| `includes()` | Check existence | Boolean |

### Best Practices →
1. Use `const` for arrays you won't reassign
2. Use methods that don't change original when you need to keep original data
3. Use descriptive variable names for arrays
4. Use array methods instead of traditional loops when possible
5. Chain methods for complex operations

### Common Patterns →
```javascript
// Chain methods
let result = array
    .filter(item => item > 10)
    .map(item => item * 2)
    .reduce((sum, item) => sum + item, 0);

// Check array before operations
if (array.length > 0) {
    // Do something with array
}

// Copy array to avoid mutations
let copy = [...array]; // or array.slice()
```

---