# JavaScript Template Literals and Operators

## Table of Contents
- [Template Literals](#template-literals)
- [Arithmetic Operators](#arithmetic-operators)
- [Assignment Operators](#assignment-operators)
- [Comparison Operators](#comparison-operators)
- [Logical Operators](#logical-operators)
- [Operator Precedence](#operator-precedence)
- [Summary](#summary)

---

## Template Literals

Template literals (introduced in ES6) provide an easy way to work with strings and embed expressions.

### Basic Syntax
```javascript
// Traditional strings
let traditional1 = 'Hello World';
let traditional2 = "Hello World";

// Template literals use backticks ``
let template = `Hello World`;

console.log(template); // "Hello World"
```

### String Interpolation
```javascript
// Variables in strings without template literals
let name = "John";
let age = 25;
let message1 = "My name is " + name + " and I am " + age + " years old.";

// With template literals - much cleaner!
let message2 = `My name is ${name} and I am ${age} years old.`;

console.log(message2); // "My name is John and I am 25 years old."
```

### Multi-line Strings
```javascript
// Traditional multi-line (ugly)
let oldMultiLine = "Line 1\n" +
                   "Line 2\n" +
                   "Line 3";

// With template literals (clean)
let newMultiLine = `Line 1
Line 2
Line 3`;

console.log(newMultiLine);
// Output:
// Line 1
// Line 2
// Line 3
```

### Expression Evaluation
```javascript
let a = 5;
let b = 10;

// Calculations inside template literals
let calculation = `The sum of ${a} and ${b} is ${a + b}`;
console.log(calculation); // "The sum of 5 and 10 is 15"

// Function calls
function getPrice() {
    return 19.99;
}
let priceMessage = `The price is $${getPrice()}`;
console.log(priceMessage); // "The price is $19.99"

// Conditional expressions
let isMember = true;
let discountMessage = `Your discount: ${isMember ? "20%" : "0%"}`;
console.log(discountMessage); // "Your discount: 20%"
```

---

## Arithmetic Operators

Used for mathematical operations on numbers.

### Basic Arithmetic Operators
```javascript
let x = 10;
let y = 3;

// Addition
let sum = x + y;        // 13
console.log(`Addition: ${x} + ${y} = ${sum}`);

// Subtraction
let difference = x - y; // 7
console.log(`Subtraction: ${x} - ${y} = ${difference}`);

// Multiplication
let product = x * y;    // 30
console.log(`Multiplication: ${x} * ${y} = ${product}`);

// Division
let quotient = x / y;   // 3.333...
console.log(`Division: ${x} / ${y} = ${quotient}`);

// Modulus (Remainder)
let remainder = x % y;  // 1
console.log(`Modulus: ${x} % ${y} = ${remainder}`);

// Exponentiation (ES6)
let power = x ** y;     // 1000
console.log(`Exponent: ${x} ** ${y} = ${power}`);
```

### Increment and Decrement
```javascript
let count = 5;

// Post-increment (returns value, then increments)
console.log(count++); // 5
console.log(count);   // 6

// Pre-increment (increments, then returns value)
let anotherCount = 5;
console.log(++anotherCount); // 6

// Post-decrement
let num = 8;
console.log(num--); // 8
console.log(num);   // 7

// Pre-decrement
let anotherNum = 8;
console.log(--anotherNum); // 7
```

### Unary Operators
```javascript
let positive = 10;
let negative = -positive; // -10

let notNumber = "hello";
let converted = +notNumber; // NaN (Not a Number)
```

---

## Assignment Operators

Used to assign values to variables.

### Basic Assignment
```javascript
let a = 10;  // Simple assignment
console.log(`a = ${a}`); // 10
```

### Compound Assignment Operators
```javascript
let number = 10;

// Addition assignment
number += 5;  // number = number + 5
console.log(`After += 5: ${number}`); // 15

// Subtraction assignment
number -= 3;  // number = number - 3
console.log(`After -= 3: ${number}`); // 12

// Multiplication assignment
number *= 2;  // number = number * 2
console.log(`After *= 2: ${number}`); // 24

// Division assignment
number /= 4;  // number = number / 4
console.log(`After /= 4: ${number}`); // 6

// Modulus assignment
number %= 4;  // number = number % 4
console.log(`After %= 4: ${number}`); // 2

// Exponentiation assignment
number **= 3; // number = number ** 3
console.log(`After **= 3: ${number}`); // 8
```

---

## Comparison Operators

Used to compare values and return boolean results.

### Equality Operators
```javascript
let num = 5;
let str = "5";

// Loose equality (checks value only)
console.log(num == str);   // true
console.log(num != str);   // false

// Strict equality (checks value AND type)
console.log(num === str);  // false
console.log(num !== str);  // true

// Real-world example
let userInput = "25";
let actualAge = 25;

// This might cause bugs!
if (userInput == actualAge) {
    console.log("Loose equality: They match!");
}

// This is safer
if (userInput === actualAge) {
    console.log("This won't run because types are different");
} else {
    console.log("Strict equality: They don't match exactly");
}
```

### Relational Operators
```javascript
let x = 10;
let y = 5;

// Greater than
console.log(x > y);   // true
console.log(y > x);   // false

// Less than
console.log(x < y);   // false
console.log(y < x);   // true

// Greater than or equal to
console.log(x >= 10); // true
console.log(x >= 15); // false

// Less than or equal to
console.log(y <= 5);  // true
console.log(y <= 3);  // false

// String comparison (lexicographical)
console.log("apple" < "banana"); // true
console.log("zebra" > "apple");  // true
```

---

## Logical Operators

Used to combine or invert boolean values.

### AND Operator (&&)
```javascript
let isLoggedIn = true;
let hasPermission = true;
let isAdmin = false;

// AND - both must be true
console.log(isLoggedIn && hasPermission); // true
console.log(isLoggedIn && isAdmin);       // false

// Practical example
let age = 20;
let hasID = true;

if (age >= 18 && hasID) {
    console.log("Access granted"); // This will run
}
```

### OR Operator (||)
```javascript
let hasCreditCard = false;
let hasPayPal = true;
let hasCash = false;

// OR - at least one must be true
console.log(hasCreditCard || hasPayPal); // true
console.log(hasCreditCard || hasCash);   // false

// Practical example
let isWeekend = true;
let isHoliday = false;

if (isWeekend || isHoliday) {
    console.log("Store is closed"); // This will run
}
```

### NOT Operator (!)
```javascript
let isActive = true;
let isBanned = false;

// NOT - inverts the boolean value
console.log(!isActive); // false
console.log(!isBanned); // true

// Double NOT (converts to boolean)
let userCount = 0;
console.log(!!userCount); // false (0 is falsy)

let userName = "John";
console.log(!!userName);  // true (non-empty string is truthy)
```

### Short-circuit Evaluation
```javascript
// AND short-circuit - if first is false, return first
let result1 = false && someFunction(); // someFunction never called
console.log(result1); // false

// OR short-circuit - if first is true, return first
let result2 = true || someFunction(); // someFunction never called
console.log(result2); // true

// Practical use with template literals
let user = null;
let displayName = user || "Guest";
console.log(`Welcome, ${displayName}`); // "Welcome, Guest"

let settings = { theme: "dark" };
let theme = settings.theme || "light";
console.log(`Theme: ${theme}`); // "Theme: dark"
```

---

## Operator Precedence

The order in which operations are performed.

### Common Precedence Order
```javascript
// Higher precedence operators execute first
let result1 = 2 + 3 * 4;     // 14 (not 20)
let result2 = (2 + 3) * 4;   // 20 (parentheses change order)

console.log(`Without parentheses: 2 + 3 * 4 = ${result1}`);
console.log(`With parentheses: (2 + 3) * 4 = ${result2}`);

// Logical operator precedence: NOT > AND > OR
let a = true;
let b = false;
let c = true;

let logicalResult = !a && b || c; // Equivalent to: ((!a) && b) || c
console.log(`Logical result: ${logicalResult}`); // true
```

### Using Parentheses for Clarity
```javascript
// Complex expression without parentheses (confusing)
let confusing = 5 + 3 * 2 > 10 && 4 < 7 || true;

// Same expression with parentheses (clear)
let clear = ((5 + (3 * 2)) > 10) && (4 < 7) || true;

console.log(`Result: ${clear}`); // true

// Always use parentheses for complex expressions
let calculation = (10 + 5) * (3 - 1);
console.log(`Calculation: ${calculation}`); // 30
```

---

## Summary

### Template Literals Quick Reference -
- **Syntax** - Use backticks ` `` `
- **Interpolation** - `${expression}`
- **Multi-line** - Automatic line breaks
- **Expressions** - Any valid JavaScript inside `${}`

### Operators Quick Reference -

#### Arithmetic Operators
| Operator | Description | Example |
|----------|-------------|---------|
| `+` | Addition | `5 + 3` = 8 |
| `-` | Subtraction | `5 - 3` = 2 |
| `*` | Multiplication | `5 * 3` = 15 |
| `/` | Division | `15 / 3` = 5 |
| `%` | Modulus | `15 % 4` = 3 |
| `**` | Exponentiation | `2 ** 3` = 8 |
| `++` | Increment | `x++` |
| `--` | Decrement | `x--` |

#### Assignment Operators
| Operator | Example | Equivalent |
|----------|---------|------------|
| `=` | `x = 5` | `x = 5` |
| `+=` | `x += 3` | `x = x + 3` |
| `-=` | `x -= 2` | `x = x - 2` |
| `*=` | `x *= 4` | `x = x * 4` |
| `/=` | `x /= 2` | `x = x / 2` |
| `%=` | `x %= 3` | `x = x % 3` |

#### Comparison Operators
| Operator | Description | Example |
|----------|-------------|---------|
| `==` | Loose equality | `5 == "5"` → true |
| `===` | Strict equality | `5 === "5"` → false |
| `!=` | Loose inequality | `5 != "5"` → false |
| `!==` | Strict inequality | `5 !== "5"` → true |
| `>` | Greater than | `10 > 5` → true |
| `<` | Less than | `10 < 5` → false |
| `>=` | Greater than or equal | `10 >= 10` → true |
| `<=` | Less than or equal | `10 <= 5` → false |

#### Logical Operators
| Operator | Description | Example |
|----------|-------------|---------|
| `&&` | AND | `true && false` → false |
| `\|\|` | OR | `true \|\| false` → true |
| `!` | NOT | `!true` → false |

### Best Practices -
1. **Use template literals** for string concatenation
2. **Use strict equality** (`===` and `!==`) to avoid type coercion bugs
3. **Use parentheses** to make complex expressions clear
4. **Understand operator precedence** or use parentheses
5. **Use descriptive variable names** in template literals

---