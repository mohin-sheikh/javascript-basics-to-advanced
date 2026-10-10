# JavaScript Constructors and Classes

## What are Constructors and Classes?

**Constructors** and **Classes** are ways to create multiple similar objects with the same structure.

## Function Constructors

### Simple Constructor
```javascript
// Constructor function (like a blueprint)
function Person(name, age) {
    this.name = name;
    this.age = age;
}

// Create objects using the constructor
const person1 = new Person("John", 25);
const person2 = new Person("Sarah", 30);

console.log(person1.name); // "John"
console.log(person2.age);  // 30
```

### Constructor with Methods
```javascript
function Car(brand, model) {
    this.brand = brand;
    this.model = model;
    
    this.getInfo = function() {
        return `${this.brand} ${this.model}`;
    };
}

const myCar = new Car("Toyota", "Camry");
console.log(myCar.getInfo()); // "Toyota Camry"
```

## ES6 Classes

### Simple Class
```javascript
// Class (modern way, works same as constructor)
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
}

// Create objects using class
const person1 = new Person("John", 25);
const person2 = new Person("Sarah", 30);

console.log(person1.name); // "John"
console.log(person2.age);  // 30
```

### Class with Methods
```javascript
class Car {
    constructor(brand, model) {
        this.brand = brand;
        this.model = model;
    }
    
    getInfo() {
        return `${this.brand} ${this.model}`;
    }
    
    startEngine() {
        return "Engine started!";
    }
}

const myCar = new Car("Honda", "Civic");
console.log(myCar.getInfo());   // "Honda Civic"
console.log(myCar.startEngine()); // "Engine started!"
```

## Inheritance

### Class Inheritance
```javascript
// Parent class
class Animal {
    constructor(name) {
        this.name = name;
    }
    
    speak() {
        return "Some sound";
    }
}

// Child class inherits from Animal
class Dog extends Animal {
    constructor(name, breed) {
        super(name); // Call parent constructor
        this.breed = breed;
    }
    
    // Override parent method
    speak() {
        return "Woof!";
    }
}

const myDog = new Dog("Buddy", "Golden Retriever");
console.log(myDog.name);   // "Buddy"
console.log(myDog.speak()); // "Woof!"
```

## Simple Comparison

### Function Constructor
```javascript
function Product(name, price) {
    this.name = name;
    this.price = price;
}

const product1 = new Product("Laptop", 999);
```

### ES6 Class
```javascript
class Product {
    constructor(name, price) {
        this.name = name;
        this.price = price;
    }
}

const product1 = new Product("Laptop", 999);
```

## When to Use?

### Use Function Constructors when:
- Working with older code
- Simple object creation

### Use Classes when:
- Writing new code
- Need inheritance
- Want cleaner syntax

## Quick Summary

1. **Constructors/Classes** create object blueprints
2. **`new` keyword** creates objects from blueprint
3. **Classes** are modern version of constructors
4. **`extends`** for inheritance between classes
5. Both achieve the same result, classes are preferred for new code

## Simple Example
```javascript
class Student {
    constructor(name, grade) {
        this.name = name;
        this.grade = grade;
    }
    
    getResult() {
        return `${this.name} is in grade ${this.grade}`;
    }
}

const student1 = new Student("Alice", 10);
console.log(student1.getResult()); // "Alice is in grade 10"
```

**Remember**: Classes are just syntactic sugar for function constructors - they work the same way underneath!