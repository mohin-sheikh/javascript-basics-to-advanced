# JavaScript Math Methods

## Table of Contents
- [What are Math Methods?](#what-are-math-methods)
- [Basic Math Operations](#basic-math-operations)
- [Rounding Methods](#rounding-methods)
- [Power and Roots](#power-and-roots)
- [Trigonometric Functions](#trigonometric-functions)
- [Random Numbers](#random-numbers)
- [Comparison Methods](#comparison-methods)
- [Constants](#constants)
- [Summary](#summary)

---

## What are Math Methods?

**Math Methods** are built-in JavaScript functions that perform mathematical operations and calculations.

### Simple Definition
Math methods are like a calculator built into JavaScript - they help you work with numbers easily.

```javascript
// Simple math example
let result = Math.max(10, 20, 5);
console.log(result); // 20
```

### Why Use Math Methods?
- **Built-in functionality** → No need to write complex calculations
- **Accuracy** → Handle edge cases and precision
- **Performance** → Optimized for speed
- **Consistency** → Same results across different browsers

---

## Basic Math Operations

### Math.abs() - Absolute Value
Returns the positive value of a number.

```javascript
console.log(Math.abs(-5)); // 5
console.log(Math.abs(3.14)); // 3.14
console.log(Math.abs(0)); // 0
```

### Math.sqrt() - Square Root
Returns the square root of a number.

```javascript
console.log(Math.sqrt(25)); // 5
console.log(Math.sqrt(2)); // 1.4142135623730951
console.log(Math.sqrt(-1)); // NaN (Not a Number)
```

### Math.cbrt() - Cube Root
Returns the cube root of a number.

```javascript
console.log(Math.cbrt(27)); // 3
console.log(Math.cbrt(8)); // 2
console.log(Math.cbrt(-8)); // -2
```

---

## Rounding Methods

### Math.round() - Round to Nearest Integer
Rounds to the closest whole number.

```javascript
console.log(Math.round(4.7)); // 5
console.log(Math.round(4.4)); // 4
console.log(Math.round(4.5)); // 5
```

### Math.floor() - Round Down
Always rounds down to the nearest integer.

```javascript
console.log(Math.floor(4.7)); // 4
console.log(Math.floor(4.2)); // 4
console.log(Math.floor(-4.2)); // -5
```

### Math.ceil() - Round Up
Always rounds up to the nearest integer.

```javascript
console.log(Math.ceil(4.2)); // 5
console.log(Math.ceil(4.7)); // 5
console.log(Math.ceil(-4.2)); // -4
```

### Math.trunc() - Remove Decimal Part
Removes the decimal part without rounding.

```javascript
console.log(Math.trunc(4.7)); // 4
console.log(Math.trunc(4.2)); // 4
console.log(Math.trunc(-4.2)); // -4
```

### Math.round() vs Math.floor() vs Math.ceil() vs Math.trunc()

| Method | 4.2 | 4.7 | -4.2 | -4.7 |
|--------|-----|-----|------|------|
| `Math.round()` | 4 | 5 | -4 | -5 |
| `Math.floor()` | 4 | 4 | -5 | -5 |
| `Math.ceil()` | 5 | 5 | -4 | -4 |
| `Math.trunc()` | 4 | 4 | -4 | -4 |

---

## Power and Roots

### Math.pow() - Power
Raises a number to a specified power.

```javascript
console.log(Math.pow(2, 3)); // 8 (2³)
console.log(Math.pow(5, 2)); // 25 (5²)
console.log(Math.pow(16, 0.5)); // 4 (square root)
```

### ES6 Exponentiation Operator
```javascript
console.log(2 ** 3); // 8
console.log(5 ** 2); // 25
```

### Math.exp() - Exponential
Returns e raised to a power.

```javascript
console.log(Math.exp(1)); // 2.718 (e¹)
console.log(Math.exp(2)); // 7.389 (e²)
```

### Math.log() - Natural Logarithm
Returns the natural logarithm (base e).

```javascript
console.log(Math.log(1)); // 0
console.log(Math.log(Math.E)); // 1
```

---

## Trigonometric Functions

### Math.sin() - Sine
Returns the sine of an angle (in radians).

```javascript
console.log(Math.sin(0)); // 0
console.log(Math.sin(Math.PI / 2)); // 1
```

### Math.cos() - Cosine
Returns the cosine of an angle (in radians).

```javascript
console.log(Math.cos(0)); // 1
console.log(Math.cos(Math.PI)); // -1
```

### Math.tan() - Tangent
Returns the tangent of an angle (in radians).

```javascript
console.log(Math.tan(0)); // 0
console.log(Math.tan(Math.PI / 4)); // 1
```

### Degree to Radian Conversion
```javascript
function toRadians(degrees) {
    return degrees * (Math.PI / 180);
}

console.log(Math.sin(toRadians(90))); // 1
console.log(Math.cos(toRadians(0))); // 1
```

---

## Random Numbers

### Math.random() - Random Number
Returns a random number between 0 (inclusive) and 1 (exclusive).

```javascript
console.log(Math.random()); // 0.123456789 (example)
console.log(Math.random()); // 0.987654321 (example)
```

### Random Number in Range
```javascript
// Random between 0 and 9
let random1 = Math.floor(Math.random() * 10);
console.log(random1);

// Random between 1 and 10
let random2 = Math.floor(Math.random() * 10) + 1;
console.log(random2);

// Random between min and max (inclusive)
function randomInRange(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}

console.log(randomInRange(5, 15)); // Random between 5-15
```

---

## Comparison Methods

### Math.max() - Maximum Value
Returns the largest number from the arguments.

```javascript
console.log(Math.max(10, 20, 5)); // 20
console.log(Math.max(-1, -5, -10)); // -1
```

### Math.min() - Minimum Value
Returns the smallest number from the arguments.

```javascript
console.log(Math.min(10, 20, 5)); // 5
console.log(Math.min(-1, -5, -10)); // -10
```

### With Arrays
```javascript
let numbers = [10, 20, 5, 30];

console.log(Math.max(...numbers)); // 30
console.log(Math.min(...numbers)); // 5
```

---

## Constants

### Math.PI - Pi
The ratio of a circle's circumference to its diameter.

```javascript
console.log(Math.PI); // 3.141592653589793

// Calculate circle area
function circleArea(radius) {
    return Math.PI * Math.pow(radius, 2);
}

console.log(circleArea(5)); // 78.53981633974483
```

### Math.E - Euler's Number
The base of natural logarithms.

```javascript
console.log(Math.E); // 2.718281828459045
```

### Math.SQRT2 - Square Root of 2
```javascript
console.log(Math.SQRT2); // 1.4142135623730951
```

---

## Practical Examples

### Example 1: Calculator Functions
```javascript
// Basic calculator operations
const calculator = {
    add: (a, b) => a + b,
    subtract: (a, b) => a - b,
    multiply: (a, b) => a * b,
    divide: (a, b) => a / b,
    power: (a, b) => Math.pow(a, b),
    squareRoot: (a) => Math.sqrt(a),
    absolute: (a) => Math.abs(a)
};

console.log(calculator.power(2, 3)); // 8
console.log(calculator.squareRoot(16)); // 4
console.log(calculator.absolute(-5)); // 5
```

### Example 2: Number Utilities
```javascript
// Utility functions for number manipulation
const numberUtils = {
    // Round to specified decimal places
    roundTo: (number, decimals = 0) => {
        const factor = Math.pow(10, decimals);
        return Math.round(number * factor) / factor;
    },
    
    // Check if number is within range
    inRange: (number, min, max) => {
        return number >= min && number <= max;
    },
    
    // Generate random integer array
    randomArray: (length, min, max) => {
        return Array.from({ length }, () => 
            Math.floor(Math.random() * (max - min + 1)) + min
        );
    }
};

console.log(numberUtils.roundTo(3.14159, 2)); // 3.14
console.log(numberUtils.inRange(5, 1, 10)); // true
console.log(numberUtils.randomArray(5, 1, 100)); // [23, 67, 45, 89, 12] (example)
```

### Example 3: Geometry Calculations
```javascript
// Geometry functions using Math methods
const geometry = {
    // Circle calculations
    circle: {
        area: (radius) => Math.PI * Math.pow(radius, 2),
        circumference: (radius) => 2 * Math.PI * radius,
        diameter: (radius) => 2 * radius
    },
    
    // Distance between two points
    distance: (x1, y1, x2, y2) => {
        return Math.sqrt(Math.pow(x2 - x1, 2) + Math.pow(y2 - y1, 2));
    },
    
    // Convert between degrees and radians
    toRadians: (degrees) => degrees * (Math.PI / 180),
    toDegrees: (radians) => radians * (180 / Math.PI)
};

console.log(geometry.circle.area(5)); // 78.53981633974483
console.log(geometry.distance(0, 0, 3, 4)); // 5
console.log(geometry.toRadians(180)); // 3.141592653589793
```

### Example 4: Game Development Utilities
```javascript
// Useful math functions for games
const gameMath = {
    // Random movement
    randomMovement: (speed) => {
        const angle = Math.random() * Math.PI * 2;
        return {
            x: Math.cos(angle) * speed,
            y: Math.sin(angle) * speed
        };
    },
    
    // Clamp value between min and max
    clamp: (value, min, max) => {
        return Math.min(Math.max(value, min), max);
    },
    
    // Linear interpolation
    lerp: (start, end, factor) => {
        return start + (end - start) * factor;
    },
    
    // Check collision between two circles
    circleCollision: (x1, y1, r1, x2, y2, r2) => {
        const distance = Math.sqrt(Math.pow(x2 - x1, 2) + Math.pow(y2 - y1, 2));
        return distance < r1 + r2;
    }
};

// Usage examples
console.log(gameMath.clamp(15, 0, 10)); // 10
console.log(gameMath.lerp(0, 100, 0.5)); // 50
console.log(gameMath.circleCollision(0, 0, 5, 8, 0, 5)); // false (distance 8, sum of radii 10)
```

---

## Summary

### Math Methods Quick Reference

| Category | Methods | Description |
|----------|---------|-------------|
| **Basic** | `abs()`, `sqrt()`, `cbrt()` | Absolute value, square root, cube root |
| **Rounding** | `round()`, `floor()`, `ceil()`, `trunc()` | Different rounding behaviors |
| **Power** | `pow()`, `exp()`, `log()` | Exponentiation and logarithms |
| **Trigonometry** | `sin()`, `cos()`, `tan()` | Trigonometric functions (radians) |
| **Random** | `random()` | Random numbers 0-1 |
| **Comparison** | `max()`, `min()` | Find largest/smallest values |
| **Constants** | `PI`, `E`, `SQRT2` | Mathematical constants |

### Common Patterns

#### Random Number Generation
```javascript
// Random integer between min and max (inclusive)
function randomInt(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}

// Random float between min and max
function randomFloat(min, max) {
    return Math.random() * (max - min) + min;
}
```

#### Rounding to Decimals
```javascript
function roundToDecimal(number, decimals) {
    const factor = Math.pow(10, decimals);
    return Math.round(number * factor) / factor;
}

console.log(roundToDecimal(3.14159, 2)); // 3.14
```

#### Distance Calculation
```javascript
function distance2D(x1, y1, x2, y2) {
    return Math.sqrt(Math.pow(x2 - x1, 2) + Math.pow(y2 - y1, 2));
}
```
This guide provides a comprehensive overview of JavaScript Math Methods, complete with definitions, examples, and practical applications. You can use this as a reference for implementing mathematical operations in your JavaScript projects.