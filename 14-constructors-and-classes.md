# JavaScript Constructors and Classes

## Table of Contents
- [What are Constructors?](#what-are-constructors)
- [Function Constructors](#function-constructors)
- [ES6 Classes](#es6-classes)
- [Constructor vs Class](#constructor-vs-class)
- [Inheritance](#inheritance)
- [Static Methods](#static-methods)
- [Summary](#summary)

---

## What are Constructors?

### Definition
**Constructors** are special functions that create and initialize objects.

### Simple Definition
Constructors are like blueprints for creating multiple similar objects.

```javascript
// Without constructor (manual creation)
let car1 = { brand: "Toyota", model: "Camry", year: 2020 };
let car2 = { brand: "Honda", model: "Civic", year: 2021 };
let car3 = { brand: "Ford", model: "Focus", year: 2019 };

// With constructor (automated creation)
function Car(brand, model, year) {
    this.brand = brand;
    this.model = model;
    this.year = year;
}

let car4 = new Car("Toyota", "Camry", 2020);
let car5 = new Car("Honda", "Civic", 2021);
```

---

## Function Constructors

### Basic Constructor
```javascript
// Constructor function (start with capital letter)
function Person(name, age) {
    this.name = name;
    this.age = age;
    
    // Method
    this.greet = function() {
        return `Hello, I'm ${this.name}`;
    };
}

// Create objects using 'new'
const person1 = new Person("John", 25);
const person2 = new Person("Sarah", 30);

console.log(person1.greet()); // "Hello, I'm John"
console.log(person2.greet()); // "Hello, I'm Sarah"
```

### What happens with `new` keyword?
1. Creates a new empty object
2. Sets `this` to point to the new object
3. Executes the constructor function
4. Returns the new object

### Adding Methods to Prototype
```javascript
function Student(name, grade) {
    this.name = name;
    this.grade = grade;
}

// Add method to prototype (better for memory)
Student.prototype.getGrade = function() {
    return `${this.name} is in grade ${this.grade}`;
};

const student1 = new Student("Alice", 10);
console.log(student1.getGrade()); // "Alice is in grade 10"
```

---

## ES6 Classes

### Definition
**Classes** are syntactic sugar over constructor functions - they work the same way but with cleaner syntax.

### Basic Class
```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
    
    // Method (automatically goes to prototype)
    greet() {
        return `Hello, I'm ${this.name}`;
    }
}

// Usage (same as constructor)
const person1 = new Person("John", 25);
const person2 = new Person("Sarah", 30);

console.log(person1.greet()); // "Hello, I'm John"
console.log(person2.greet()); // "Hello, I'm Sarah"
```

### Class with Multiple Methods
```javascript
class Car {
    constructor(brand, model, year) {
        this.brand = brand;
        this.model = model;
        this.year = year;
        this.speed = 0;
    }
    
    accelerate() {
        this.speed += 10;
        return `Speed: ${this.speed} km/h`;
    }
    
    brake() {
        this.speed -= 5;
        return `Speed: ${this.speed} km/h`;
    }
    
    getInfo() {
        return `${this.year} ${this.brand} ${this.model}`;
    }
}

// Create car objects
const myCar = new Car("Toyota", "Camry", 2020);
console.log(myCar.getInfo()); // "2020 Toyota Camry"
console.log(myCar.accelerate()); // "Speed: 10 km/h"
console.log(myCar.accelerate()); // "Speed: 20 km/h"
```

---

## Constructor vs Class

### Same Result, Different Syntax

#### Function Constructor
```javascript
function Product(name, price) {
    this.name = name;
    this.price = price;
}

Product.prototype.getPrice = function() {
    return `$${this.price}`;
};

const product1 = new Product("Laptop", 999);
```

#### ES6 Class
```javascript
class Product {
    constructor(name, price) {
        this.name = name;
        this.price = price;
    }
    
    getPrice() {
        return `$${this.price}`;
    }
}

const product1 = new Product("Laptop", 999);
```

### Key Differences
| Feature | Function Constructor | Class |
|---------|---------------------|-------|
| **Syntax** | Function-based | Class-based |
| **Methods** | Added to prototype | Inside class body |
| **Hoisting** | Yes | No |
| **Readability** | Less intuitive | More intuitive |

---

## Inheritance

### Function Constructor Inheritance
```javascript
// Parent constructor
function Animal(name) {
    this.name = name;
}

Animal.prototype.speak = function() {
    return `${this.name} makes a sound`;
};

// Child constructor
function Dog(name, breed) {
    Animal.call(this, name); // Call parent constructor
    this.breed = breed;
}

// Set up prototype chain
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

// Child method
Dog.prototype.bark = function() {
    return `${this.name} barks!`;
};

const myDog = new Dog("Buddy", "Golden Retriever");
console.log(myDog.speak()); // "Buddy makes a sound"
console.log(myDog.bark());  // "Buddy barks!"
```

### Class Inheritance (Much Simpler!)
```javascript
// Parent class
class Animal {
    constructor(name) {
        this.name = name;
    }
    
    speak() {
        return `${this.name} makes a sound`;
    }
}

// Child class
class Dog extends Animal {
    constructor(name, breed) {
        super(name); // Call parent constructor
        this.breed = breed;
    }
    
    bark() {
        return `${this.name} barks!`;
    }
}

const myDog = new Dog("Buddy", "Golden Retriever");
console.log(myDog.speak()); // "Buddy makes a sound"
console.log(myDog.bark());  // "Buddy barks!"
```

---

## Static Methods

### Definition
**Static methods** belong to the class itself, not to individual objects.

### Function Constructor Static Method
```javascript
function MathHelper() {}

// Static method
MathHelper.add = function(a, b) {
    return a + b;
};

// Usage (call on constructor, not instance)
console.log(MathHelper.add(5, 3)); // 8

// This won't work:
// const helper = new MathHelper();
// helper.add(5, 3); // Error
```

### Class Static Method
```javascript
class MathHelper {
    static add(a, b) {
        return a + b;
    }
    
    static multiply(a, b) {
        return a * b;
    }
}

// Usage (call on class, not instance)
console.log(MathHelper.add(5, 3)); // 8
console.log(MathHelper.multiply(5, 3)); // 15
```

---

## Practical Examples

### Example 1: User Management
```javascript
class User {
    constructor(username, email) {
        this.username = username;
        this.email = email;
        this.isLoggedIn = false;
    }
    
    login() {
        this.isLoggedIn = true;
        return `${this.username} logged in`;
    }
    
    logout() {
        this.isLoggedIn = false;
        return `${this.username} logged out`;
    }
    
    getProfile() {
        return `Username: ${this.username}, Email: ${this.email}`;
    }
}

// Create users
const user1 = new User("john_doe", "john@example.com");
const user2 = new User("sarah_smith", "sarah@example.com");

console.log(user1.login()); // "john_doe logged in"
console.log(user1.getProfile()); // "Username: john_doe, Email: john@example.com"
```

### Example 2: Bank Account
```javascript
class BankAccount {
    constructor(accountHolder, initialBalance = 0) {
        this.accountHolder = accountHolder;
        this.balance = initialBalance;
        this.accountNumber = this.generateAccountNumber();
    }
    
    generateAccountNumber() {
        return 'ACC' + Math.random().toString().slice(2, 11);
    }
    
    deposit(amount) {
        this.balance += amount;
        return `Deposited $${amount}. New balance: $${this.balance}`;
    }
    
    withdraw(amount) {
        if (amount > this.balance) {
            return "Insufficient funds";
        }
        this.balance -= amount;
        return `Withdrew $${amount}. New balance: $${this.balance}`;
    }
    
    getBalance() {
        return `Balance: $${this.balance}`;
    }
}

// Create account
const myAccount = new BankAccount("John Doe", 1000);
console.log(myAccount.deposit(500)); // "Deposited $500. New balance: $1500"
console.log(myAccount.withdraw(200)); // "Withdrew $200. New balance: $1300"
```

### Example 3: Shopping Cart
```javascript
class ShoppingCart {
    constructor() {
        this.items = [];
        this.total = 0;
    }
    
    addItem(product, price) {
        this.items.push({ product, price });
        this.total += price;
        return `Added ${product} for $${price}`;
    }
    
    removeItem(productName) {
        const index = this.items.findIndex(item => item.product === productName);
        if (index !== -1) {
            const removed = this.items.splice(index, 1)[0];
            this.total -= removed.price;
            return `Removed ${removed.product}`;
        }
        return "Item not found";
    }
    
    getTotal() {
        return `Total: $${this.total}`;
    }
    
    checkout() {
        const summary = `Checkout complete! ${this.items.length} items, Total: $${this.total}`;
        this.items = [];
        this.total = 0;
        return summary;
    }
}

// Usage
const cart = new ShoppingCart();
console.log(cart.addItem("Laptop", 999)); // "Added Laptop for $999"
console.log(cart.addItem("Mouse", 25)); // "Added Mouse for $25"
console.log(cart.getTotal()); // "Total: $1024"
console.log(cart.checkout()); // "Checkout complete! 2 items, Total: $1024"
```

---

## Summary

### Key Points

#### Function Constructors
- Use `function` keyword with capital name
- Use `new` keyword to create objects
- Add methods to `prototype` for better memory usage
- Use for simple object creation patterns

#### ES6 Classes
- Use `class` keyword
- Cleaner, more readable syntax
- Methods automatically go to prototype
- Built-in inheritance with `extends`
- Recommended for modern JavaScript

### When to Use Which?

| Use Case | Recommendation |
|----------|----------------|
| **Simple objects** | Either works fine |
| **Complex inheritance** | Use classes |
| **Modern code** | Use classes |
| **Legacy code** | Function constructors |
| **Learning OOP** | Start with classes |

### Quick Reference

#### Function Constructor
```javascript
function Person(name) {
    this.name = name;
}
Person.prototype.greet = function() {
    return `Hello, I'm ${this.name}`;
};
const john = new Person("John");
```

#### ES6 Class
```javascript
class Person {
    constructor(name) {
        this.name = name;
    }
    
    greet() {
        return `Hello, I'm ${this.name}`;
    }
}
const john = new Person("John");
```

### Best Practices
1. **Use classes** for new code
2. **Use descriptive names** (PascalCase for constructors/classes)
3. **Keep constructors simple** - just initialization
4. **Use `extends`** for inheritance instead of manual prototype setup
5. **Use static methods** for utility functions related to the class

---