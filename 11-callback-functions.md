# JavaScript Callback Functions

## Table of Contents
- [What are Callback Functions?](#what-are-callback-functions)
- [Why Use Callbacks?](#why-use-callbacks)
- [Common Use Cases](#common-use-cases)
- [Callback Hell and Solutions](#callback-hell-and-solutions)
- [Summary](#summary)

---

## What are Callback Functions?

### Definition
A **callback function** is a function passed as an argument to another function, to be executed later.

### Simple Definition
Callbacks are like giving instructions to someone: "When you finish task A, then do task B."

### Basic Example
```javascript
// Callback function
function greet(name) {
    console.log(`Hello, ${name}!`);
}

// Main function that accepts a callback
function processUser(callback) {
    const userName = "John";
    callback(userName); // Execute the callback
}

// Pass greet function as callback
processUser(greet); // "Hello, John!"
```

---

## Why Use Callbacks?

### 1. Code Reusability
```javascript
// Same function, different callbacks
function calculate(a, b, operation) {
    return operation(a, b);
}

// Different callback functions
function add(x, y) {
    return x + y;
}

function multiply(x, y) {
    return x * y;
}

// Reuse the same calculate function
console.log(calculate(5, 3, add));      // 8
console.log(calculate(5, 3, multiply)); // 15
```

### 2. Customizable Behavior
```javascript
function processArray(numbers, processor) {
    const results = [];
    for (let number of numbers) {
        results.push(processor(number));
    }
    return results;
}

// Different processors
function double(n) { return n * 2; }
function square(n) { return n * n; }

const numbers = [1, 2, 3, 4, 5];

console.log(processArray(numbers, double));  // [2, 4, 6, 8, 10]
console.log(processArray(numbers, square));  // [1, 4, 9, 16, 25]
```

---
## Common Use Cases

### Use Case 1 → Data Processing Pipeline
```javascript
function processUserData(userId, callback) {
    // Step 1: Get user data
    const user = getUser(userId);
    
    // Step 2: Process user data
    const processed = processData(user);
    
    // Step 3: Execute callback with result
    callback(processed);
}

function getUser(id) {
    return { id: id, name: "John Doe", age: 30 };
}

function processData(user) {
    return {
        ...user,
        isAdult: user.age >= 18,
        birthYear: new Date().getFullYear() - user.age
    };
}

// Usage
processUserData(123, function(userInfo) {
    console.log("Processed user:", userInfo);
});
```
---

## Callback Hell and Solutions

### The Problem → Callback Hell
```javascript
// Nested callbacks become hard to read
getUser(123, function(user) {
    getPermissions(user, function(permissions) {
        getSettings(permissions, function(settings) {
            updateUI(settings, function() {
                console.log("All done!");
            });
        });
    });
});
```

### Solution 1 → Named Functions
```javascript
function handleUser(user) {
    getPermissions(user, handlePermissions);
}

function handlePermissions(permissions) {
    getSettings(permissions, handleSettings);
}

function handleSettings(settings) {
    updateUI(settings, handleCompletion);
}

function handleCompletion() {
    console.log("All done!");
}

// Much cleaner!
getUser(123, handleUser);
```

### Solution 2 → Modular Approach
```javascript
const userManager = {
    getUserData: function(userId, callback) {
        this.getUser(userId, (user) => {
            this.getPermissions(user, (permissions) => {
                this.getSettings(permissions, (settings) => {
                    callback(settings);
                });
            });
        });
    },
    
    getUser: function(id, callback) { /* ... */ },
    getPermissions: function(user, callback) { /* ... */ },
    getSettings: function(permissions, callback) { /* ... */ }
};

// Clean usage
userManager.getUserData(123, function(settings) {
    updateUI(settings);
});
```

---

## Summary

### Key Points

#### What are Callbacks?
- Functions passed as arguments to other functions
- Executed later, either immediately or after some operation

#### Types of Callbacks
- **Synchronous**: Executed immediately
- **Asynchronous**: Executed after operation completes

#### Common Patterns
```javascript
// Basic callback
function mainFunction(callback) {
    // Do work
    callback(result);
}

// Error-first callback
function asyncOperation(callback) {
    if (error) {
        callback(error, null);
    } else {
        callback(null, result);
    }
}

// Multiple callbacks
function operation(successCallback, errorCallback) {
    if (success) {
        successCallback(data);
    } else {
        errorCallback(error);
    }
}
```

### When to Use Callbacks

| Situation | Use Callbacks |
|-----------|---------------|
| Array operations | ✅ forEach, map, filter |
| Custom algorithms | ✅ Sorting, searching |
| Event handling | ✅ Click handlers, custom events |
| Async operations | ✅ File I/O, API calls |
| Code customization | ✅ Plugin systems, hooks |

### Best Practices

1. **Use named functions** for complex callbacks
2. **Follow error-first pattern** for async operations
3. **Keep callbacks small** and focused
4. **Avoid deep nesting** (callback hell)
5. **Document callback parameters**
6. **Handle errors properly**

### Quick Reference
```javascript
// Basic callback usage
function processor(data, callback) {
    const result = data * 2;
    callback(result);
}

processor(5, function(output) {
    console.log(output); // 10
});

// Error-first pattern
function asyncTask(callback) {
    const success = true;
    if (success) {
        callback(null, "Success!");
    } else {
        callback("Error occurred", null);
    }
}
```

---