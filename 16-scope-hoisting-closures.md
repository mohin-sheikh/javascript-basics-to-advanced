# JavaScript Closures

## Table of Contents
- [What are Closures?](#what-are-closures)
- [Simple Examples](#simple-examples)
- [How Closures Work](#how-closures-work)
- [Summary](#summary)

---

## What are Closures?

### Definition
A **closure** is a function that remembers variables from its outer scope even after the outer function has finished running.

### Simple Definition
Closures let functions "remember" things from where they were created.

### Basic Concept
```javascript
function outer() {
    let message = "Hello"; // Outer variable
    
    function inner() {
        console.log(message); // Inner function remembers 'message'
    }
    
    return inner;
}

const myFunction = outer();
myFunction(); // "Hello" - still remembers the message!
```

---

## Simple Examples

### Example 1 → Basic Counter
```javascript
function createCounter() {
    let count = 0; // This variable gets "remembered"
    
    return function() {
        count = count + 1;
        return count;
    };
}

const counter = createCounter();
console.log(counter()); // 1
console.log(counter()); // 2
console.log(counter()); // 3
```

### Example 2 → Greeting Maker
```javascript
function createGreeter(greeting) {
    return function(name) {
        return `${greeting}, ${name}!`;
    };
}

const sayHello = createGreeter("Hello");
const sayHi = createGreeter("Hi");

console.log(sayHello("John")); // "Hello, John!"
console.log(sayHi("Sarah"));   // "Hi, Sarah!"
```

### Example 3 → Private Counter
```javascript
function createPrivateCounter() {
    let privateCount = 0;
    
    return {
        increment: function() {
            privateCount++;
            return privateCount;
        },
        getCount: function() {
            return privateCount;
        }
    };
}

const counter = createPrivateCounter();
console.log(counter.increment()); // 1
console.log(counter.increment()); // 2
console.log(counter.getCount());  // 2
// privateCount is not accessible from outside
```

### Example 4 → Multiplier Factory
```javascript
function createMultiplier(multiplyBy) {
    return function(number) {
        return number * multiplyBy;
    };
}

const double = createMultiplier(2);
const triple = createMultiplier(3);

console.log(double(5)); // 10
console.log(triple(5)); // 15
```

### Example 5 → Unique ID Generator
```javascript
function createIdGenerator() {
    let id = 0;
    
    return function() {
        id++;
        return id;
    };
}

const generateId = createIdGenerator();
console.log(generateId()); // 1
console.log(generateId()); // 2
console.log(generateId()); // 3
```

---

## How Closures Work

### The "Remembering" Magic
```javascript
function outer(x) {
    let y = 10; // Gets remembered
    
    function inner(z) {
        return x + y + z; // Can access x, y, and z
    }
    
    return inner;
}

const myFunc = outer(5); // x=5, y=10 get remembered
console.log(myFunc(3)); // 5 + 10 + 3 = 18
```

### Multiple Closures
```javascript
function createClosures() {
    let value = 0;
    
    const increment = function() {
        value++;
        return value;
    };
    
    const decrement = function() {
        value--;
        return value;
    };
    
    return { increment, decrement };
}

const { increment, decrement } = createClosures();
console.log(increment()); // 1
console.log(increment()); // 2
console.log(decrement()); // 1
// Both functions share the same 'value' variable
```

---

## Summary

### What are Closures?
- Functions that remember their creation environment
- Can access variables from outer scopes
- Keep variables alive after outer function finishes

### Key Points
1. **Memory**: Closures remember variables
2. **Privacy**: Can create private variables
3. **Persistence**: Variables stay alive between function calls
4. **Flexibility**: Can create specialized functions

### Simple Rule
If a function accesses variables from outside its own scope, it's a closure.

### Quick Examples Recap
```javascript
// Counter closure
const counter = createCounter();
counter(); // 1
counter(); // 2

// Greeter closure  
const greet = createGreeter("Hello");
greet("John"); // "Hello, John!"

// Multiplier closure
const double = createMultiplier(2);
double(5); // 10
```

### Why Use Closures?
- Create functions with "memory"
- Keep variables private
- Build specialized utility functions
- Maintain state between function calls

---