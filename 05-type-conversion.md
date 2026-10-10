# Type Conversion

## Table of Contents
- [What is Type Conversion](#what-is-type-conversion)
- [Explicit and Implicit Conversion](#explicit-and-implicit-conversion)
- [Converting to a Number with Number()](#converting-to-a-number-with-number)
- [The Unary + Shortcut](#the-unary--shortcut)
- [parseInt() and parseFloat()](#parseint-and-parsefloat)
- [Number() vs parseInt()](#number-vs-parseint)
- [Checking the Result: Number.isNaN()](#checking-the-result-numberisnan)
- [More Checks: isInteger and isFinite](#more-checks-isinteger-and-isfinite)
- [Converting to a String](#converting-to-a-string)
- [Converting to a Boolean: Truthy and Falsy](#converting-to-a-boolean-truthy-and-falsy)
- [The "false" String Trap](#the-false-string-trap)
- [Implicit Conversion](#implicit-conversion)
- [NaN Spreads](#nan-spreads)
- [Converting User Input Safely](#converting-user-input-safely)
- [Mini Example: Reading a Search Request](#mini-example-reading-a-search-request)
- [Beginner Mistakes](#beginner-mistakes)
- [Practice Exercises](#practice-exercises)
- [Interview Questions](#interview-questions)

---

## What is Type Conversion

**Type conversion** means changing a value from one type to another: for example, the text `"2"` into the number `2`.

Why does a backend developer need this every day? Because everything that comes from a URL or a form reaches the server as **text** (Session 03)

why.js

```javascript
// The URL /products?page=2 gives the server the TEXT "2"
const pageFromUrl = "2";

console.log(pageFromUrl + 1);           // joins text
console.log(Number(pageFromUrl) + 1);   // converted first: real math
```

Output

```text
21
3
```

![The URL sends the text "2" to the server; "2" + 1 gives "21", Number("2") + 1 gives 3](images/05-type-conversion/why-conversion.gif)

Without conversion, "the next page" becomes page **21**.

---

## Explicit and Implicit Conversion

There are two ways a value changes type

![Explicit: you call Number("5") and get 5. Implicit: "5" * 2 is converted by JavaScript and gives 10](images/05-type-conversion/explicit-vs-implicit.gif)

| Kind      | Who converts     | Example            | Result |
| --------- | ---------------- | ------------------ | ------ |
| Explicit  | You, on purpose  | `Number("5")`      | `5`    |
| Implicit  | JavaScript, by itself | `"5" * 2`     | `10`   |

Implicit conversion is also called **type coercion**. It is the cause of many surprises (like `"5" + 1` being `"51"`, Session 04). Explicit conversion is clear and safe, so **professional code converts explicitly**.

The three conversion functions

| Function      | Converts to |
| ------------- | ----------- |
| `Number(x)`   | number      |
| `String(x)`   | string      |
| `Boolean(x)`  | boolean     |

---

## Converting to a Number with Number()

to-number.js

```javascript
console.log(Number("42"));
console.log(Number("3.5"));
console.log(Number("  42  "));   // spaces at the ends are ignored
console.log(Number(""));         // empty text becomes 0!
console.log(Number("42px"));
console.log(Number("abc"));
console.log(Number("1,000"));    // a comma is not allowed
console.log(Number(true));
console.log(Number(false));
console.log(Number(null));
console.log(Number(undefined));
```

Output

```text
42
3.5
42
0
NaN
NaN
NaN
1
0
0
NaN
```

![Values go into the Number() machine: "42" gives 42, "" gives 0, "42px" gives NaN, null gives 0](images/05-type-conversion/number-machine.gif)

| Value          | `Number(value)` | Notes                                 |
| -------------- | --------------- | ------------------------------------- |
| `"42"`         | `42`            |                                       |
| `"  42  "`     | `42`            | Spaces at the start and end are ignored |
| `""`           | `0`             | **Careful:** an empty form field becomes 0 |
| `"42px"`       | `NaN`           | The whole text must be a number       |
| `"1,000"`      | `NaN`           | No commas                             |
| `true` / `false` | `1` / `0`     |                                       |
| `null`         | `0`             | **Careful**                           |
| `undefined`    | `NaN`           |                                       |

When the text is not a number, you get `NaN` (Session 03), not an error. You must check for it yourself (see [below](#checking-the-result-numberisnan)).

---

## The Unary + Shortcut

A `+` in front of a value also converts it to a number

unary-plus.js

```javascript
const priceText = "499";
console.log(+priceText);          // + in front converts to a number
console.log(typeof +priceText);
```

Output

```text
499
number
```

`+priceText` works exactly like `Number(priceText)`. You will see it in other people's code, but `Number()` is easier to read. This course uses `Number()`.

---

## parseInt() and parseFloat()

`parseInt()` and `parseFloat()` read a number **from the start** of the text and stop at the first character that does not fit

parse.js

```javascript
console.log(parseInt("42px", 10));     // reads 42, stops at "p"
console.log(parseInt("3.99", 10));     // whole numbers only
console.log(parseFloat("3.99kg"));     // keeps the decimals
console.log(parseInt("abc", 10));      // no number at the start
console.log(parseInt("", 10));
console.log(parseInt("  7  ", 10));
```

Output

```text
42
3
3.99
NaN
NaN
7
```

![parseInt reads 4 and 2 and stops at p; parseFloat reads 3.99 and stops at k; Number("42px") gives NaN](images/05-type-conversion/parseint-reading.gif)

| Function       | Reads                                   | `"3.99kg"` gives |
| -------------- | --------------------------------------- | ---------------- |
| `parseInt()`   | Whole numbers only                      | `3`              |
| `parseFloat()` | Numbers with decimals                   | `3.99`           |

**Always pass `10` as the second value of `parseInt`.** It means "read this as a normal base-10 number". Code checkers warn when it is missing, and the Node.js course writes it every time.

---

## Number() vs parseInt()

number-vs-parse.js

```javascript
console.log(Number("42"), parseInt("42", 10));
console.log(Number("42px"), parseInt("42px", 10));
console.log(Number("3.99"), parseInt("3.99", 10));
console.log(Number(""), parseInt("", 10));
console.log(Number("1e3"), parseInt("1e3", 10));
```

Output

```text
42 42
NaN 42
3.99 3
0 NaN
1000 1
```

![A table comparing Number() and parseInt() for "42", "42px", "3.99", "" and "1e3"](images/05-type-conversion/number-vs-parseint.gif)

| Text       | `Number()` | `parseInt(text, 10)` | Why                                    |
| ---------- | ---------- | -------------------- | -------------------------------------- |
| `"42"`     | `42`       | `42`                 | Both work                              |
| `"42px"`   | `NaN`      | `42`                 | `parseInt` ignores the rest            |
| `"3.99"`   | `3.99`     | `3`                  | `parseInt` drops the decimals          |
| `""`       | `0`        | `NaN`                | `Number("")` is 0!                     |
| `"1e3"`    | `1000`     | `1`                  | `1e3` means 1 × 10³ = 1000             |

Which one to use?

| Use            | When                                                          |
| -------------- | ------------------------------------------------------------- |
| `Number()`     | You want to be **strict**: the whole text must be a number    |
| `parseInt(x, 10)` | You need a whole number, like a page number, and want to take the number at the start |
| `parseFloat()` | You need decimals from text like `"3.99kg"`                   |

---

## Checking the Result: Number.isNaN()

After converting, check whether it worked

isnan.js

```javascript
const limitText = "abc";
const limit = Number(limitText);

console.log(limit);
console.log(Number.isNaN(limit));        // true: the conversion failed
console.log(Number.isNaN(Number("20"))); // false: a real number

console.log(isNaN("abc"));               // true: old global isNaN converts first
console.log(Number.isNaN("abc"));        // false: "abc" is a string, not NaN
```

Output

```text
NaN
true
false
true
false
```

![Number.isNaN(limit) is true after a failed conversion; the old isNaN("abc") converts first and is confusing](images/05-type-conversion/isnan-check.gif)

Remember from Session 04: `limit === NaN` is always `false`, so you **must** use `Number.isNaN()`.

| Check                 | `"abc"`  | `NaN`   | Use it?                                  |
| --------------------- | -------- | ------- | ---------------------------------------- |
| `Number.isNaN(x)`     | `false`  | `true`  | Yes: exact, no conversion                |
| `isNaN(x)` (old)      | `true`   | `true`  | Avoid: converts first, confusing         |

The pattern: **convert first, then check** with `Number.isNaN()`.

---

## More Checks: isInteger and isFinite

checks.js

```javascript
console.log(Number.isInteger(5));          // whole number?
console.log(Number.isInteger(5.5));
console.log(Number.isFinite(Number("Infinity")));  // a real, finite number?
console.log(Number.isFinite(Number("42")));
console.log(Number("Infinity"));           // a user can type this!
```

Output

```text
true
false
false
true
Infinity
```

| Check                  | True for                                   |
| ---------------------- | ------------------------------------------ |
| `Number.isInteger(x)`  | Whole numbers: `5`, `-3`, `0`              |
| `Number.isFinite(x)`   | Real numbers: not `NaN`, not `Infinity`    |

`Number.isFinite()` is the safest check for user input: it rejects `NaN` **and** `Infinity`. A user really can type `Infinity` into a form, and `Number("Infinity")` happily gives `Infinity`.

---

## Converting to a String

to-string.js

```javascript
console.log(String(42));
console.log(String(3.5));
console.log(String(true));
console.log(String(null));
console.log(String(undefined));

const count = 42;
console.log(count.toString());
console.log(typeof String(42));
```

Output

```text
42
3.5
true
null
undefined
42
string
```

![Values go into the String() machine and come out as text: 42 becomes "42", null becomes "null"](images/05-type-conversion/string-machine.gif)

`String(x)` and `x.toString()` both convert to text, but `toString()` crashes on `null` and `undefined`

tostring-null.js

```javascript
const nickname = null;
console.log(String(nickname));      // works: "null"
console.log(nickname.toString());   // crashes
```

Output

```text
null
D:\js-practice\tostring-null.js:3
console.log(nickname.toString());   // crashes
                     ^

TypeError: Cannot read properties of null (reading 'toString')
```

**Use `String(x)`**: it works for every value. (You will see `Cannot read properties of null` a lot on servers: it means you used something that was `null`.)

---

## Converting to a Boolean: Truthy and Falsy

`Boolean(x)` converts any value to `true` or `false`. The rule is simple: there are exactly **8 falsy values**

to-boolean.js

```javascript
// The 8 falsy values
console.log(Boolean(false));
console.log(Boolean(0));
console.log(Boolean(-0));
console.log(Boolean(0n));
console.log(Boolean(""));
console.log(Boolean(null));
console.log(Boolean(undefined));
console.log(Boolean(NaN));
```

Output

```text
false
false
false
false
false
false
false
false
```

**Everything else is truthy**, even values that look empty or false

truthy.js

```javascript
// Everything else is truthy, even these
console.log(Boolean("0"));
console.log(Boolean("false"));
console.log(Boolean(" "));      // a space is not empty
console.log(Boolean(-1));
console.log(Boolean([]));       // an empty array
console.log(Boolean({}));       // an empty object
```

Output

```text
true
true
true
true
true
true
```

![Values are sorted into two boxes: 8 falsy values and everything else truthy, including "0", "false", [] and {}](images/05-type-conversion/truthy-falsy.gif)

| Falsy (only these 8)                                       | Truthy (examples)                          |
| ---------------------------------------------------------- | ------------------------------------------ |
| `false`, `0`, `-0`, `0n`, `""`, `null`, `undefined`, `NaN` | `"0"`, `"false"`, `" "`, `-1`, `[]`, `{}`, `"hello"`, `42` |

Where does this matter? Everywhere JavaScript needs a yes/no answer: `||`, `&&`, `!` (Session 04) and `if` (Session 06).

`!!` is a short way to write `Boolean()`

double-not.js

```javascript
const userName = "Sara";
const emptyName = "";

console.log(!!userName);     // !! is a short way to write Boolean()
console.log(!!emptyName);
```

Output

```text
true
false
```

The first `!` flips to a boolean, the second `!` flips it back.

---

## The "false" String Trap

false-string.js

```javascript
const sendEmails = "false";   // text from a form, a URL or a settings file

console.log(Boolean(sendEmails));     // true! Any non-empty text is truthy
console.log(sendEmails === "true");   // false: the right way
```

Output

```text
true
false
```

![Boolean("false") is true, so emails are sent anyway; comparing with === "true" gives the right answer](images/05-type-conversion/false-string-trap.gif)

`"false"` is non-empty text, so it is truthy. This bug happens in real servers: a setting like `SEND_EMAILS=false` is read as text, and the emails are sent anyway. You will meet this again with settings files in the Node.js course (Session 16).

**The fix:** compare the text: `value === "true"`.

---

## Implicit Conversion

Some operators convert values by themselves

implicit.js

```javascript
console.log("5" * "2");     // * converts to numbers
console.log("10" / "2");
console.log("5" - "2");
console.log("5" + "2");     // + joins text instead!
console.log(true + 1);      // true becomes 1
console.log(null + 1);      // null becomes 0
console.log(undefined + 1); // undefined becomes NaN
console.log("5" + null);    // + with text: null becomes "null"
```

Output

```text
10
5
3
52
2
1
NaN
5null
```

![* / and - convert text to numbers; + joins the text instead](images/05-type-conversion/implicit-math.gif)

| Operator            | What happens                                    |
| ------------------- | ----------------------------------------------- |
| `-`, `*`, `/`, `%`  | Both sides become numbers                       |
| `+`                 | If one side is text, both become text (joined)  |
| `==`                | Converts before comparing (Session 04)          |
| `\|\|`, `&&`, `!`, `if` | Use truthy/falsy                            |

Knowing these rules helps you read errors. But in your own code, **convert explicitly**: `Number(a) * Number(b)` says exactly what you mean.

---

## NaN Spreads

`NaN` does not stop your program. It quietly spreads into every calculation that uses it

nan-spreads.js

```javascript
const priceText = "abc";        // bad input
const price = Number(priceText);
const total = price * 3;
const withTax = total + 18;

console.log(price, total, withTax);   // NaN spreads through every step
```

Output

```text
NaN NaN NaN
```

![A bad input becomes NaN, and NaN flows into the total and the tax](images/05-type-conversion/nan-spreads.gif)

On a server, this could save an order with a total of `NaN` in the database. That is why you check input **right after converting it**, before using it.

---

## Converting User Input Safely

The safe pattern for numbers from a URL or a form

1. **Convert** with `Number()` (or `parseInt(x, 10)` for whole numbers)
2. **Check** with `Number.isFinite()` (and `Number.isInteger()` if needed)
3. **Use** the number, or reject the input

![Four inputs go through Number() and Number.isFinite(): "2" and "12.5" are used, "abc" and "Infinity" are rejected](images/05-type-conversion/safe-convert.gif)

| Input         | `Number(text)` | `Number.isFinite()` | Result   |
| ------------- | -------------- | ------------------- | -------- |
| `"2"`         | `2`            | `true`              | Use it   |
| `"abc"`       | `NaN`          | `false`             | Reject   |
| `"Infinity"`  | `Infinity`     | `false`             | Reject   |
| `"12.5"`      | `12.5`         | `true`              | Use it   |
| `""`          | `0`            | `true`              | Careful: maybe the user typed nothing |

"Reject" usually means sending an error back to the user. To do that, you need `if` (Session 06). For now, you can calculate the `true`/`false` answer, or use `||` / `??` to fall back to a default value.

---

## Mini Example: Reading a Search Request

A shop's server receives `/products?page=2&limit=abc&minPrice=&inStock=false`. All four values arrive as text

search-request.js

```javascript
// Values from the URL: /products?page=2&limit=abc&minPrice=&inStock=false
const pageText = "2";
const limitText = "abc";
const minPriceText = "";
const inStockText = "false";

const page = Number(pageText);
const limit = Number(limitText) || 10;     // NaN is falsy: use 10
const minPrice = parseFloat(minPriceText); // "" gives NaN, not 0
const inStock = inStockText === "true";

console.log("page:", page, typeof page);
console.log("limit:", limit);
console.log("minPrice:", minPrice, "valid:", Number.isFinite(minPrice));
console.log("inStock:", inStock);
console.log("page is valid:", Number.isInteger(page) && page >= 1);
```

Run

```bash
node search-request.js
```

Output

```text
page: 2 number
limit: 10
minPrice: NaN valid: false
inStock: false
page is valid: true
```

| Value              | Conversion                     | Why                                           |
| ------------------ | ------------------------------ | --------------------------------------------- |
| `page`             | `Number()`                     | `"2"` becomes `2`                             |
| `limit`            | `Number() \|\| 10`             | `"abc"` gives `NaN`, which is falsy, so the default `10` is used |
| `minPrice`         | `parseFloat()`                 | An empty field gives `NaN` instead of a misleading `0` |
| `inStock`          | `=== "true"`                   | Avoids the `"false"` trap                     |
| `page is valid`    | `isInteger` + `>= 1`           | Page 2.5 or page -1 would be invalid          |

This is exactly what the Node.js course does with pages and limits (Sessions 13 and 20).

---

## Beginner Mistakes

### Mistake 1: Doing math with text from a URL or form

**Incorrect**

```javascript
const pageFromUrl = "2";
console.log(pageFromUrl + 1);           // joins text
```

```text
21
```

**Correct:** `Number(pageFromUrl) + 1` gives `3`.

### Mistake 2: Thinking Number("") is NaN

**Incorrect:** expecting an empty field to fail the check. `Number("")` is `0`, and `Number.isFinite(0)` is `true`.

**Correct:** if empty input is not allowed, check for it, or use `parseFloat()`, which gives `NaN` for `""`.

### Mistake 3: Checking NaN with ===

**Incorrect:** `limit === NaN` is always `false`.

**Correct:** `Number.isNaN(limit)`, or `Number.isFinite(limit)` to also reject `Infinity`.

### Mistake 4: Using the old isNaN()

**Incorrect:** `isNaN("abc")` is `true` because it converts first, which hides what really happened.

**Correct:** convert with `Number()`, then check with `Number.isNaN()`.

### Mistake 5: parseInt without 10

**Incorrect:** `parseInt(pageText)`

**Correct:** `parseInt(pageText, 10)`. Always say "base 10".

### Mistake 6: Using parseInt for prices

**Incorrect:** `parseInt("3.99", 10)` gives `3`: the decimals are lost.

**Correct:** `Number("3.99")` or `parseFloat("3.99")` give `3.99`.

### Mistake 7: Boolean("false")

**Incorrect**

```javascript
const sendEmails = "false";   // text from a form, a URL or a settings file
console.log(Boolean(sendEmails));     // true! Any non-empty text is truthy
```

```text
true
```

**Correct:** `sendEmails === "true"`.

### Mistake 8: Calling toString() on null

**Incorrect:** `nickname.toString()` crashes with `TypeError: Cannot read properties of null`.

**Correct:** `String(nickname)` works for every value.

### Mistake 9: Thinking "0" or [] are falsy

**Incorrect:** expecting `"0"`, `" "` or `[]` to count as empty. They are truthy.

**Correct:** only the 8 falsy values are falsy: `false`, `0`, `-0`, `0n`, `""`, `null`, `undefined`, `NaN`.

### Mistake 10: Not checking input after converting

**Incorrect:** converting and using the number directly. One bad value gives `NaN` everywhere (see [NaN Spreads](#nan-spreads)).

**Correct:** convert, then check with `Number.isFinite()`, then use it.

---

## Practice Exercises

### Exercise 1

Convert these with `Number()` and print the results: `"100"`, `"  25 "`, `"12.5"`, `"12,5"`, `""`, `"ten"`, `true`, `null`. Mark the ones that surprised you.

### Exercise 2

Do the same with `parseInt(x, 10)` and `parseFloat(x)`. Make a table in comments: which function gives which result?

### Exercise 3

Create `const ageText = "abc";`. Convert it, then print `Number.isNaN(age)` and `Number.isFinite(age)`. Do the same for `"25"` and `"Infinity"`.

### Exercise 4

Print `Boolean()` for: `0`, `"0"`, `""`, `" "`, `"false"`, `null`, `[]`, `{}`, `-5`, `NaN`. Guess first, then check.

### Exercise 5

A settings value `const darkMode = "true";` is read from a file. Create a real boolean `isDarkMode` from it. Then change the text to `"false"` and check that your boolean changes too.

### Exercise 6

Predict, then check: `"8" * "2"`, `"8" + "2"`, `"8" - "2"`, `true + true`, `null + 5`, `undefined + 5`.

### Exercise 7

A form sends `quantityText = "3"` and `priceText = "249.50"`. Convert both, calculate the total, and print whether both values are valid with `Number.isFinite()`.

### Exercise 8

Extend the [mini example](#mini-example-reading-a-search-request): add `sortText = ""` and `maxPriceText = "5000"`. Use `??` or `||` to give `sort` a default of `"newest"`, and convert `maxPrice` safely.

---

## Interview Questions

### What is type conversion?

Changing a value from one type to another, like the string `"42"` to the number `42`.

### What is the difference between explicit and implicit conversion?

Explicit conversion is done by you with `Number()`, `String()` or `Boolean()`. Implicit conversion (coercion) is done by JavaScript automatically, for example `"5" * 2`.

### What is the difference between Number() and parseInt()?

`Number()` needs the whole string to be a number (`"42px"` gives `NaN`). `parseInt()` reads digits from the start and stops at the first other character (`"42px"` gives `42`), and it only returns whole numbers.

### What does Number("") return?

`0`. This surprises many developers, because an empty input becomes a valid number.

### Why should you pass 10 to parseInt?

It sets the base (radix) to 10, so the text is always read as a normal decimal number. Code checkers require it.

### What is the difference between isNaN() and Number.isNaN()?

The global `isNaN()` converts the value first, so `isNaN("abc")` is `true`. `Number.isNaN()` does not convert: it is `true` only for the actual `NaN` value.

### What are the falsy values in JavaScript?

`false`, `0`, `-0`, `0n`, `""`, `null`, `undefined` and `NaN`. Everything else is truthy.

### Is "0" truthy or falsy? What about []?

Both are truthy. `"0"` is a non-empty string and `[]` is an object.

### What does Boolean("false") return?

`true`, because `"false"` is a non-empty string. Compare with `=== "true"` instead.

### What is the difference between String(x) and x.toString()?

Both convert to a string, but `toString()` throws an error for `null` and `undefined`. `String()` works for every value.

### What does !! do?

It converts a value to a boolean, like `Boolean()`. `!!"Sara"` is `true`, `!!""` is `false`.

### What is "5" - "2" and "5" + "2"?

`3` and `"52"`. `-` converts both sides to numbers; `+` joins strings.

### How do you safely convert user input to a number?

Convert with `Number()` (or `parseInt(x, 10)`), check the result with `Number.isFinite()`, and only then use it.
