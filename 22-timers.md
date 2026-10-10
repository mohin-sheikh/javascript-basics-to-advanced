# JavaScript Timing Events setTimeout and setInterval

## Table of Contents
- [Introduction to Timing Events](#introduction-to-timing-events)
- [setTimeout](#settimeout)
- [setInterval](#setinterval)
- [Clearing Timers](#clearing-timers)
- [Practical Examples](#practical-examples)
- [Common Use Cases](#common-use-cases)
- [Best Practices](#best-practices)
- [Summary](#summary)

---

## Introduction to Timing Events

**Timing events** allow you to execute code after a specified time period or at regular intervals.

### Simple Definition
Timing events are like setting alarms or timers for your code to run in the future.

```javascript
// Example: Show message after 2 seconds
setTimeout(() => {
    console.log("Hello after 2 seconds!");
}, 2000);
```

---

## setTimeout

### Definition
**setTimeout** executes a function once after a specified delay.

### Syntax
```javascript
setTimeout(function, delay, param1, param2, ...)
```

### Parameters
- **function** → The function to execute
- **delay** → Time to wait in milliseconds (1000ms = 1 second)
- **param1, param2** → Optional parameters to pass to the function

### Basic Examples

#### Example 1 → Simple Timeout
```javascript
// Execute after 3 seconds
setTimeout(() => {
    console.log("This runs after 3 seconds");
}, 3000);
```

#### Example 2 → Timeout with Function
```javascript
function showMessage() {
    console.log("Hello from timeout!");
}

// Call function after 2 seconds
setTimeout(showMessage, 2000);
```

#### Example 3 → Timeout with Parameters
```javascript
function greet(name, age) {
    console.log(`Hello ${name}, you are ${age} years old`);
}

// Pass parameters to the function
setTimeout(greet, 1000, "John", 25);
```

#### Example 4 → Immediate Timeout (0ms)
```javascript
console.log("Start");

setTimeout(() => {
    console.log("This runs after current code finishes");
}, 0);

console.log("End");

// Output:
// "Start"
// "End"
// "This runs after current code finishes"
```

---

## setInterval

### Definition
**setInterval** repeatedly executes a function at specified time intervals.

### Syntax
```javascript
setInterval(function, interval, param1, param2, ...)
```

### Parameters
- **function** → The function to execute repeatedly
- **interval** → Time between executions in milliseconds
- **param1, param2** → Optional parameters to pass to the function

### Basic Examples

#### Example 1 → Simple Interval
```javascript
// Execute every 2 seconds
setInterval(() => {
    console.log("This runs every 2 seconds");
}, 2000);
```

#### Example 2 → Interval Counter
```javascript
let count = 0;

// Increase counter every second
setInterval(() => {
    count++;
    console.log(`Count: ${count}`);
}, 1000);
```

#### Example 3 → Interval with Function
```javascript
function updateClock() {
    const now = new Date();
    console.log(`Current time: ${now.toLocaleTimeString()}`);
}

// Update clock every second
setInterval(updateClock, 1000);
```

#### Example 4 → Interval with Parameters
```javascript
function showStatus(message, count) {
    console.log(`${message} - Count: ${count}`);
}

let counter = 0;
setInterval(showStatus, 1500, "Processing", counter++);
```

---

## Clearing Timers

### Definition
You can stop timers using `clearTimeout` and `clearInterval`.

### clearTimeout
```javascript
// Start a timeout
const timeoutId = setTimeout(() => {
    console.log("This will never run");
}, 3000);

// Cancel the timeout
clearTimeout(timeoutId);
console.log("Timeout cancelled");
```

### clearInterval
```javascript
let counter = 0;

// Start an interval
const intervalId = setInterval(() => {
    counter++;
    console.log(`Counter: ${counter}`);
    
    // Stop after 5 counts
    if (counter >= 5) {
        clearInterval(intervalId);
        console.log("Interval stopped");
    }
}, 1000);
```

### Practical Clearing Examples

#### Example 1 → Stopwatch with Stop Button
```javascript
let seconds = 0;
let timerId;

function startStopwatch() {
    timerId = setInterval(() => {
        seconds++;
        console.log(`Elapsed: ${seconds} seconds`);
    }, 1000);
}

function stopStopwatch() {
    clearInterval(timerId);
    console.log("Stopwatch stopped");
}

// Start the stopwatch
startStopwatch();

// Stop after 10 seconds
setTimeout(stopStopwatch, 10000);
```

#### Example 2 → Cancellable Message
```javascript
let messageTimer;

function showTemporaryMessage() {
    messageTimer = setTimeout(() => {
        console.log("Important message!");
    }, 5000);
}

function cancelMessage() {
    if (messageTimer) {
        clearTimeout(messageTimer);
        console.log("Message cancelled");
    }
}

// Start message timer
showTemporaryMessage();

// Cancel after 2 seconds (before message shows)
setTimeout(cancelMessage, 2000);
```

---

## Practical Examples

### Example 1 → Countdown Timer
```javascript
function startCountdown(seconds) {
    let timeLeft = seconds;
    
    const countdown = setInterval(() => {
        console.log(`Time left: ${timeLeft} seconds`);
        timeLeft--;
        
        if (timeLeft < 0) {
            clearInterval(countdown);
            console.log("Time's up! 🎉");
        }
    }, 1000);
}

// Start 10 second countdown
startCountdown(10);
```

### Example 2 → Typing Effect
```javascript
function typeText(text, element) {
    let index = 0;
    
    const typing = setInterval(() => {
        // Simulate adding text to element
        console.log(text.substring(0, index));
        index++;
        
        if (index > text.length) {
            clearInterval(typing);
        }
    }, 100);
}

// Simulate typing effect
typeText("Hello, welcome to JavaScript!", "output");
```

### Example 3 → Slideshow
```javascript
const images = ["Image 1", "Image 2", "Image 3", "Image 4"];
let currentIndex = 0;

function startSlideshow() {
    const slideshow = setInterval(() => {
        console.log(`Showing: ${images[currentIndex]}`);
        currentIndex = (currentIndex + 1) % images.length;
    }, 2000);
    
    return slideshow;
}

// Start slideshow
const slideshowId = startSlideshow();

// Stop after 10 seconds
setTimeout(() => {
    clearInterval(slideshowId);
    console.log("Slideshow ended");
}, 10000);
```

### Example 4 → API Polling
```javascript
function checkServerStatus() {
    console.log("Checking server status...");
    // Simulate API call
    const isOnline = Math.random() > 0.3;
    console.log(isOnline ? "Server is online ✅" : "Server is offline ❌");
    
    return isOnline;
}

// Check server status every 5 seconds
const statusChecker = setInterval(checkServerStatus, 5000);

// Stop checking after 30 seconds
setTimeout(() => {
    clearInterval(statusChecker);
    console.log("Stopped monitoring server");
}, 30000);
```

---

## Common Use Cases

### 1. Delayed Actions
```javascript
// Show success message after form submission
function submitForm() {
    console.log("Form submitted!");
    
    setTimeout(() => {
        console.log("✅ Form processed successfully");
    }, 2000);
}

submitForm();
```

### 2. Animation Sequences
```javascript
function animateSequence() {
    console.log("Animation started");
    
    setTimeout(() => console.log("Step 1 complete"), 1000);
    setTimeout(() => console.log("Step 2 complete"), 2000);
    setTimeout(() => console.log("Step 3 complete"), 3000);
    setTimeout(() => console.log("Animation finished"), 4000);
}

animateSequence();
```

### 3. Debouncing User Input
```javascript
let searchTimer;

function handleSearch(input) {
    // Clear previous timer
    clearTimeout(searchTimer);
    
    // Set new timer
    searchTimer = setTimeout(() => {
        console.log(`Searching for: ${input}`);
        // Actual search logic here
    }, 500);
}

// Simulate user typing
handleSearch("jav");
handleSearch("java");
handleSearch("javascript"); // Only this search will execute
```

### 4. Periodic Updates
```javascript
// Update dashboard every 30 seconds
function updateDashboard() {
    console.log("Updating dashboard data...");
    // Fetch new data and update UI
}

// Start periodic updates
const dashboardUpdater = setInterval(updateDashboard, 30000);

// Stop updates when user leaves page
setTimeout(() => {
    clearInterval(dashboardUpdater);
    console.log("Dashboard updates stopped");
}, 300000); // Stop after 5 minutes
```

---

## Best Practices

### 1. Always Clear Intervals
```javascript
// Good: Clear interval when done
let dataRefresh = setInterval(fetchData, 5000);

// Later, when no longer needed
clearInterval(dataRefresh);
```

### 2. Use Variables for Timer IDs
```javascript
// Good: Store timer ID
const timerId = setTimeout(myFunction, 1000);

// Bad: No way to clear later
setTimeout(myFunction, 1000);
```

### 3. Handle Cleanup
```javascript
function startProcess() {
    const processId = setInterval(() => {
        // Do work
    }, 1000);
    
    // Return cleanup function
    return () => clearInterval(processId);
}

const cleanup = startProcess();

// When done, call cleanup
setTimeout(cleanup, 10000);
```

### 4. Avoid Memory Leaks
```javascript
// Good: Clear timers in event handlers
let autoSaveTimer;

document.getElementById('saveBtn').addEventListener('click', () => {
    clearTimeout(autoSaveTimer);
    autoSaveTimer = setTimeout(saveDocument, 2000);
});
```

---

## Summary

### setTimeout vs setInterval

| Feature | setTimeout | setInterval |
|---------|------------|-------------|
| **Execution** | Once after delay | Repeatedly at intervals |
| **Returns** | Timer ID | Timer ID |
| **Clearing** | clearTimeout() | clearInterval() |
| **Use Case** | One-time delayed actions | Repeated actions |

### Syntax Comparison
```javascript
// setTimeout - runs once
const timeoutId = setTimeout(function, delay, param1, param2);

// setInterval - runs repeatedly  
const intervalId = setInterval(function, interval, param1, param2);
```

### Common Patterns

#### Basic Usage
```javascript
// One-time delay
setTimeout(() => {
    console.log("Done waiting!");
}, 2000);

// Repeated action
setInterval(() => {
    console.log("Tick-tock");
}, 1000);
```

#### With Clearing
```javascript
// Start timer
const timer = setTimeout(someFunction, 5000);

// Cancel if needed
clearTimeout(timer);
```

#### Chained Timeouts (Alternative to setInterval)
```javascript
function repeatedTask() {
    console.log("Task executed");
    
    // Schedule next execution
    setTimeout(repeatedTask, 1000);
}

// Start the chain
setTimeout(repeatedTask, 1000);
```

### Key Points to Remember
1. **Time is in milliseconds** (1000ms = 1 second)
2. **Always store timer IDs** so you can clear them later
3. **Clear intervals** when they're no longer needed
4. **setTimeout with 0ms** doesn't run immediately - it waits for current code to finish
5. **Timers are not precise** - they're minimum delays, not exact

### Quick Reference
```javascript
// Common time conversions
const second = 1000;
const minute = 60 * second;
const hour = 60 * minute;

// Usage
setTimeout(task, 2 * second);    // 2 seconds
setInterval(task, 5 * minute);   // 5 minutes
```

---