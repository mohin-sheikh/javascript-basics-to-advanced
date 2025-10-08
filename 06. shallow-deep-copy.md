# JavaScript Shallow Copy vs Deep Copy

## Table of Contents
- [What is Copying?](#what-is-copying)
- [Shallow Copy](#shallow-copy)
- [Deep Copy](#deep-copy)
- [Quick Comparison](#quick-comparison)
- [When to Use Each](#when-to-use-each)

---

## What is Copying?

**Copying** means creating a new variable with the same data as an existing one.

```javascript
// Simple values (numbers, strings) - easy copy
let a = 10;
let b = a; // Real copy
b = 20;
console.log(a); // 10 (unchanged)

// Objects and arrays - tricky copy
let obj1 = { name: "John" };
let obj2 = obj1; // Not a real copy!
obj2.name = "Jane";
console.log(obj1.name); // "Jane" (changed!)
```

---

## Shallow Copy

### Simple Definition
**Shallow Copy** copies only the first level. Nested objects and arrays are still connected.

### How to Make Shallow Copy
```javascript
let original = { 
    name: "John", 
    address: { city: "NY" } 
};

// Method 1: Spread Operator
let copy1 = { ...original };

// Method 2: Object.assign()
let copy2 = Object.assign({}, original);
```

### Shallow Copy Example
```javascript
let original = {
    name: "John",
    address: { city: "NY" }
};

let shallowCopy = { ...original };

// Change first level - SAFE
shallowCopy.name = "Jane";
console.log(original.name); // "John" (unchanged)

// Change nested level - DANGEROUS
shallowCopy.address.city = "LA";
console.log(original.address.city); // "LA" (changed!)
```

---

## Deep Copy

### Simple Definition
**Deep Copy** copies everything completely. No connections between original and copy.

### How to Make Deep Copy
```javascript
let original = { 
    name: "John", 
    address: { city: "NY" } 
};

// Easy method using JSON
let deepCopy = JSON.parse(JSON.stringify(original));
```

### Deep Copy Example
```javascript
let original = {
    name: "John",
    address: { city: "NY" }
};

let deepCopy = JSON.parse(JSON.stringify(original));

// Change anything - SAFE
deepCopy.name = "Jane";
deepCopy.address.city = "LA";

console.log(original.name); // "John" (unchanged)
console.log(original.address.city); // "NY" (unchanged)
```

---

## Quick Comparison

| | Shallow Copy | Deep Copy |
|---|---|---|
| **Copies** | First level only | All levels |
| **Nested Objects** | Connected | Completely separate |
| **Performance** | Fast | Slow |
| **Use When** | No nested objects | Has nested objects |

### Visual Example
```javascript
let data = {
    name: "John",           // Level 1
    address: {              // Level 1
        city: "NY",         // Level 2
        zip: "10001"        // Level 2
    }
};

// Shallow Copy: name is copied, address is shared
// Deep Copy: everything is copied, nothing shared
```

---

## When to Use Each

### Use Shallow Copy When →
- Object has no nested objects/arrays
- You want better performance
- Simple data structure

```javascript
// Good for shallow copy
let user = { name: "John", age: 30 };
let userCopy = { ...user }; // Perfect!
```

### Use Deep Copy When →
- Object has nested objects/arrays
- You need complete separation
- Working with complex data

```javascript
// Needs deep copy
let complexData = {
    user: { 
        name: "John", 
        settings: { theme: "dark" } 
    }
};
let safeCopy = JSON.parse(JSON.stringify(complexData));
```

## Simple Rule
- **Flat objects** → Use shallow copy (`...spread`)
- **Nested objects** → Use deep copy (`JSON method`)

---