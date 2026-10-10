# JavaScript Promises

## Table of Contents
- [What are Promises?](#what-are-promises)
- [Promise States](#promise-states)
- [Creating Promises](#creating-promises)
- [Using Promises](#using-promises)
- [Promise Chaining](#promise-chaining)
- [Error Handling](#error-handling)
- [Promise Methods](#promise-methods)
- [Async/Await](#asyncawait)
- [Summary](#summary)

---

## What are Promises?

### Definition
A **Promise** is an object that represents the eventual completion (or failure) of an asynchronous operation and its resulting value.

### Simple Definition
A promise is like a receipt you get when you order food. It doesn't give you the food immediately, but it guarantees you'll get it later (or get a reason why you can't).

### Basic Example
```javascript
// Creating a promise
const myPromise = new Promise((resolve, reject) => {
    // Async operation here
    const success = true;
    
    if (success) {
        resolve("Operation completed successfully!");
    } else {
        reject("Operation failed!");
    }
});

// Using the promise
myPromise
    .then(result => {
        console.log(result); // "Operation completed successfully!"
    })
    .catch(error => {
        console.log(error); // "Operation failed!"
    });
```

---

## Promise States

A promise can be in one of three states:

### 1. Pending
- Initial state
- Operation not completed yet

### 2. Fulfilled
- Operation completed successfully
- `.then()` method is called

### 3. Rejected
- Operation failed
- `.catch()` method is called

```javascript
// Visualizing promise states
const promise = new Promise((resolve, reject) => {
    // State: Pending
    // ... some operation
});

promise
    .then(result => {
        // State: Fulfilled
    })
    .catch(error => {
        // State: Rejected
    });
```

---

## Creating Promises

### Basic Promise Creation
```javascript
// Success case
const successPromise = new Promise((resolve, reject) => {
    resolve("Data loaded successfully");
});

// Failure case  
const failurePromise = new Promise((resolve, reject) => {
    reject("Failed to load data");
});
```

### Real-world Example: User Authentication
```javascript
function loginUser(email, password) {
    return new Promise((resolve, reject) => {
        // Simulate API call
        if (email === "user@example.com" && password === "password") {
            resolve({ 
                userId: 123, 
                name: "John Doe", 
                email: email 
            });
        } else {
            reject("Invalid email or password");
        }
    });
}
```

### Real-world Example: File Validation
```javascript
function validateFile(file) {
    return new Promise((resolve, reject) => {
        const allowedTypes = ['image/jpeg', 'image/png', 'application/pdf'];
        const maxSize = 5 * 1024 * 1024; // 5MB
        
        if (!allowedTypes.includes(file.type)) {
            reject("File type not allowed");
        } else if (file.size > maxSize) {
            reject("File too large");
        } else {
            resolve({ 
                name: file.name, 
                size: file.size, 
                type: file.type 
            });
        }
    });
}
```

---

## Using Promises

### .then() method
Handles successful promise resolution
```javascript
const userPromise = getUserData(123);

userPromise.then(user => {
    console.log("User data:", user);
    return user.email; // Pass to next .then()
}).then(email => {
    console.log("User email:", email);
});
```

### .catch() method
Handles promise rejection
```javascript
getUserData(999)
    .then(user => {
        console.log("User found:", user);
    })
    .catch(error => {
        console.log("Error:", error); // Handles any rejection in chain
    });
```

### .finally() method
Runs regardless of success or failure
```javascript
loadData()
    .then(data => {
        console.log("Data loaded:", data);
    })
    .catch(error => {
        console.log("Error loading data:", error);
    })
    .finally(() => {
        console.log("Data loading attempt completed");
        // Good for cleanup operations
    });
```

---

## Promise Chaining

### Sequential Operations
```javascript
function getUser(userId) {
    return new Promise(resolve => {
        resolve({ id: userId, name: "John Doe" });
    });
}

function getUserPosts(user) {
    return new Promise(resolve => {
        resolve([...user.posts, "New Post"]);
    });
}

function getPostComments(post) {
    return new Promise(resolve => {
        resolve([...post.comments, "Nice post!"]);
    });
}

// Promise chaining
getUser(123)
    .then(user => {
        console.log("User:", user);
        return getUserPosts(user);
    })
    .then(posts => {
        console.log("User posts:", posts);
        return getPostComments(posts[0]);
    })
    .then(comments => {
        console.log("Post comments:", comments);
    })
    .catch(error => {
        console.log("Error in chain:", error);
    });
```

### Data Transformation Chain
```javascript
// Start with initial data
const initialData = 10;

// Create a promise that resolves immediately
Promise.resolve(initialData)
    .then(number => {
        console.log("Initial:", number); // 10
        return number * 2; // 20
    })
    .then(number => {
        console.log("After multiplication:", number); // 20
        return number + 5; // 25
    })
    .then(number => {
        console.log("After addition:", number); // 25
        return number / 5; // 5
    })
    .then(finalResult => {
        console.log("Final result:", finalResult); // 5
    });
```

---

## Error Handling

### Single .catch() for Entire Chain
```javascript
getUserData()
    .then(user => validateUser(user))
    .then(validUser => processUser(validUser))
    .then(result => saveResult(result))
    .catch(error => {
        // Catches ANY error in the entire chain
        console.log("Something went wrong:", error);
    });
```

### Handling Specific Errors
```javascript
function processOrder(orderId) {
    return validateOrder(orderId)
        .then(order => processPayment(order))
        .then(payment => sendConfirmation(payment))
        .catch(error => {
            if (error.type === 'validation') {
                console.log("Order validation failed");
                return { status: 'retry' };
            } else if (error.type === 'payment') {
                console.log("Payment processing failed");
                return { status: 'failed' };
            } else {
                throw error; // Re-throw unknown errors
            }
        });
}
```

---

## Promise Methods

### Promise.resolve()
Creates a resolved promise
```javascript
const resolvedPromise = Promise.resolve("Immediate value");

resolvedPromise.then(value => {
    console.log(value); // "Immediate value"
});
```

### Promise.reject()
Creates a rejected promise
```javascript
const rejectedPromise = Promise.reject("Immediate error");

rejectedPromise.catch(error => {
    console.log(error); // "Immediate error"
});
```

### Promise.all()
Waits for ALL promises to resolve
```javascript
const promise1 = getUser(1);
const promise2 = getUser(2);
const promise3 = getUser(3);

Promise.all([promise1, promise2, promise3])
    .then(users => {
        console.log("All users:", users); // Array of all results
    })
    .catch(error => {
        console.log("One promise failed:", error);
        // Fails if ANY promise rejects
    });
```

### Promise.race()
Returns when FIRST promise settles
```javascript
const fastApi = fetchFromFastServer();
const slowApi = fetchFromSlowServer();

Promise.race([fastApi, slowApi])
    .then(firstResult => {
        console.log("First response:", firstResult);
        // Uses whichever responds first
    });
```

### Promise.allSettled()
Waits for ALL promises to complete (success or failure)
```javascript
const promises = [
    Promise.resolve("Success"),
    Promise.reject("Error"),
    Promise.resolve("Another success")
];

Promise.allSettled(promises)
    .then(results => {
        results.forEach(result => {
            if (result.status === 'fulfilled') {
                console.log("Success:", result.value);
            } else {
                console.log("Failed:", result.reason);
            }
        });
    });
```

---

## Async/Await

### Basic Async/Await
```javascript
// async function always returns a promise
async function getUserData() {
    try {
        const user = await getUser(123); // Wait for promise to resolve
        const posts = await getUserPosts(user.id);
        const comments = await getPostComments(posts[0].id);
        
        return { user, posts, comments };
    } catch (error) {
        console.log("Error:", error);
        throw error; // Re-throw to let caller handle
    }
}

// Usage
getUserData()
    .then(data => console.log("User data:", data))
    .catch(error => console.log("Failed:", error));
```

### Multiple Awaits in Parallel
```javascript
async function loadUserDashboard(userId) {
    try {
        // Run promises in parallel
        const [user, posts, settings] = await Promise.all([
            getUser(userId),
            getUserPosts(userId),
            getUserSettings(userId)
        ]);
        
        return { user, posts, settings };
    } catch (error) {
        console.log("Failed to load dashboard:", error);
    }
}
```

---

## Practical Examples

### Example 1 → E-commerce Order Processing
```javascript
class OrderProcessor {
    processOrder(order) {
        return this.validateOrder(order)
            .then(validOrder => this.checkInventory(validOrder))
            .then(availableOrder => this.processPayment(availableOrder))
            .then(paidOrder => this.shipOrder(paidOrder))
            .then(shippedOrder => {
                console.log("Order completed:", shippedOrder);
                return shippedOrder;
            });
    }
    
    validateOrder(order) {
        return new Promise((resolve, reject) => {
            if (order.items && order.items.length > 0) {
                resolve(order);
            } else {
                reject("Order must contain items");
            }
        });
    }
    
    checkInventory(order) {
        return new Promise(resolve => {
            // Simulate inventory check
            order.items.forEach(item => item.inStock = true);
            resolve(order);
        });
    }
    
    processPayment(order) {
        return new Promise((resolve, reject) => {
            // Simulate payment processing
            const paymentSuccess = Math.random() > 0.2;
            if (paymentSuccess) {
                order.paymentStatus = 'paid';
                resolve(order);
            } else {
                reject("Payment failed");
            }
        });
    }
    
    shipOrder(order) {
        return new Promise(resolve => {
            order.shippingStatus = 'shipped';
            order.trackingNumber = 'TRK' + Date.now();
            resolve(order);
        });
    }
}

// Usage
const processor = new OrderProcessor();
processor.processOrder({ items: [{ id: 1, name: "Product", price: 100 }] })
    .then(order => console.log("Success:", order))
    .catch(error => console.log("Error:", error));
```

### Example 2 → Form Validation Chain
```javascript
function validateRegistration(formData) {
    return Promise.resolve(formData)
        .then(data => validateEmail(data.email))
        .then(data => validatePassword(data.password))
        .then(data => checkUsernameAvailability(data.username))
        .then(data => {
            console.log("All validations passed");
            return { success: true, user: data };
        })
        .catch(error => {
            console.log("Validation failed:", error);
            return { success: false, error: error };
        });
}

function validateEmail(email) {
    return new Promise((resolve, reject) => {
        if (email.includes('@')) {
            resolve({ email });
        } else {
            reject("Invalid email format");
        }
    });
}

function validatePassword(password) {
    return new Promise((resolve, reject) => {
        if (password.length >= 6) {
            resolve({ password });
        } else {
            reject("Password too short");
        }
    });
}

function checkUsernameAvailability(username) {
    return new Promise((resolve, reject) => {
        const takenUsernames = ['admin', 'user', 'test'];
        if (!takenUsernames.includes(username)) {
            resolve({ username });
        } else {
            reject("Username already taken");
        }
    });
}
```

---

## Summary

### Promise Creation
```javascript
// Create promise
const promise = new Promise((resolve, reject) => {
    // Do work
    if (success) {
        resolve(value);
    } else {
        reject(error);
    }
});
```

### Promise Usage
```javascript
promise
    .then(result => {
        // Handle success
    })
    .catch(error => {
        // Handle error
    })
    .finally(() => {
        // Always execute
    });
```

### Static Methods
```javascript
Promise.resolve(value) // Create resolved promise
Promise.reject(error)  // Create rejected promise  
Promise.all([p1, p2])  // Wait for all promises
Promise.race([p1, p2]) // First to settle wins
```

### Async/Await
```javascript
async function myFunction() {
    try {
        const result = await somePromise;
        return result;
    } catch (error) {
        console.log(error);
    }
}
```

### Key Points to Remember
1. **Promises handle async operations** cleanly
2. **Use .then()** for success cases
3. **Use .catch()** for error handling  
4. **Chain promises** for sequential operations
5. **Use Promise.all()** for parallel operations
6. **Async/await** makes promise code more readable
7. **Always handle errors** in promise chains

---