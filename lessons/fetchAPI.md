# Fetch API in JavaScript

The Fetch API is a modern interface in JavaScript that allows you to make HTTP requests. It replaces the older XMLHttpRequest method and provides a cleaner and more flexible way to fetch resources asynchronously. The Fetch API uses Promises, making it easier to work with asynchronous data.

## Syntax

```javascript
fetch(url, options)
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

- **url**: The API endpoint from which data is fetched.
- **options** (optional): Specifies method, headers, body, etc.
- **response.json()**: Parses the response as JSON.
- **.catch(error)**: Handles any errors that occur during the request.

## How Fetch API Works?

1. A request is sent to the specified URL.
2. The server processes the request and sends a response.
3. The response is converted to JSON (or another format) using `.json()`.
4. Errors are handled using `.catch()` or try-catch blocks.

## Common HTTP Request Methods in Fetch API

- **GET**: Retrieves data from another server.
- **POST**: Adds data to the server.
- **PUT**: Updates data on the server.
- **DELETE**: Removes data from the server.

## Basic Fetch Request

A simple GET request to fetch data from an API.

```javascript
fetch('https://fakestoreapi.com/products/1')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

- `fetch()` sends an HTTP request to the specified URL.
- `.json()` parses the response body as JSON.
- `.then()` handles the resolved promise with the fetched data, and `.catch()` catches any errors (e.g., network issues).

## Handling Response Status Codes

When making an HTTP request, handling response status codes is crucial for determining whether the request was successful or if there was an error.

```javascript
fetch('https://jsonplaceholder.typicode.com/posts/')
    .then(response => {
        if (response.ok) {
            return response.json(); 
        } else {
            throw new Error('Network response was not ok'); 
        }
    })
    .then(data => console.log(data))
    .catch(error => console.error('There was a problem with the fetch operation:', error));
```

- **fetch()**: Initiates a network request to the provided URL.
- **response.ok**: Checks if the HTTP response status is in the range of 200–299, indicating success.
- **return response.json()**: If the response is successful, the data is parsed as JSON for further use.
- **throw new Error()**: If the status code indicates an error (e.g., 404 or 500), an error is thrown to handle it.
- **catch(error)**: Catches any errors (network or HTTP issues) and logs them to the console for debugging.

## Using async/await with Fetch API

Using async/await makes handling asynchronous code like fetch cleaner and more readable.

```javascript
async function getProducts() {
    try {
        const response = await fetch('https://fakestoreapi.com/products');
        if (response.ok) {
            const data = await response.json(); 
            console.log(data);
        } else {
            throw new Error('Failed to fetch data');
        }
    } catch (error) {
        console.error('Error:', error); 
    }
}
getProducts();
```

- **async function**: Defines an asynchronous function that can handle tasks like fetching data without blocking the rest of the program.
- **await fetch()**: Pauses execution until the fetch request completes.
- **response.ok**: Checks if the fetch request was successful (status 200-299).
- **await response.json()**: Converts the server response into a JavaScript object.
- **try/catch block**: Catches errors and prevents the program from crashing.

## Handling Different Request Methods

### 1. GET Request to Retrieve Data

```javascript
fetch('https://fakestoreapi.com/products/1')
    .then(response => response.json())
    .then(items => console.log(items));
```

### 2. POST Request to Submit Data

```javascript
const data = { name: 'John', age: 25 };
fetch('https://fakestoreapi.com/products', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(data)
})
    .then(response => response.json())
    .then(result => console.log(result));
```

### 3. PUT Request to Update Data

```javascript
const updatedData = { id: 1, price: 300 };

fetch('https://fakestoreapi.com/products/1', {
    method: 'PUT',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(updatedData)
})
    .then(response => response.json())
    .then(result => console.log(result));
```

### 4. DELETE Request to Remove Data

```javascript
fetch('https://fakestoreapi.com/products/1', {
    method: 'DELETE'
})
    .then(response => response.json())
    .then(result => console.log('Deleted:', result));
```

## Error Handling in Fetch

So far, our `GET` and `POST` examples assume everything goes smoothly — but what if they don't? What happens if the resource doesn't exist or a network error occurs while sending data?

To handle these cases, we can append a `.catch` method to catch network errors and check the response status to handle HTTP errors. Let's look at how to make our fetch requests more resilient.

```javascript
fetch('https://api.example.com/data')
    .then(response => {
        if (!response.ok) {
            throw new Error(`HTTP error! Status: ${response.status}`);
        }
        return response.json();
    })
    .then(data => console.log('Data:', data))
    .catch(error => console.error('Fetch error:', error.message));
```

- **Fetching Data**: The `fetch()` call requests data from the API.
- **Checking for Errors**: The `.then()` block checks if `response.ok` is true. If not, it throws an error.
- **Parsing JSON**: If successful, `response.json()` converts the response into JSON format.
- **Logging Data**: The second `.then()` logs the received data.
- **Handling Errors**: The `.catch()` captures and logs errors.

### Example 2 with UI 

```html
<style>
    .container { font-family: sans-serif; max-width: 400px; margin: 2rem auto; }
    #todoForm { display: flex; gap: 10px; }
    #todoInput { flex: 1; padding: 8px; }3 
    button { padding: 8px 16px; cursor: pointer; }
    #statusMessage { margin-top: 1rem; font-weight: bold; }
</style>
<div class="container">
    <h2>Add New Todo</h2>
    <form id="todoForm">
        <input type="text" id="todoInput" placeholder="Enter todo title..." required>
        <button type="submit">Add Todo</button>
    </form>
    <p id="statusMessage"></p>
</div>
```

```javascript
const form = document.getElementById("todoForm");
const input = document.getElementById("todoInput");
const statusMsg = document.getElementById("statusMessage");
const url = "https://jsonplaceholder.typicode.com/posts";

form.addEventListener("submit", (event) => {
  event.preventDefault();

  const newTodo = {
    title: input.value,
    completed: false,
  };

  fetch(url, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(newTodo),
  })
    .then((response) => {
      // Check if the HTTP status is in the 200-299 range
      if (!response.ok) {
        throw new Error(`HTTP error! status: ${response.status}`);
      }
      console.log("Todo added");
      return response.json();
    })
    .catch((error) => {
      // Handles network failures OR the error thrown above
      console.error("Error:", error);
    });
});

```

### How it Works

* **The `.ok` Property:** Unlike other libraries (like Axios), `fetch()` **does not** reject the promise on HTTP error states (like 404 or 500). It only rejects on true network failures (like DNS issues or no internet). We must manually check `response.ok` to catch server-side issues.
* **Throwing Errors:** We use `.then` to check if the response is OK—if not, we `throw` an error with the status code.
* **The `.catch` Block:** This acts as a safety net. It handles any fetch errors—whether it's a total network collapse or the custom error we threw manually—and logs them to the console.

### Common HTTP Status Codes

Proper error handling ensures issues are caught and communicated effectively. HTTP status codes play a key role here, as each one has a specific meaning and requires a different response.

| Code | Status | Meaning |
| --- | --- | --- |
| **200** | OK | The request was successful. |
| **201** | Created | The request was successful and a resource was created. |
| **400** | Bad Request | The server cannot process the request (e.g., malformed syntax). |
| **401** | Unauthorized | Authentication is required and has failed or hasn't been provided. |
| **404** | Not Found | The requested resource could not be found. |
| **500** | Internal Server Error | The server encountered an unexpected condition. |
