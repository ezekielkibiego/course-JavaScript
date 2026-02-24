# Introduction to Asynchronous Programming

## What is Asynchronous Programming?

Asynchronous JavaScript is a programming approach that enables non-blocking execution of tasks, allowing concurrent operations and efficient handling of time-consuming operations in web applications. Although JavaScript is single-threaded and synchronous by default, it can appear asynchronous through various patterns and APIs.

Several methods exist for performing asynchronous JavaScript tasks:

**Callbacks** are functions passed as arguments to be executed after an asynchronous operation completes. They ensure non-blocking execution but can lead to callback hell with nested functions.

**Promises** are objects representing the eventual completion or failure of an asynchronous operation, providing better handling through `.then()` and `.catch()` methods.

**Async/await** is syntactic sugar built on Promises, allowing asynchronous code to be written in a more synchronous style for improved readability.

## Callback Functions

A callback function is a function passed as an argument to another function and executed later. Callbacks allow one function to call another at a later time, enabling asynchronous execution and flexible code design.

### Basic Callback Example

```javascript
function greet(name, callback) {
    console.log("Hello, " + name);
    callback();
}

function sayBye() {
    console.log("Goodbye!");
}

greet("Joseph", sayBye);
```

Here, `sayBye()` is passed as a callback to `greet()`, which executes after the greeting.

### How Callbacks Work

JavaScript executes code line by line synchronously, but callbacks enable delayed or event-based execution. When a callback is passed to a function, it runs after the main task completes.

### Asynchronous Callbacks

```javascript
console.log("Start");

setTimeout(function () {
    console.log("Inside setTimeout");
}, 2000);

console.log("End");
```

`setTimeout()` is asynchronous and takes a callback to execute after 2 seconds. The rest of the code continues without waiting.

### Common Use Cases

**API Requests & File Operations:** Callbacks handle responses from API calls and file system operations.

**Event Listeners:** User interactions trigger callbacks.

```javascript
document.getElementById("myButton").addEventListener("click", function () {
    console.log("Button clicked!");
});
```

**Higher-Order Functions:** Functions accept other functions as parameters for flexible behavior.

```javascript
function calc(a, b, callback) {
    return callback(a, b);
}

console.log(calc(5, 3, (x, y) => x + y));   // 8
console.log(calc(5, 3, (x, y) => x * y));   // 15
```

### Callback Hell Problem

Deeply nested callbacks become hard to read and maintain:

```javascript
step1(() => {
    step2(() => {
        step3(() => {
            console.log("All steps completed");
        });
    });
});
```

### Solutions: Promises and Async/Await

Promises and async/await provide cleaner alternatives to callback nesting, offering better error handling and readability.


## JavaScript Promises

Promises make handling asynchronous operations like API calls, file loading, or time delays easier. Think of a Promise as a placeholder for a value that will be available in the future. It can be in one of three states:

- **Pending:** The task is in the initial state.
- **Fulfilled:** The task was completed successfully, and the result is available.
- **Rejected:** The task failed, and an error is provided.

### Basic Promise Example

Here's an example Promise to check if a number is even:

```javascript
let checkEven = new Promise((resolve, reject) => {
    let number = 4;
    if (number % 2 === 0) resolve("The number is even!");
    else reject("The number is odd!");
});

checkEven
    .then((message) => console.log(message)) // On success
    .catch((error) => console.error(error)); // On failure
```

**Note:** The `resolve` and `reject` are not keywords. You can use any name you want to give to the functions.

### Syntax

```javascript
let promise = new Promise((resolve, reject) => {
    // Perform async operation
    if (operationSuccessful) {
        resolve("Task successful");
    } else {
        reject("Task failed");
    }
});
```

- **`resolve(value)`:** Marks the promise as fulfilled and provides a result.
- **`reject(error)`:** Marks the promise as rejected with an error.

### Advanced Promise Methods

#### 1. Promise.all()
Waits for all promises to resolve and returns their results as an array. If any promise is rejected, it immediately rejects.

```javascript
Promise.all([
    Promise.resolve("Task 1 completed"),
    Promise.resolve("Task 2 completed"),
    Promise.reject("Task 3 failed")
])
    .then((results) => console.log(results))
    .catch((error) => console.error(error));
```

#### 2. Promise.allSettled()
Waits for all promises to settle (fulfilled or rejected) and returns an array of their outcomes.

```javascript
Promise.allSettled([
    Promise.resolve("Task 1 completed"),
    Promise.reject("Task 2 failed"),
    Promise.resolve("Task 3 completed")
])
    .then((results) => console.log(results));
```

#### 3. Promise.race()
Resolves or rejects as soon as the first promise settles.

```javascript
Promise.race([
    new Promise((resolve) =>
        setTimeout(() => resolve("Task 1 finished"), 1000)),
    new Promise((resolve) =>
        setTimeout(() => resolve("Task 2 finished"), 500))
]).then((result) => console.log(result));
```

#### 4. Promise.any()
Resolves with the first fulfilled promise. If all are rejected, it rejects with an `AggregateError`.

```javascript
Promise.any([
    Promise.reject("Task 1 failed"),
    Promise.resolve("Task 2 completed"),
    Promise.resolve("Task 3 completed")
])
    .then((result) => console.log(result))
    .catch((error) => console.error(error));
```

#### 5. Promise.resolve()
Returns a promise that resolves with the given value.

```javascript
Promise.resolve("Immediate success")
    .then((value) => console.log(value));
```

#### 6. Promise.reject()
Returns a promise that immediately rejects with a given reason.

```javascript
Promise.reject("Immediate failure")
    .catch((error) => console.error(error));
```

#### 7. Promise.finally()
Runs cleanup or final code block regardless of the promise's result.

```javascript
Promise.resolve("Task completed")
    .then((result) => console.log(result))
    .catch((error) => console.error(error))
    .finally(() => console.log("Cleanup completed"));
```

#### 8. Chaining with .then()
Allows sequential execution of promises, passing results to the next `.then()`.

```javascript
Promise.resolve(5)
    .then((value) => value * 2)     // Multiplies by 2
    .then((value) => value + 3)     // Adds 3
    .then((finalValue) => console.log(finalValue)); // Logs: 13
```

#### 9. Sequential Execution with reduce()

```javascript
let tasks = [1, 2, 3];
tasks.reduce((prevPromise, current) => {
    return prevPromise.then(() => {
        return new Promise((resolve) => {
            console.log(`Processing task ${current}`);
            setTimeout(resolve, 500);
        });
    });
}, Promise.resolve());
```

#### 10. Dynamic Promise Creation

```javascript
function asyncTask(taskName) {
    return new Promise((resolve) => {
        setTimeout(() => 
            resolve(`${taskName} completed`), 1000);
    });
}

asyncTask("Download File").then((result) => 
    console.log(result));
```

#### 11. Timeout Handling with Promise.race()

```javascript
let fetchData = new Promise((resolve) =>
    setTimeout(() => resolve("Data loaded"), 3000));

let timeout = new Promise((_, reject) =>
    setTimeout(() => reject("Timeout!"), 2000));

Promise.race([fetchData, timeout])
    .then((result) => console.log(result))
    .catch((error) => console.error(error));
```

#### 12. Handling Multiple Failures with Promise.allSettled()

```javascript
Promise.allSettled([
    Promise.resolve("Task 1 done"),
    Promise.reject("Task 2 failed"),
    Promise.resolve("Task 3 done")
])
    .then((results) => console.log(results));
```

#### 13. Parallel and Sequential Execution

```javascript
Promise.all([
    new Promise((resolve) =>
        setTimeout(() => resolve("Task A done"), 1000)),
    new Promise((resolve) =>
        setTimeout(() => resolve("Task B done"), 500))
])
    .then(([resultA, resultB]) => {
        console.log(resultA, resultB);
        return new Promise((resolve) =>
            setTimeout(() => resolve("Final Task done"), 700));
    })
    .then((finalResult) => console.log(finalResult));
```

#### 14. Converting Callbacks to Promises

```javascript
function loadData(callback) {
    setTimeout(() => 
        callback("Data loaded"), 1000);
}

function promisifiedLoadData() {
    return new Promise((resolve) => {
        loadData((result) => resolve(result));
    });
}

promisifiedLoadData().then((data) => console.log(data));
```

### Benefits of Promises

- **Avoid Callback Hell:** Promises organize asynchronous code more cleanly than nested callbacks.
- **Error Handling:** Errors can be caught in one place using `.catch()`.
- **Chaining:** Perform tasks sequentially with `.then()`.

## Event Loop in JavaScript

The event loop is an important concept in JavaScript that enables asynchronous programming by handling tasks efficiently. Since JavaScript is single-threaded, it uses the event loop to manage the execution of multiple tasks without blocking the main thread.

### Execution Order Example

```javascript
console.log("Start");

setTimeout(() => {
    console.log("setTimeout Callback");
}, 0);

Promise.resolve().then(() => {
    console.log("Promise Resolved");
});

console.log("End");
```

**Output:**
```
Start
End
Promise Resolved
setTimeout Callback
```

**Explanation:**
- `console.log("Start")` executes first.
- `setTimeout` schedules its callback but does not execute it immediately.
- `Promise.resolve().then()` is placed in the microtask queue and executes before the callback queue.
- "Promise Resolved" appears before "setTimeout Callback" due to microtask priority.

JavaScript executes code synchronously in a single thread. However, it can handle asynchronous operations such as fetching data from an API, handling user events, or setting timeouts without pausing execution. This is made possible by the event loop.

### How the Event Loop Works

The event loop continuously checks whether the call stack is empty and whether there are pending tasks in the callback queue or microtask queue.

**Key Components:**

- **Call Stack:** JavaScript has a call stack where function execution is managed in a Last-In, First-Out (LIFO) order.
- **Web APIs (Background Tasks):** These include `setTimeout`, `setInterval`, `fetch`, DOM events, and other non-blocking operations.
- **Callback Queue (Task Queue):** When an asynchronous operation is completed, its callback is pushed into the task queue.
- **Microtask Queue:** Promises and other microtasks go into the microtask queue, which is processed before the task queue.
- **Event Loop:** It continuously checks the call stack and, if empty, moves tasks from the queue to the stack for execution.

### Phases of the Event Loop

The event loop operates in multiple phases:

1. **Timers Phase:** Executes callbacks from `setTimeout` and `setInterval`.
2. **I/O Callbacks Phase:** Handles I/O operations like file reading, network requests, etc.
3. **Prepare Phase:** Internal phase used by Node.js.
4. **Poll Phase:** Retrieves new I/O events and executes callbacks.
5. **Check Phase:** Executes callbacks from `setImmediate`.
6. **Close Callbacks Phase:** Executes close event callbacks, e.g., `socket.on('close')`.
7. **Microtask Execution:** After each phase, the event loop processes the microtask queue before moving to the next phase.

### Common Issues Related to the Event Loop

#### 1. Blocking the Main Thread

Heavy computations block the event loop, making the app unresponsive.

```javascript
while(true) {
    console.log('Blocking...')
}
```

An infinite `while(true)` loop continuously runs, blocking the event loop and freezing the browser by preventing any other task from executing.

#### 2. Delayed Execution of setTimeout

`setTimeout` doesn't always run exactly after the specified time.

```javascript
console.log("Start");
setTimeout(() => console.log("Inside setTimeout"), 1000);
for (let i = 0; i < 1e9; i++) {} // Long loop
console.log("End");
```

The blocking loop delays `setTimeout` execution because the Call Stack is busy. This code will also lead to Time Limit Exceed Error or will freeze the browser.

#### 3. Priority of Microtasks Over Callbacks

Microtasks run before `setTimeout`, even if set with 0ms delay.

```javascript
setTimeout(() => console.log("setTimeout"), 0);
Promise.resolve().then(() => console.log("Promise"));
console.log("End");
```

The event loop first checks for functions in the microtask queue and then in the callback queue. In JavaScript, the microtask queue is given more priority than the callback queue, which is why functions present in the microtask queue are executed first.

#### 4. Callback Hell

Too many nested callbacks make code unreadable.

```javascript
setTimeout(() => {
    console.log("Step 1");
    setTimeout(() => {
        console.log("Step 2");
        setTimeout(() => {
            console.log("Step 3");
        }, 1000);
    }, 1000);
}, 1000);
```

This creates callback hell, making it hard to read and maintain. Use Promises or async/await instead.

### Best Practices for Working with the Event Loop

- **Use Asynchronous Operations:** Avoid blocking the event loop with synchronous file reads or complex calculations.
- **Optimize Long-Running Tasks:** Use worker threads or child processes for CPU-intensive tasks.
- **Use Microtasks Wisely:** Since microtasks execute before other queued tasks, excessive usage can delay other operations.
- **Leverage setImmediate() for High-Priority Tasks:** Unlike `setTimeout(fn, 0)`, `setImmediate()` executes immediately after the I/O phase.
- **Debug Using Performance Tools:** Utilize Node.js Performance Hooks and the Chrome DevTools profiler to monitor the event loop behavior.

## Async and Await in JavaScript

Async/await allows you to write asynchronous code in a clean, synchronous-like manner, making it easier to read, understand, and maintain while working with promises.

### Key Benefits

- **async functions always return a Promise**
- **await pauses execution** until the Promise is resolved or rejected
- **Improves readability** compared to `.then()` and `.catch()` chaining
- **Simpler error handling** using `try...catch`
- **Ideal for managing complex asynchronous flows** in a structured way

### Basic Example

```javascript
async function fetchData() {
    try {
        const response = await Promise.resolve({
            json: async () => ({
                userId: 1,
                id: 1,
                title: "Sample Post",
                body: "This is mock data for async/await demonstration"
            })
        });

        const data = await response.json();
        console.log(data);
    } catch (error) {
        console.error("Error fetching data:", error);
    }
}

fetchData();
```

### Basic Syntax

```javascript
async function functionName() {
    try {
        const result = await someAsyncFunction();
        console.log(result);
    } catch (error) {
        console.error("Error:", error.message);
    }
}
```

## Async Functions

Async functions let you write promise-based code in a synchronous-looking way, improving readability while keeping execution non-blocking. An async function always returns a Promise — if it returns a non-promise value, JavaScript automatically wraps it in a resolved Promise.

### Benefits

- Makes asynchronous code easier to read and maintain
- Does not block the main execution thread
- Always returns a Promise
- Non-promise return values are auto-wrapped in `Promise.resolve()`
- Works seamlessly with `await` for handling promises

### Examples

```javascript
async function myFunction() {
    return "Hello";
}

const getData = async () => {
        let data = "Hello World";
        return data;
}

getData().then(data => console.log(data));
```

## Await Keyword

The `await` keyword pauses the execution of an async function until a Promise is resolved or rejected. It can only be used inside an async function, making asynchronous code easier to read and manage.

### Key Points

- Used to wait for a Promise to settle
- Can only be used inside async functions
- Prevents callback and `.then()` chaining
- Makes asynchronous code cleaner and more readable
- Supports error handling with `try...catch`

### Example

```javascript
const getData = async () => {
        let y = await "Hello World";
        console.log(y);
}

console.log(1);
getData();
console.log(2);
```

The `async` keyword transforms a regular JavaScript function into an asynchronous function, causing it to return a Promise. The `await` keyword is used inside an async function to pause its execution and wait for a Promise to resolve before continuing.

## Error Handling in Async/Await

Use `try...catch` blocks to handle errors in async functions. This provides cleaner error handling compared to `.catch()` chains.

```javascript
async function fetchData() {
    try {
        let response = await fetch('https://jsonplaceholder.typicode.com/posts/');
        let data = await response.json();
        console.log(data);
    } catch (error) {
        console.error('Error fetching data:', error);
    }
}
fetchData()
```

### Breakdown

- **`async function fetchData()`:** Declares an asynchronous function that always returns a Promise
- **`await fetch(...)`:** Sends an HTTP request and waits for the response without blocking the main thread
- **`await response.json()`:** Converts the response body into JavaScript data (JSON format)
- **`console.log(data)`:** Prints the fetched data to the console if the request is successful
- **`try...catch`:** Handles errors such as network failure or invalid responses


