# JavaScript Objects
## Table of Contents
- [What are Objects?](#what-are-objects)
- [Creating Objects](#creating-objects)
- [Accessing Properties](#accessing-properties)
- [Object Methods](#object-methods)
- [CRUD Operations](#crud-operations)
- [Summary](#summary)

---

## What are Objects?

**Objects** are collections of key-value pairs used to store related data and functionality.

### Simple Definition
Objects are like containers that hold multiple pieces of information about something.

```javascript
// Example: Object representing a person
let person = {
    name: "John Doe",
    age: 30,
    city: "New York"
};
```

---

## Creating Objects

### 1. Object Literal (Most Common)
```javascript
let person = {
    name: "John",
    age: 25,
    isStudent: true
};
```

### 2. Using new Object()
```javascript
let car = new Object();
car.brand = "Toyota";
car.model = "Camry";
car.year = 2020;
```

### 3. Object with Methods
```javascript
let person = {
    name: "Alice",
    age: 28,
    greet: function() {
        return "Hello, I'm " + this.name;
    }
};
```

---

## Accessing Properties

### Dot Notation
```javascript
let person = { name: "John", age: 30 };

console.log(person.name); // "John"
console.log(person.age);  // 30
```

### Bracket Notation
```javascript
let person = { name: "John", age: 30 };

console.log(person["name"]); // "John"
console.log(person["age"]);  // 30

// Useful for dynamic property names
let property = "name";
console.log(person[property]); // "John"
```

---

## Object Methods

### 1. Object.keys()
**Gets all property names**
```javascript
let person = { name: "John", age: 30, city: "NY" };
let keys = Object.keys(person);
console.log(keys); // ["name", "age", "city"]
```

### 2. Object.values()
**Gets all property values**
```javascript
let person = { name: "John", age: 30, city: "NY" };
let values = Object.values(person);
console.log(values); // ["John", 30, "NY"]
```

### 3. Object.entries()
**Gets all key-value pairs**
```javascript
let person = { name: "John", age: 30 };
let entries = Object.entries(person);
console.log(entries); // [["name", "John"], ["age", 30]]
```

### 4. Object.assign()
**Copies properties between objects**
```javascript
let obj1 = { a: 1, b: 2 };
let obj2 = { c: 3, d: 4 };
let combined = Object.assign({}, obj1, obj2);
console.log(combined); // { a: 1, b: 2, c: 3, d: 4 }
```

---

## CRUD Operations

CRUD stands for **Create, Read, Update, Delete** - the four basic operations for data.

### Create (Add Properties)
```javascript
let person = { name: "John" };

// Add new properties
person.age = 30;
person["city"] = "New York";
person.country = "USA";

console.log(person);
// { name: "John", age: 30, city: "New York", country: "USA" }
```

### Read (Access Properties)
```javascript
let person = { 
    name: "John", 
    age: 30, 
    city: "New York" 
};

// Read properties
console.log(person.name);    // "John"
console.log(person["age"]);  // 30

// Check if property exists
console.log("name" in person); // true
console.log(person.hasOwnProperty("age")); // true
```

### Update (Modify Properties)
```javascript
let person = { 
    name: "John", 
    age: 30, 
    city: "New York" 
};

// Update existing properties
person.age = 31;
person["city"] = "Boston";
person.name = "John Smith";

console.log(person);
// { name: "John Smith", age: 31, city: "Boston" }
```

### Delete (Remove Properties)
```javascript
let person = { 
    name: "John", 
    age: 30, 
    city: "New York" 
};

// Delete properties
delete person.age;
delete person["city"];

console.log(person); // { name: "John" }
```

---

## Practical CRUD Examples

### Example 1: User Profile Management
```javascript
// Create user profile
let user = {
    username: "johndoe",
    email: "john@email.com",
    profile: {
        firstName: "John",
        lastName: "Doe"
    }
};

// READ - Get user information
console.log(user.username); // "johndoe"
console.log(user.profile.firstName); // "John"

// UPDATE - Change user email
user.email = "john.doe@newemail.com";

// CREATE - Add new property
user.isActive = true;
user.lastLogin = "2023-12-01";

// DELETE - Remove property
delete user.profile.lastName;

console.log(user);
```

### Example 2: Shopping Cart
```javascript
let cart = {
    items: [],
    total: 0
};

// CREATE - Add item
cart.items.push({ product: "Book", price: 20 });
cart.total += 20;

// READ - View cart
console.log(cart.items);
console.log("Total: $" + cart.total);

// UPDATE - Modify item
cart.items[0].price = 25;
cart.total += 5; // Update total

// DELETE - Remove item
cart.total -= cart.items[0].price;
cart.items.pop();

console.log(cart);
```

### Example 3: Student Record System
```javascript
let student = {
    id: "S001",
    name: "Alice Johnson",
    grades: {
        math: 85,
        science: 92,
        english: 78
    }
};

// CRUD Operations
console.log("Student:", student.name); // READ

student.grades.history = 88; // CREATE
student.grades.math = 90; // UPDATE

let subjects = Object.keys(student.grades); // READ all subjects
console.log("Subjects:", subjects);

delete student.grades.english; // DELETE

console.log("Updated grades:", student.grades);
```

---

## Object Iteration

### Loop Through Object Properties
```javascript
let person = { 
    name: "John", 
    age: 30, 
    city: "NY" 
};

// Using for...in loop
for (let key in person) {
    console.log(key + ": " + person[key]);
}
// Output:
// name: John
// age: 30
// city: NY

// Using Object.keys() with forEach
Object.keys(person).forEach(key => {
    console.log(`${key}: ${person[key]}`);
});
```

---

## Summary

### Object Creation Methods:
```javascript
// 1. Object Literal (Recommended)
let obj1 = { key: "value" };

// 2. Constructor
let obj2 = new Object();
obj2.key = "value";

// 3. Object.create()
let obj3 = Object.create(null);
obj3.key = "value";
```

### CRUD Operations Cheat Sheet →

| Operation | Syntax | Example |
|-----------|--------|---------|
| **Create** | `obj.key = value` | `person.age = 30` |
| **Read** | `obj.key` or `obj["key"]` | `person.name` |
| **Update** | `obj.key = newValue` | `person.age = 31` |
| **Delete** | `delete obj.key` | `delete person.age` |

### Essential Object Methods →
- `Object.keys(obj)` - Get all keys
- `Object.values(obj)` - Get all values  
- `Object.entries(obj)` - Get key-value pairs
- `Object.assign(target, source)` - Copy properties

### Best Practices →
1. Use **dot notation** when you know the property name
2. Use **bracket notation** for dynamic property names
3. Use `const` for objects that won't be reassigned
4. Use meaningful property names
5. Group related data in nested objects

---