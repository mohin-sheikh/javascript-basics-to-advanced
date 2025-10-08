# JavaScript String Methods

## Table of Contents
- [String Basics](#string-basics)
- [String Property](#string-property)
- [String Search Methods](#string-search-methods)
- [String Extraction Methods](#string-extraction-methods)
- [String Modification Methods](#string-modification-methods)
- [Case Conversion Methods](#case-conversion-methods)
- [String Validation Methods](#string-validation-methods)
- [Summary](#summary)

---

## String Basics

### Creating Strings
```javascript
// Different ways to create strings
let single = 'Hello World';
let double = "Hello World";
let template = `Hello World`;

// String constructor
let fromConstructor = new String("Hello");

console.log(single); // "Hello World"
```

### String Characteristics
- **Immutable** → Strings cannot be changed once created
- **Indexed** → Each character has a position (index) starting from 0
- **Length** → Every string has a length property

---

## String Property

### `length` - String Length
**Definition** → Returns the number of characters in a string.

```javascript
let text = "Hello World";
console.log(text.length); // 11

let empty = "";
console.log(empty.length); // 0

let space = "   ";
console.log(space.length); // 3
```

---

## String Search Methods

### `indexOf()` - Find First Occurrence
**Definition** → Returns the position of the first occurrence of specified value.

```javascript
let text = "Hello world, welcome to the world.";

console.log(text.indexOf("world")); // 6
console.log(text.indexOf("World")); // -1 (not found)
console.log(text.indexOf("o")); // 4
console.log(text.indexOf("o", 5)); // 7 (search from position 5)
```

### `lastIndexOf()` - Find Last Occurrence
**Definition** → Returns the position of the last occurrence of specified value.

```javascript
let text = "Hello world, welcome to the world.";

console.log(text.lastIndexOf("world")); // 23
console.log(text.lastIndexOf("o")); // 24
console.log(text.lastIndexOf("o", 20)); // 17
```

### `search()` - Search with Regex
**Definition** → Searches for a match using regular expression.

```javascript
let text = "Hello world!";

console.log(text.search("world")); // 6
console.log(text.search(/world/)); // 6
console.log(text.search(/[A-Z]/)); // 0 (first uppercase)
```

### `includes()` - Check for Substring
**Definition** → Returns true if string contains specified value.

```javascript
let sentence = "The quick brown fox jumps over the lazy dog";

console.log(sentence.includes("fox")); // true
console.log(sentence.includes("cat")); // false
console.log(sentence.includes("brown", 10)); // false (search from position 10)
```

### `startsWith()` - Check Beginning
**Definition** → Returns true if string starts with specified value.

```javascript
let filename = "document.pdf";

console.log(filename.startsWith("doc")); // true
console.log(filename.startsWith("pdf")); // false
console.log(filename.startsWith("ument", 3)); // true
```

### `endsWith()` - Check Ending
**Definition** → Returns true if string ends with specified value.

```javascript
let filename = "document.pdf";

console.log(filename.endsWith(".pdf")); // true
console.log(filename.endsWith("doc")); // false
console.log(filename.endsWith("ment", 10)); // true
```

---

## String Extraction Methods

### `slice()` - Extract Substring
**Definition** → Extracts part of string and returns new string.

```javascript
let text = "Hello World";

console.log(text.slice(0, 5)); // "Hello"
console.log(text.slice(6)); // "World"
console.log(text.slice(-5)); // "World" (from end)
console.log(text.slice(3, 7)); // "lo W"
```

### `substring()` - Extract Between Indexes
**Definition** → Extracts characters between two specified indices.

```javascript
let text = "Hello World";

console.log(text.substring(0, 5)); // "Hello"
console.log(text.substring(6)); // "World"
console.log(text.substring(3, 7)); // "lo W"

// Difference from slice - swaps if start > end
console.log(text.substring(7, 3)); // "lo W" (swaps to 3,7)
```

### `substr()` - Extract from Position
**Definition** → Extracts specified number of characters from start position.

```javascript
let text = "Hello World";

console.log(text.substr(0, 5)); // "Hello"
console.log(text.substr(6)); // "World"
console.log(text.substr(3, 7)); // "lo World"
console.log(text.substr(-5, 3)); // "Wor" (from end)
```

### `charAt()` - Get Character at Index
**Definition** → Returns the character at specified index.

```javascript
let text = "Hello";

console.log(text.charAt(0)); // "H"
console.log(text.charAt(4)); // "o"
console.log(text.charAt(10)); // "" (empty string)
```

### `charCodeAt()` - Get Character Code
**Definition** → Returns the Unicode of character at specified index.

```javascript
let text = "Hello";

console.log(text.charCodeAt(0)); // 72 (H)
console.log(text.charCodeAt(1)); // 101 (e)
console.log(text.charCodeAt(10)); // NaN
```

---

## String Modification Methods

### `replace()` - Replace Substring
**Definition** → Replaces specified value with another value in string.

```javascript
let text = "Hello World";

console.log(text.replace("World", "JavaScript")); // "Hello JavaScript"
console.log(text.replace(/hello/i, "Hi")); // "Hi World" (case-insensitive)

// Only replaces first occurrence
let multiple = "cat dog cat";
console.log(multiple.replace("cat", "bird")); // "bird dog cat"
```

### `replaceAll()` - Replace All Occurrences
**Definition** → Replaces all occurrences of specified value with new value.

```javascript
let text = "Hello World World";

console.log(text.replaceAll("World", "JavaScript")); // "Hello JavaScript JavaScript"

let multiple = "cat dog cat";
console.log(multiple.replaceAll("cat", "bird")); // "bird dog bird"
```

### `toUpperCase()` - Convert to Uppercase
**Definition** → Converts string to uppercase letters.

```javascript
let text = "Hello World";

console.log(text.toUpperCase()); // "HELLO WORLD"
console.log("javascript".toUpperCase()); // "JAVASCRIPT"
```

### `toLowerCase()` - Convert to Lowercase
**Definition** → Converts string to lowercase letters.

```javascript
let text = "Hello World";

console.log(text.toLowerCase()); // "hello world"
console.log("JAVASCRIPT".toLowerCase()); // "javascript"
```

### `concat()` - Join Strings
**Definition** → Joins two or more strings and returns new string.

```javascript
let firstName = "John";
let lastName = "Doe";

console.log(firstName.concat(" ", lastName)); // "John Doe"
console.log("Hello".concat(" ", "World", "!")); // "Hello World!"
```

### `trim()` - Remove Whitespace
**Definition** → Removes whitespace from both ends of string.

```javascript
let text = "   Hello World!   ";

console.log(text.trim()); // "Hello World!"
console.log("  no space  ".trim()); // "no space"
```

### `trimStart()` - Remove Start Whitespace
**Definition** → Removes whitespace from beginning of string.

```javascript
let text = "   Hello World!";

console.log(text.trimStart()); // "Hello World!"
console.log("  left space  ".trimStart()); // "left space  "
```

### `trimEnd()` - Remove End Whitespace
**Definition** → Removes whitespace from end of string.

```javascript
let text = "Hello World!   ";

console.log(text.trimEnd()); // "Hello World!"
console.log("  right space  ".trimEnd()); // "  right space"
```

### `padStart()` - Pad Start of String
**Definition** → Pads string with another string until it reaches given length.

```javascript
let number = "5";

console.log(number.padStart(4, "0")); // "0005"
console.log("123".padStart(6, "0")); // "000123"
console.log("hello".padStart(8, "*")); // "***hello"
```

### `padEnd()` - Pad End of String
**Definition** → Pads string with another string until it reaches given length.

```javascript
let number = "5";

console.log(number.padEnd(4, "0")); // "5000"
console.log("123".padEnd(6, "0")); // "123000"
console.log("hello".padEnd(8, "*")); // "hello***"
```

---

## Case Conversion Methods

### `toLocaleUpperCase()` - Locale Uppercase
**Definition** → Converts to uppercase according to host locale.

```javascript
let text = "hello world";

console.log(text.toLocaleUpperCase()); // "HELLO WORLD"
console.log("café".toLocaleUpperCase('tr-TR')); // "CAFÉ"
```

### `toLocaleLowerCase()` - Locale Lowercase
**Definition** → Converts to lowercase according to host locale.

```javascript
let text = "HELLO WORLD";

console.log(text.toLocaleLowerCase()); // "hello world"
console.log("İ".toLocaleLowerCase('tr-TR')); // "i"
```

---

## String Validation Methods

### `match()` - Match Regular Expression
**Definition** → Retrieves matches when matching string against regex.

```javascript
let text = "The rain in SPAIN stays mainly in the plain";

console.log(text.match(/ain/g)); // ["ain", "ain", "ain"]
console.log(text.match(/AIN/gi)); // ["ain", "AIN", "ain"]
```

### `matchAll()` - Match All Occurrences
**Definition** → Returns iterator of all results matching regex.

```javascript
let text = "test1 test2 test3";
let regex = /test(\d)/g;

for (let match of text.matchAll(regex)) {
    console.log(match[0] + " at " + match.index); 
}
// "test1 at 0"
// "test2 at 6" 
// "test3 at 12"
```

### `split()` - Split String into Array
**Definition** → Splits string into array of substrings using separator.

```javascript
let text = "apple,banana,orange";

console.log(text.split(",")); // ["apple", "banana", "orange"]
console.log("hello".split("")); // ["h", "e", "l", "l", "o"]
console.log("a,b,c".split(",", 2)); // ["a", "b"] (limit 2)
```

### `repeat()` - Repeat String
**Definition** → Returns new string with specified number of copies.

```javascript
let text = "Hello";

console.log(text.repeat(3)); // "HelloHelloHello"
console.log("abc".repeat(2)); // "abcabc"
console.log("*".repeat(5)); // "*****"
```

### `toString()` - Convert to String
**Definition** → Returns string representation of string object.

```javascript
let text = new String("Hello");

console.log(text.toString()); // "Hello"
console.log(typeof text.toString()); // "string"
```

### `valueOf()` - Return Primitive Value
**Definition** → Returns primitive value of string object.

```javascript
let text = new String("Hello");

console.log(text.valueOf()); // "Hello"
console.log(typeof text.valueOf()); // "string"
```

---

## Summary

### Most Commonly Used String Methods →

| Method | Purpose | Example |
|--------|---------|---------|
| `length` | Get string length | `"hi".length` → 2 |
| `indexOf()` | Find first occurrence | `"hello".indexOf("l")` → 2 |
| `slice()` | Extract substring | `"hello".slice(1,4)` → "ell" |
| `replace()` | Replace content | `"hi".replace("hi","hello")` → "hello" |
| `toUpperCase()` | Convert to uppercase | `"hi".toUpperCase()` → "HI" |
| `toLowerCase()` | Convert to lowercase | `"HI".toLowerCase()` → "hi" |
| `trim()` | Remove whitespace | `" hi ".trim()` → "hi" |
| `split()` | Split into array | `"a,b".split(",")` → ["a","b"] |
| `includes()` | Check if contains | `"hello".includes("ell")` → true |

### Quick Reference Categories →

- **Search** - `indexOf()`, `lastIndexOf()`, `search()`, `includes()`, `startsWith()`, `endsWith()`
- **Extract** - `slice()`, `substring()`, `substr()`, `charAt()`, `charCodeAt()`
- **Modify** - `replace()`, `replaceAll()`, `toUpperCase()`, `toLowerCase()`, `concat()`, `trim()`
- **Padding** - `padStart()`, `padEnd()`
- **Split/Join** - `split()`, `repeat()`

### Best Practices →
1. Use `includes()` instead of `indexOf() !== -1` for readability
2. Prefer `slice()` over `substring()` for negative indexing
3. Use template literals instead of `concat()` for string joining
4. Always use `trim()` on user input
5. Use `startsWith()`/`endsWith()` for prefix/suffix checks

---