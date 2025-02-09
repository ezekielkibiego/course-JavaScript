# Introduction to the DOM

## 1. What is the DOM?

The Document Object Model (DOM) is a programming interface for web documents. It represents the structure of an HTML or XML document as a tree of objects that JavaScript can manipulate.

### Key Points about the DOM:
- The DOM is a tree-like structure that represents the elements of a web page.
- It allows dynamic manipulation of HTML and CSS using JavaScript.
- The DOM provides methods and properties to access, modify, delete, or add elements.
- It is not part of JavaScript; it is provided by web browsers to enable JavaScript to interact with webpages.

### Example:
Consider the following simple HTML document:

```html
<!DOCTYPE html>
<html>
    <head>
        <title>DOM Example</title>
    </head>
    <body>
        <h1>Hello, World!</h1>
        <p>This is a paragraph.</p>
    </body>
</html>
```

The DOM representation of this document is a tree structure, where each HTML element is represented as an object that can be accessed and manipulated.

## Understanding the DOM Tree (Document, Elements, Nodes, Attributes, Text)

The DOM represents an HTML or XML document as a tree of nodes. The key components of the DOM tree are:

- **Document** – The root node of the DOM tree (represents the whole page).
- **Elements** – HTML tags (e.g., `<html>`, `<head>`, `<body>`, `<h1>`).
- **Attributes** – Properties of elements (e.g., class, id, src).
- **Text Nodes** – The text inside elements (e.g., "Hello, World!").

### DOM Tree Structure for the Above HTML:

```plaintext
Document
 ├── <html>
 │    ├── <head>
 │    │    ├── <title> → "DOM Example"
 │    ├── <body>
 │         ├── <h1> → "Hello, World!"
 │         ├── <p> → "This is a paragraph."
```

Each part of the HTML document is represented as a node in the DOM tree.

### Types of Nodes in the DOM:

| Node Type       | Description                                      |
|-----------------|--------------------------------------------------|
| Document Node   | The root of the DOM tree (document).             |
| Element Node    | Represents HTML tags like `<div>`, `<p>`, `<h1>`.|
| Attribute Node  | Represents attributes like class, id, href.      |
| Text Node       | Represents text inside an element.               |

## How the DOM Represents HTML and XML Documents

### DOM for HTML Documents

The DOM for an HTML document allows JavaScript to:
- Modify elements (`document.getElementById("id")`).
- Change styles (`element.style.color = "red"`).
- Handle events (`element.addEventListener("click", function() {...})`).

### DOM for XML Documents

The DOM also represents XML documents similarly. Example XML:

```xml
<bookstore>
    <book>
        <title>JavaScript Basics</title>
        <author>John Doe</author>
    </book>
</bookstore>
```

The DOM tree for this XML follows the same structure:

```plaintext
Document
 ├── <bookstore>
            ├── <book>
                     ├── <title> → "JavaScript Basics"
                     ├── <author> → "John Doe"
```

JavaScript can interact with XML just like HTML, but it requires XML DOM parsers to manipulate XML data.

## DOM vs. BOM (Browser Object Model)

| Feature        | DOM (Document Object Model)                           | BOM (Browser Object Model)                           |
|----------------|-------------------------------------------------------|------------------------------------------------------|
| Definition     | Represents the structure of an HTML/XML document as a tree of objects. | Represents browser-specific objects (window, navigator, location, history). |
| Access         | Accessed using document object.                       | Accessed using window object.                        |
| Example Objects| document, element, attribute, text node.              | window, navigator, location, history.                |
| Purpose        | Allows manipulation of the webpage structure and content. | Allows interaction with browser features.            |

### Example Differences:

#### DOM Example (Manipulating HTML Content)

```javascript
document.getElementById("myTitle").textContent = "New Title!";
```

#### BOM Example (Navigating to a New Page)

```javascript
window.location.href = "https://example.com";
```



## 2. Selecting Elements from the DOM

One of the most important tasks when working with the DOM is selecting elements so that you can manipulate them. JavaScript provides multiple ways to select elements from the DOM, each with different use cases.

### Using Selectors

JavaScript provides the following methods for selecting elements:

- `document.getElementById("id")`
- `document.getElementsByClassName("class")`
- `document.getElementsByTagName("tag")`
- `document.querySelector("selector")`
- `document.querySelectorAll("selector")`

#### 1. Selecting by ID: `document.getElementById("id")`

The `getElementById` method is used to select a single element by its id. Since id is unique in an HTML document, this method always returns a single element (or null if not found).

**Example:**

```html
<h1 id="title">Hello, World!</h1>
<button onclick="changeText()">Click Me</button>

<script>
    function changeText() {
        let heading = document.getElementById("title");
        heading.textContent = "Text Changed!";
    }
</script>
```

**Explanation:**

- The `getElementById("title")` selects the `<h1>` element with the ID "title".
- When the button is clicked, the text inside `<h1>` changes to "Text Changed!".

#### 2. Selecting by Class: `document.getElementsByClassName("class")`

The `getElementsByClassName` method selects all elements with a specific class name. It returns a collection (HTMLCollection), which is similar to an array but does not support array methods like `.forEach()`.

**Example:**

```html
<p class="message">First paragraph</p>
<p class="message">Second paragraph</p>
<button onclick="changeColor()">Change Color</button>

<script>
    function changeColor() {
        let elements = document.getElementsByClassName("message");
        for (let i = 0; i < elements.length; i++) {
            elements[i].style.color = "blue";
        }
    }
</script>
```

**Explanation:**

- `getElementsByClassName("message")` selects all elements with the class "message".
- Since it returns an HTMLCollection, we loop through it using `for` to change the text color of each paragraph to blue.

#### 3. Selecting by Tag Name: `document.getElementsByTagName("tag")`

The `getElementsByTagName` method selects all elements with the given tag name (e.g., `<p>`, `<div>`, `<h1>`). It returns an HTMLCollection (similar to `getElementsByClassName`).

**Example:**

```html
<ul>
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>
<button onclick="makeBold()">Make Bold</button>

<script>
    function makeBold() {
        let items = document.getElementsByTagName("li");
        for (let i = 0; i < items.length; i++) {
            items[i].style.fontWeight = "bold";
        }
    }
</script>
```

**Explanation:**

- `getElementsByTagName("li")` selects all `<li>` elements in the document.
- The `for` loop makes each `<li>` item bold when the button is clicked.

#### 4. Selecting with CSS Selectors: `document.querySelector("selector")`

The `querySelector` method selects the first matching element based on a CSS selector (e.g., `#id`, `.class`, `tag`).

**Example:**

```html
<p class="info">First paragraph</p>
<p class="info">Second paragraph</p>
<button onclick="highlight()">Highlight First</button>

<script>
    function highlight() {
        let firstParagraph = document.querySelector(".info");
        firstParagraph.style.backgroundColor = "yellow";
    }
</script>
```

**Explanation:**

- `document.querySelector(".info")` selects only the first `<p>` with class "info".
- The first paragraph gets a yellow background when the button is clicked.

Use `querySelector` when you only need the first match!

#### 5. Selecting Multiple Elements: `document.querySelectorAll("selector")`

The `querySelectorAll` method selects all matching elements based on a CSS selector. It returns a NodeList, which is similar to an array and supports `.forEach()`.

**Example:**

```html
<p class="info">First paragraph</p>
<p class="info">Second paragraph</p>
<button onclick="underlineText()">Underline All</button>

<script>
    function underlineText() {
        let paragraphs = document.querySelectorAll(".info");
        paragraphs.forEach((p) => {
            p.style.textDecoration = "underline";
        });
    }
</script>
```

**Explanation:**

- `querySelectorAll(".info")` selects all `<p>` elements with class "info".
- The `.forEach()` method loops through each paragraph and underlines the text.

Use `querySelectorAll` when you need multiple elements!

### Comparison of Selection Methods

| Method                        | Returns                     | Selects                                      |
|-------------------------------|-----------------------------|----------------------------------------------|
| `getElementById("id")`        | Single element (or null)    | An element by ID                             |
| `getElementsByClassName("class")` | HTMLCollection            | All elements with a class                    |
| `getElementsByTagName("tag")` | HTMLCollection              | All elements with a tag name                 |
| `querySelector("selector")`   | Single element (first match)| Any element using a CSS selector             |
| `querySelectorAll("selector")`| NodeList (all matches)      | Multiple elements using a CSS selector       |

### Best Practices

✔ Use `getElementById` when selecting a single unique element (fastest method).  
✔ Use `querySelector` if selecting a single element using a CSS selector.  
✔ Use `querySelectorAll` when selecting multiple elements (better than `getElementsByClassName`).  
✔ Avoid `getElementsByClassName` and `getElementsByTagName` unless you need older browser support.

### Conclusion

- `getElementById("id")` → Selects one element by ID.
- `getElementsByClassName("class")` → Selects multiple elements by class.
- `getElementsByTagName("tag")` → Selects multiple elements by tag.
- `querySelector("selector")` → Selects one element using a CSS selector.
- `querySelectorAll("selector")` → Selects multiple elements using a CSS selector.

## 3. Modifying and Manipulating Elements in the DOM

After selecting elements, you can modify them by changing their content, attributes, styles, or classes. Below, we will explore different ways to modify and manipulate DOM elements with examples.

### 1. Changing Content & Attributes

#### Changing Content: `innerHTML` vs. `textContent` vs. `innerText`

These three properties allow us to modify the content inside an element, but they behave differently.

- **`element.innerHTML`**
    - Gets or sets HTML content inside an element.
    - Can be used to insert HTML elements inside an element.

    **Example:**

    ```html
    <div id="content">Hello, <strong>World!</strong></div>
    <button onclick="changeHTML()">Change HTML</button>

    <script>
        function changeHTML() {
            let div = document.getElementById("content");
            div.innerHTML = "New <em>HTML</em> Content!";
        }
    </script>
    ```

- **`element.textContent`**
    - Gets or sets text content (ignores HTML formatting).
    - Useful for security, as it prevents script injection.

    **Example:**

    ```html
    <div id="text">Hello, <strong>World!</strong></div>
    <button onclick="changeText()">Change Text</button>

    <script>
        function changeText() {
            let div = document.getElementById("text");
            div.textContent = "New <em>Text</em> Content!";
        }
    </script>
    ```

- **`element.innerText`**
    - Similar to `textContent`, but it considers hidden elements (it only retrieves visible text).

    **Example:**

    ```html
    <p id="textExample">Hello <span style="display: none;">Hidden</span> World!</p>
    <button onclick="showInnerText()">Show innerText</button>

    <script>
        function showInnerText() {
            let text = document.getElementById("textExample").innerText;
            alert(text); // Output: "Hello World!" (ignores hidden span)
        }
    </script>
    ```

#### Changing Attributes

You can modify an element’s attributes dynamically using JavaScript.

- **Setting an Attribute: `element.setAttribute("attribute", "value")`**

    **Example:**

    ```html
    <img id="logo" src="old-logo.png" width="100">
    <button onclick="changeImage()">Change Image</button>

    <script>
        function changeImage() {
            let img = document.getElementById("logo");
            img.setAttribute("src", "new-logo.png");
            img.setAttribute("alt", "New Logo");
        }
    </script>
    ```

- **Getting an Attribute: `element.getAttribute("attribute")`**

    **Example:**

    ```html
    <img id="profile-pic" src="avatar.jpg" alt="User Avatar">
    <button onclick="showAltText()">Get Alt Text</button>

    <script>
        function showAltText() {
            let img = document.getElementById("profile-pic");
            alert(img.getAttribute("alt")); // Shows "User Avatar"
        }
    </script>
    ```

- **Removing an Attribute: `element.removeAttribute("attribute")`**

    **Example:**

    ```html
    <input type="text" id="username" required>
    <button onclick="removeRequired()">Remove Required</button>

    <script>
        function removeRequired() {
            let input = document.getElementById("username");
            input.removeAttribute("required");
        }
    </script>
    ```

### 2. Modifying Styles

You can change the CSS styles of an element dynamically using JavaScript.

- **Changing a Style Property: `element.style.property = "value"`**

    **Example:**

    ```html
    <p id="textStyle">Change my color!</p>
    <button onclick="changeColor()">Change Color</button>

    <script>
        function changeColor() {
            let text = document.getElementById("textStyle");
            text.style.color = "red";
            text.style.fontSize = "20px";
        }
    </script>
    ```

### 3. Adding and Removing Classes with `classList`

Instead of modifying styles directly, it's best practice to add or remove CSS classes.

- **Adding a Class: `element.classList.add("class")`**

    **Example:**

    ```html
    <p id="highlightText">Highlight me!</p>
    <button onclick="addHighlight()">Add Highlight</button>

    <style>
        .highlight {
            background-color: yellow;
        }
    </style>

    <script>
        function addHighlight() {
            let text = document.getElementById("highlightText");
            text.classList.add("highlight");
        }
    </script>
    ```

- **Removing a Class: `element.classList.remove("class")`**

    **Example:**

    ```html
    <p id="removableText" class="highlight">Remove my highlight!</p>
    <button onclick="removeHighlight()">Remove Highlight</button>

    <script>
        function removeHighlight() {
            let text = document.getElementById("removableText");
            text.classList.remove("highlight");
        }
    </script>
    ```

- **Toggling a Class: `element.classList.toggle("class")`**

    **Example:**

    ```html
    <p id="toggleText">Click to toggle color</p>
    <button onclick="toggleHighlight()">Toggle Highlight</button>

    <script>
        function toggleHighlight() {
            let text = document.getElementById("toggleText");
            text.classList.toggle("highlight");
        }
    </script>
    ```

- **Checking if a Class Exists: `element.classList.contains("class")`**

    **Example:**

    ```html
    <p id="checkText" class="highlight">Am I highlighted?</p>
    <button onclick="checkHighlight()">Check Highlight</button>

    <script>
        function checkHighlight() {
            let text = document.getElementById("checkText");
            alert(text.classList.contains("highlight")); // true or false
        }
    </script>
    ```

### Summary Table

| Method                | Description                                      | Example                                |
|-----------------------|--------------------------------------------------|----------------------------------------|
| `innerHTML`           | Changes HTML content inside an element           | `element.innerHTML = "<b>New Content</b>";` |
| `textContent`         | Changes text content (ignores HTML formatting)   | `element.textContent = "Plain Text";`  |
| `innerText`           | Changes visible text only (ignores hidden elements) | `element.innerText = "Visible Text";`  |
| `setAttribute`        | Sets an attribute                                | `element.setAttribute("src", "image.jpg");` |
| `getAttribute`        | Gets an attribute                                | `element.getAttribute("alt");`         |
| `removeAttribute`     | Removes an attribute                             | `element.removeAttribute("disabled");` |
| `style.property`      | Changes a style property                         | `element.style.color = "red";`         |
| `classList.add`       | Adds a class                                     | `element.classList.add("highlight");`  |
| `classList.remove`    | Removes a class                                  | `element.classList.remove("highlight");` |
| `classList.toggle`    | Toggles a class                                  | `element.classList.toggle("hidden");`  |
| `classList.contains`  | Checks if a class exists                         | `element.classList.contains("active");` |

### Conclusion

- You can change content using `innerHTML`, `textContent`, or `innerText`.
- Modify attributes with `setAttribute`, `getAttribute`, and `removeAttribute`.
- Adjust styles with `element.style.property`.
- Use `classList` for adding, removing, or toggling CSS classes.


## 4. Creating and Removing Elements in the DOM

The DOM allows us to dynamically create, insert, remove, and replace elements using JavaScript. Below, we explore various methods for working with elements and text nodes.

### 1. Creating Elements

#### `document.createElement("tag")`

This method creates a new element but does not add it to the DOM until we append it somewhere.

Example:

```html
<button onclick="createDiv()">Create a Div</button>
<div id="container"></div>

<script>
    function createDiv() {
        let newDiv = document.createElement("div"); // Create a new div
        newDiv.textContent = "Hello, I am a new div!";
        newDiv.style.backgroundColor = "lightblue";
        newDiv.style.padding = "10px";

        let container = document.getElementById("container");
        container.appendChild(newDiv); // Append to the container
    }
</script>
```

🔹 When the button is clicked, a new `<div>` is created and added inside `#container`.

#### `document.createTextNode("text")`

This creates a text node that can be inserted into an element.

Example:

```html
<button onclick="createText()">Create Text</button>
<p id="text-container"></p>

<script>
    function createText() {
        let textNode = document.createTextNode("This is a text node.");
        
        let paragraph = document.getElementById("text-container");
        paragraph.appendChild(textNode); // Append text inside paragraph
    }
</script>
```

🔹 This adds text inside the `<p>` without using `innerHTML` (which is safer to prevent script injections).

### 2. Inserting Elements

#### `element.appendChild(childElement)`

Adds a new child at the end of the parent element.

Example:

```html
<ul id="list">
    <li>Item 1</li>
</ul>
<button onclick="addListItem()">Add Item</button>

<script>
    function addListItem() {
        let newItem = document.createElement("li");
        newItem.textContent = "New Item";
        
        let list = document.getElementById("list");
        list.appendChild(newItem); // Add new item at the end
    }
</script>
```

🔹 Clicking the button adds a new list item at the bottom of the list.

#### `element.insertBefore(newElement, referenceElement)`

Inserts a new element before another element inside a parent.

Example:

```html
<ul id="ordered-list">
    <li id="first-item">First Item</li>
</ul>
<button onclick="insertBeforeFirst()">Insert Before First</button>

<script>
    function insertBeforeFirst() {
        let newItem = document.createElement("li");
        newItem.textContent = "Inserted Before First Item";

        let list = document.getElementById("ordered-list");
        let firstItem = document.getElementById("first-item");

        list.insertBefore(newItem, firstItem); // Insert before first item
    }
</script>
```

🔹 The new item will be added above "First Item."

### 3. Removing Elements

#### `element.removeChild(childElement)`

Removes a specific child element from its parent.

Example:

```html
<ul id="removable-list">
    <li id="remove-me">Remove me</li>
</ul>
<button onclick="removeItem()">Remove Item</button>

<script>
    function removeItem() {
        let list = document.getElementById("removable-list");
        let item = document.getElementById("remove-me");

        if (item) {
            list.removeChild(item); // Remove the item
        }
    }
</script>
```

🔹 Clicking the button removes the `<li>` with "Remove me".

### 4. Replacing Elements

#### `element.replaceChild(newElement, oldElement)`

Replaces an existing child element with a new one.

Example:

```html
<p id="replace-me">I will be replaced!</p>
<button onclick="replaceElement()">Replace Element</button>

<script>
    function replaceElement() {
        let newPara = document.createElement("p");
        newPara.textContent = "I replaced the old paragraph!";

        let container = document.body;
        let oldPara = document.getElementById("replace-me");

        container.replaceChild(newPara, oldPara); // Replace old with new
    }
</script>
```

🔹 The old paragraph will be removed and replaced with the new one.

### 5. Clearing Content

#### `element.innerHTML = ""`

Removes all inner content from an element.

Example:

```html
<div id="clear-container">
    <p>This will be removed.</p>
    <p>And this too!</p>
</div>
<button onclick="clearContent()">Clear Content</button>

<script>
    function clearContent() {
        document.getElementById("clear-container").innerHTML = ""; // Remove all child elements
    }
</script>
```

🔹 Clicking the button removes all paragraphs inside `#clear-container`.

### Summary Table

| Method                                      | Description                          | Example                                |
|---------------------------------------------|--------------------------------------|----------------------------------------|
| `document.createElement("tag")`             | Creates an element                   | `document.createElement("div");`       |
| `document.createTextNode("text")`           | Creates a text node                  | `document.createTextNode("Hello!");`   |
| `element.appendChild(childElement)`         | Adds a child at the end              | `parent.appendChild(child);`           |
| `element.insertBefore(newElement, referenceElement)` | Inserts an element before another    | `parent.insertBefore(newEl, refEl);`   |
| `element.removeChild(childElement)`         | Removes a child element              | `parent.removeChild(child);`           |
| `element.replaceChild(newElement, oldElement)` | Replaces a child element             | `parent.replaceChild(newEl, oldEl);`   |
| `element.innerHTML = ""`                    | Clears all child elements            | `parent.innerHTML = "";`               |

### Conclusion

- Use `createElement` and `createTextNode` to dynamically create elements.
- Use `appendChild` and `insertBefore` to add elements to the DOM.
- Use `removeChild` and `replaceChild` to modify existing elements.
- Use `innerHTML = ""` to quickly clear all content from an element.

## 5. DOM Events and Event Handling

The DOM allows us to interact with elements through events like clicks, key presses, and mouse movements. JavaScript provides methods to listen for and handle these events efficiently.

### 1. Understanding Events

#### What is an Event?

An event is an action that occurs in the browser, such as a user clicking a button, submitting a form, or pressing a key. Events help make web pages interactive.

#### Common DOM Events

| Event Type | Description                         |
|------------|-------------------------------------|
| click      | Fires when an element is clicked    |
| mouseover  | Fires when the mouse enters an element |
| mouseout   | Fires when the mouse leaves an element |
| keydown    | Fires when a key is pressed         |
| keyup      | Fires when a key is released        |
| load       | Fires when the page finishes loading |
| submit     | Fires when a form is submitted      |

### 1. Click 


Example: Listening for a click event

```html
<button id="btn">Click Me</button>
<p id="message"></p>

<script>
    document.getElementById("btn").addEventListener("click", function() {
        document.getElementById("message").textContent = "Button clicked!";
    });
</script>
```

🔹 When the button is clicked, the text "Button clicked!" appears.

### 2. mouseover - Fires when the mouse enters an element

The mouseover event occurs when the mouse pointer enters an element.

Example: Change Background on Hover

```html
<div id="hoverBox" style="width: 150px; height: 100px; background: lightblue; text-align: center; padding: 20px;">
    Hover over me
</div>

<script>
    document.getElementById("hoverBox").addEventListener("mouseover", function() {
        this.style.backgroundColor = "lightcoral";
    });
</script>
```

🔹 Hovering over the box changes its background color.

### 3. mouseout - Fires when the mouse leaves an element

The mouseout event occurs when the mouse moves away from an element.

Example: Reset Background on Mouse Leave

```html
<div id="hoverBox2" style="width: 150px; height: 100px; background: lightblue; text-align: center; padding: 20px;">
    Hover over me
</div>

<script>
    let box = document.getElementById("hoverBox2");

    box.addEventListener("mouseover", function() {
        this.style.backgroundColor = "lightcoral";
    });

    box.addEventListener("mouseout", function() {
        this.style.backgroundColor = "lightblue";
    });
</script>
```

🔹 The background changes to red when hovering and resets to blue when the mouse leaves.

### 4. keydown - Fires when a key is pressed

The keydown event is triggered when a key is pressed down.

Example: Detect Key Press

```html
<input type="text" id="keyInput" placeholder="Type something..." />
<p id="keyMessage"></p>

<script>
    document.getElementById("keyInput").addEventListener("keydown", function(event) {
        document.getElementById("keyMessage").textContent = `You pressed: ${event.key}`;
    });
</script>
```

🔹 Typing in the input field displays the pressed key.

### 5. keyup - Fires when a key is released

The keyup event is triggered when a pressed key is released.

Example: Detect Key Release

```html
<input type="text" id="keyupInput" placeholder="Type and release a key" />
<p id="keyupMessage"></p>

<script>
    document.getElementById("keyupInput").addEventListener("keyup", function(event) {
        document.getElementById("keyupMessage").textContent = `Key released: ${event.key}`;
    });
</script>
```

🔹 The last released key is displayed in the paragraph.

### 6. load - Fires when the page finishes loading

The load event ensures all resources (images, scripts, etc.) are fully loaded before executing code.

Example: Show an Alert When Page Loads

```html
<script>
    window.addEventListener("load", function() {
        alert("Page has fully loaded!");
    });
</script>
```

🔹 The alert appears once the page loads completely.

### 7. submit - Fires when a form is submitted

The submit event is used to handle form submissions.

Example: Validate Form Before Submission

```html
<form id="myForm">
    <input type="text" id="nameInput" placeholder="Enter your name" required />
    <button type="submit">Submit</button>
</form>
<p id="formMessage"></p>

<script>
    document.getElementById("myForm").addEventListener("submit", function(event) {
        event.preventDefault(); // Prevents form from actually submitting
        let name = document.getElementById("nameInput").value;
        if (name.trim() === "") {
            document.getElementById("formMessage").textContent = "Please enter a valid name!";
        } else {
            document.getElementById("formMessage").textContent = `Form submitted with name: ${name}`;
        }
    });
</script>
```

🔹 The form submission is prevented unless the user enters a name.

### 2. Event Propagation: Bubbling vs. Capturing

#### Event Bubbling (Default Behavior)

Events start from the target element and bubble up to parent elements.

Example: Bubbling

```html
<div id="parent" style="padding: 20px; background: lightblue;">
    <button id="child">Click Me</button>
</div>

<script>
    document.getElementById("parent").addEventListener("click", function() {
        alert("Parent clicked!");
    });

    document.getElementById("child").addEventListener("click", function(event) {
        alert("Child clicked!");
    });
</script>
```

🔹 Clicking the button triggers both event listeners (child first, then parent).

#### Stopping Bubbling with `event.stopPropagation()`

```javascript
document.getElementById("child").addEventListener("click", function(event) {
    alert("Child clicked!");
    event.stopPropagation(); // Prevents parent from being triggered
});
```

🔹 Now, clicking the button only triggers the child event.

#### Event Capturing (Use `true` in `addEventListener`)

Events start from the top (document) and go down to the target.

Ex## Conclusion

- The DOM is a structured representation of a webpage that JavaScript can manipulate.
- The DOM tree consists of elements, attributes, and text nodes.
- The DOM can represent both HTML and XML documents.
- The DOM is different from the BOM, which deals with browser-related objects like window and navigator.ample: Capturing

```javascript
document.getElementById("parent").addEventListener("click", function() {
    alert("Parent clicked!");
}, true);
```

🔹 The parent event fires before the child when `true` is passed.

### 3. Event Delegation

Instead of adding event listeners to multiple child elements, we add a single listener to a parent and detect the target.

Example: Using `event.target` for Delegation

```html
<ul id="list">
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>

<script>
    document.getElementById("list").addEventListener("click", function(event) {
        if (event.target.tagName === "LI") {
            alert("You clicked on: " + event.target.textContent);
        }
    });
</script>
```

🔹 This method works even for dynamically added list items!

### 4. Adding Event Listeners

`element.addEventListener("event", callbackFunction)`

This is the recommended way to attach event listeners.

Example: click event listener

```html
<button id="myButton">Click Me</button>

<script>
    document.getElementById("myButton").addEventListener("click", function() {
        alert("Button was clicked!");
    });
</script>
```

### 5. Removing Event Listeners

`element.removeEventListener("event", callbackFunction)`

To remove an event, the function reference must be the same as the one added.

Example: Removing an event listener

```html
<button id="toggleBtn">Click Me</button>

<script>
    function handleClick() {
        alert("Button clicked!");
    }

    let button = document.getElementById("toggleBtn");
    button.addEventListener("click", handleClick);

    setTimeout(() => {
        button.removeEventListener("click", handleClick);
        alert("Event listener removed!");
    }, 5000); // Removes after 5 seconds
</script>
```

🔹 Clicking the button works for 5 seconds before the listener is removed.

### 6. Passing Parameters to Event Handlers

#### Using an Arrow Function to Pass Arguments

Example: Passing custom parameters

```html
<button id="btnPass">Click Me</button>

<script>
    function showMessage(name) {
        alert("Hello, " + name);
    }

    document.getElementById("btnPass").addEventListener("click", () => showMessage("Alice"));
</script>
```

🔹 The function `showMessage("Alice")` is called when the button is clicked.

#### Using `bind()` to Pass Parameters

Example: Using `bind()`

```html
<button id="btnBind">Click Me</button>

<script>
    function greet(name) {
        alert("Hello, " + name);
    }

    document.getElementById("btnBind").addEventListener("click", greet.bind(null, "Bob"));
</script>
```

🔹 `bind(null, "Bob")` pre-fills the argument "Bob".

### Summary Table

| Feature                | Description                          | Example                                |
|------------------------|--------------------------------------|----------------------------------------|
| `addEventListener`     | Adds an event listener               | `el.addEventListener("click", handler)`|
| `removeEventListener`  | Removes an event listener            | `el.removeEventListener("click", handler)`|
| `event.stopPropagation()` | Stops event bubbling              | `event.stopPropagation()`              |
| `event.target`         | Identifies the clicked element       | `event.target.tagName`                 |
| `bind()`               | Passes arguments to event handlers   | `handler.bind(null, arg)`              |

### Conclusion

- Use `addEventListener` for better event management.
- Use event delegation to handle multiple child elements efficiently.
- Understand bubbling vs. capturing to control event flow.
- Remove event listeners when they are no longer needed for better performance.

## 6. Working with Forms and Inputs

### 1️⃣ Getting Form Values

You can retrieve user input from different form elements using:

- `input.value` for text fields
- `select.value` for dropdowns
- `checkbox.checked` for checkboxes

Example: Getting Values from Input, Select, and Checkbox

```html
<form id="userForm">
    <label for="username">Name:</label>
    <input type="text" id="username" placeholder="Enter name" />

    <label for="userRole">Role:</label>
    <select id="userRole">
        <option value="admin">Admin</option>
        <option value="editor">Editor</option>
    </select>

    <label>
        <input type="checkbox" id="terms" />
        Accept Terms
    </label>

    <button type="submit">Submit</button>
</form>

<p id="output"></p>

<script>
    document.getElementById("userForm").addEventListener("submit", function(event) {
        event.preventDefault(); // Prevent form from refreshing

        let name = document.getElementById("username").value;
        let role = document.getElementById("userRole").value;
        let termsAccepted = document.getElementById("terms").checked;

        document.getElementById("output").textContent = 
            `Name: ${name}, Role: ${role}, Terms Accepted: ${termsAccepted}`;
    });
</script>
```

🔹 How it works?
- The submit event triggers when the button is clicked.
- `event.preventDefault()` stops the default form submission.
- We retrieve the values using `.value` for inputs and `.checked` for checkboxes.
- The output is displayed inside the `<p>` tag.

### 2️⃣ Validating User Input

Validation ensures correct data entry before submission.

Example: Checking for Empty Input Fields

```html
<form id="validateForm">
    <label for="userInput">Enter your name:</label>
    <input type="text" id="userInput" placeholder="Enter your name" required />
    <button type="submit">Submit</button>
</form>

<p id="validationMessage"></p>

<script>
    document.getElementById("validateForm").addEventListener("submit", function(event) {
        let input = document.getElementById("userInput").value;
        
        if (input.trim() === "") {
            event.preventDefault();
            document.getElementById("validationMessage").textContent = "⚠️ Name is required!";
        } else {
            document.getElementById("validationMessage").textContent = "";
        }
    });
</script>
```

🔹 How it works?
- If the input field is empty, `event.preventDefault()` stops submission.
- A warning message appears instead of proceeding.

### 3️⃣ Handling Form Submission

Use `onsubmit` to prevent submission and process form data.

Example: Preventing Default Form Submission

```html
<form id="customForm">
    <label for="email">Email:</label>
    <input type="email" id="email" placeholder="Enter your email" required />
    <button type="submit">Submit</button>
</form>

<script>
    document.getElementById("customForm").addEventListener("submit", function(event) {
        event.preventDefault(); // Prevent actual form submission
        let email = document.getElementById("email").value;
        alert("Form Submitted Successfully!\nEmail: " + email);
    });
</script>
```

🔹 How it works?
- `event.preventDefault()` stops the default page reload.
- The form processes data and displays an alert.

### Summary

- **Getting values:** Use `.value` for text fields, `.checked` for checkboxes.
- **Validation:** Ensure fields are not empty before submission.

## 7. Traversing the DOM (Navigating Elements)

DOM Traversal allows you to move between elements dynamically. Here’s how to navigate using different properties:

### 1️⃣ parentElement (Getting the Parent of an Element)

The `parentElement` property returns the parent node of an element.

Example: Finding the Parent of an Element

```html
<div id="container">
    <p id="child">This is a paragraph.</p>
</div>

<script>
    let childElement = document.getElementById("child");
    let parent = childElement.parentElement;
    console.log(parent); // Logs: <div id="container">...</div>
</script>
```

🔹 How it works?
- The paragraph (`<p>`) is a child of `div#container`.
- `parentElement` returns the `div` containing the paragraph.

### 2️⃣ children (Getting All Child Elements of a Parent)

The `children` property returns all direct child elements (not text or comment nodes).

Example: Getting All Children of a Parent Element

```html
<ul id="list">
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>

<script>
    let list = document.getElementById("list");
    let children = list.children;

    console.log(children); // Logs: HTMLCollection(3) [li, li, li]
    console.log(children[0].textContent); // Logs: "Item 1"
</script>
```

🔹 How it works?
- `children` gets all `<li>` elements inside `<ul>`.
- It returns an HTMLCollection that behaves like an array.

### 3️⃣ firstChild & lastChild vs. firstElementChild & lastElementChild

- `firstChild` & `lastChild` include text nodes (like spaces).
- `firstElementChild` & `lastElementChild` only return element nodes.

Example: Using `firstChild` vs. `firstElementChild`

```html
<div id="box">
    <p>First paragraph</p>
    <p>Second paragraph</p>
</div>

<script>
    let box = document.getElementById("box");

    console.log(box.firstChild); // Logs: Text node (whitespace)
    console.log(box.firstElementChild); // Logs: <p>First paragraph</p>
</script>
```

🔹 How it works?
- `firstChild` may return whitespace as a text node.
- `firstElementChild` ensures an HTML element is returned.

Example: Using `lastElementChild`

```html
<div id="box">
    <p>First paragraph</p>
    <p>Last paragraph</p>
</div>

<script>
    let box = document.getElementById("box");
    console.log(box.lastElementChild.textContent); // Logs: "Last paragraph"
</script>
```

### 4️⃣ nextElementSibling & previousElementSibling (Navigating Siblings)

- `nextElementSibling` → Gets the next sibling element.
- `previousElementSibling` → Gets the previous sibling element.

Example: Getting Next and Previous Sibling Elements

```html
<ul>
    <li id="first">First Item</li>
    <li id="second">Second Item</li>
    <li id="third">Third Item</li>
</ul>

<script>
    let secondItem = document.getElementById("second");

    console.log(secondItem.previousElementSibling.textContent); // Logs: "First Item"
    console.log(secondItem.nextElementSibling.textContent); // Logs: "Third Item"
</script>
```

🔹 How it works?
- `previousElementSibling` gets the `<li>` before the second item.
- `nextElementSibling` gets the `<li>` after the second item.

### 5️⃣ nodeType & nodeName (Checking Node Information)

- `nodeType` returns a numeric code (1 = Element, 3 = Text, etc.).
- `nodeName` returns the name of the node (e.g., DIV, P, TEXT).
Example: Checking `nodeType` and `nodeName`

```html
<p id="paragraph">Hello, World!</p>

<script>
    let para = document.getElementById("paragraph");

    console.log(para.nodeType); // Logs: 1 (Element Node)
    console.log(para.nodeName); // Logs: "P"
</script>
```

Example: Checking `nodeType` for a Text Node

```html
<div id="container">
    Hello!
</div>

<script>
    let container = document.getElementById("container");
    let textNode = container.firstChild;

    console.log(textNode.nodeType); // Logs: 3 (Text Node)
    console.log(textNode.nodeName); // Logs: "#text"
</script>
```

🔹 How it works?
- `nodeType = 1` means it's an Element Node.
- `nodeType = 3` means it's a Text Node (whitespace or text content).

###  Summary

| Property                        | Description                                 |
|---------------------------------|---------------------------------------------|
| `parentElement`                 | Gets the parent of an element               |
| `children`                      | Gets all child elements (not text nodes)    |
| `firstChild`, `lastChild`       | Gets the first/last node (including text)   |
| `firstElementChild`, `lastElementChild` | Gets the first/last element (ignoring text) |
| `nextElementSibling`, `previousElementSibling` | Gets the next/previous element |
| `nodeType`                      | Returns type of node (1 = element, 3 = text)|
| `nodeName`                      | Returns the name of the node (e.g., DIV, P) |

## 8. Working with Attributes & Data Attributes

Attributes store extra information about an element. The DOM allows you to get, set, and remove attributes dynamically.

### 1️⃣ getAttribute("attribute") – Getting an Attribute

Retrieves the value of a specified attribute.

Example: Getting an `href` Attribute from a Link

```html
<a id="myLink" href="https://example.com">Click Here</a>

<script>
    let link = document.getElementById("myLink");
    let hrefValue = link.getAttribute("href");

    console.log(hrefValue); // Logs: "https://example.com"
</script>
```

🔹 How it works?
- The `getAttribute("href")` method gets the current `href` of the `<a>` element.

Example: Getting an `src` Attribute from an Image

```html
<img id="logo" src="logo.png" alt="Website Logo">

<script>
    let img = document.getElementById("logo");
    console.log(img.getAttribute("src")); // Logs: "logo.png"
</script>
```

### 2️⃣ setAttribute("attribute", "value") – Setting/Updating an Attribute

Used to add or modify an attribute.

Example: Changing the `href` of a Link

```html
<a id="myLink" href="https://oldsite.com">Old Site</a>

<script>
    let link = document.getElementById("myLink");
    link.setAttribute("href", "https://newsite.com");

    console.log(link.getAttribute("href")); // Logs: "https://newsite.com"
</script>
```

Example: Changing an `src` Attribute of an Image

```html
<img id="profilePic" src="default.png" alt="Profile Picture">

<script>
    let img = document.getElementById("profilePic");
    img.setAttribute("src", "new-profile.png");

    console.log(img.getAttribute("src")); // Logs: "new-profile.png"
</script>
```

Example: Adding a `title` Attribute to an Element

```html
<button id="myButton">Hover me</button>

<script>
    let button = document.getElementById("myButton");
    button.setAttribute("title", "Click to perform an action");

    console.log(button.getAttribute("title")); // Logs: "Click to perform an action"
</script>
```

### 3️⃣ removeAttribute("attribute") – Removing an Attribute

Deletes an attribute from an element.

Example: Removing the `href` from a Link

```html
<a id="myLink" href="https://example.com">Visit Site</a>

<script>
    let link = document.getElementById("myLink");
    link.removeAttribute("href");

    console.log(link.getAttribute("href")); // Logs: null (attribute removed)
</script>
```

Example: Removing the `disabled` Attribute from a Button

```html
<button id="submitButton" disabled>Submit</button>

<script>
    let button = document.getElementById("submitButton");
    button.removeAttribute("disabled");

    console.log(button.hasAttribute("disabled")); // Logs: false
</script>
```

🔹 How it works?
- `removeAttribute("disabled")` makes the button clickable again.

### 4️⃣ Using data-* Attributes (Dataset API)

Custom `data-*` attributes store extra data in HTML elements. They can be accessed using `dataset`.

Example: Getting and Setting `data-*` Attributes

```html
<button id="product" data-id="123" data-category="electronics">Buy Now</button>

<script>
    let button = document.getElementById("product");

    // Getting data-* attributes
    console.log(button.dataset.id);       // Logs: "123"
    console.log(button.dataset.category); // Logs: "electronics"

    // Modifying a data attribute
    button.dataset.id = "456";
    console.log(button.dataset.id); // Logs: "456"
</script>
```

Example: Using `data-*` Attributes in a Dynamic List

```html
<ul>
    <li data-price="10" data-name="Apple">Apple - $10</li>
    <li data-price="15" data-name="Banana">Banana - $15</li>
    <li data-price="20" data-name="Cherry">Cherry - $20</li>
</ul>

<script>
    let items = document.querySelectorAll("li");

    items.forEach(item => {
        console.log(`${item.dataset.name}: $${item.dataset.price}`);
    });

    // Logs:
    // Apple: $10
    // Banana: $15
    // Cherry: $20
</script>
```

Example: Using `data-*` Attributes in Event Listeners

```html
<button id="orderButton" data-product="Laptop" data-price="999">Order Now</button>

<script>
    let button = document.getElementById("orderButton");

    button.addEventListener("click", function () {
        alert(`You ordered a ${button.dataset.product} for $${button.dataset.price}`);
    });
</script>
```

🔹 How it works?
- When the button is clicked, it reads the `data-product` and `data-price` values and shows them in an alert.

## 9. Handling Dynamic HTML & Template Literals in JavaScript

Dynamic HTML allows you to modify and generate content on the fly. Template literals (backticks: ``) provide a cleaner way to inject variables into HTML.

### 1️⃣ Using JavaScript to Dynamically Insert HTML

You can create and insert HTML elements dynamically using `innerHTML` or `createElement()`.

#### Example 1: Using `innerHTML` to Add Content

```html
<div id="container"></div>

<script>
    let container = document.getElementById("container");
    container.innerHTML = "<h2>Welcome to Dynamic HTML!</h2><p>Content added using JavaScript.</p>";
</script>
```

#### Example 2: Using `createElement()` and `appendChild()` (Safer than `innerHTML`)

```html
<div id="container"></div>

<script>
    let container = document.getElementById("container");

    let newElement = document.createElement("h2");
    newElement.textContent = "Dynamically Created Heading";

    container.appendChild(newElement);
</script>
```

🔹 **Why use `createElement()` instead of `innerHTML`?**
- `createElement()` prevents security risks like XSS.
- `innerHTML` can overwrite existing content accidentally.

### 2️⃣ Creating Reusable UI Components with Template Literals

Template literals (``) allow you to insert variables inside HTML easily.

#### Example: Creating a User Profile Card with Template Literals

```html
<div id="profile"></div>

<script>
    let user = {
        name: "John Doe",
        age: 28,
        email: "john@example.com"
    };

    let profileCard = `
        <div class="card">
            <h2>${user.name}</h2>
            <p>Age: ${user.age}</p>
            <p>Email: ${user.email}</p>
        </div>
    `;

    document.getElementById("profile").innerHTML = profileCard;
</script>
```

🔹 **Why use template literals?**
- Cleaner syntax (No need for `+` concatenation).
- Easy to read and maintain.
- Supports multi-line strings.

#### Example: Creating a List of Items Dynamically

```html
<ul id="itemList"></ul>

<script>
    let items = ["Apple", "Banana", "Cherry"];

    let itemList = items.map(item => `<li>${item}</li>`).join("");

    document.getElementById("itemList").innerHTML = itemList;
</script>
```

### 3️⃣ Handling XSS (Cross-Site Scripting) and Avoiding `innerHTML`

**What is XSS?**
Cross-Site Scripting (XSS) happens when attackers inject malicious scripts into a website.

#### Example of XSS Attack (DO NOT USE THIS!)

```html
<input id="userInput" placeholder="Enter your name">
<button onclick="submitData()">Submit</button>
<div id="output"></div>

<script>
    function submitData() {
        let input = document.getElementById("userInput").value;
        document.getElementById("output").innerHTML = `<p>${input}</p>`; // ❌ UNSAFE!
    }
</script>
```

 **Problem?**
If a user enters `<script>alert("Hacked!")</script>`, it will execute JavaScript inside the page. ⚠️

#### Safe Way: Use `textContent` Instead of `innerHTML`

```html
<input id="userInput" placeholder="Enter your name">
<button onclick="submitData()">Submit</button>
<div id="output"></div>

<script>
    function submitData() {
        let input = document.getElementById("userInput").value;
        let output = document.getElementById("output");

        //  Securely inserting text
        let p = document.createElement("p");
        p.textContent = input;
        output.appendChild(p);
    }
</script>
```

🔹 **Why is this safe?**
- `textContent` escapes HTML, so `<script>` won't execute.
- No chance of XSS attacks.


## 10. Working with Local Storage and Session Storage

### What are Local Storage and Session Storage?

Both `localStorage` and `sessionStorage` allow you to store data persistently in the browser.

- **localStorage** → Data remains even after closing the browser.
- **sessionStorage** → Data is deleted when the session (tab) closes.

### 1️⃣ Using localStorage (Data persists after closing the browser)

Example: Storing and Retrieving Data

```html
<input type="text" id="username" placeholder="Enter your name">
<button onclick="saveData()">Save</button>
<button onclick="showData()">Show</button>
<button onclick="clearData()">Clear</button>
<p id="output"></p>

<script>
    function saveData() {
        let name = document.getElementById("username").value;
        localStorage.setItem("username", name);
        alert("Data saved in localStorage!");
    }

    function showData() {
        let name = localStorage.getItem("username");
        if (name) {
            document.getElementById("output").textContent = `Welcome, ${name}!`;
        } else {
            document.getElementById("output").textContent = "No data found!";
        }
    }

    function clearData() {
        localStorage.removeItem("username");
        document.getElementById("output").textContent = "Data cleared!";
    }
</script>
```

🔹 **How it works:**
- **Save** → Stores the input value in `localStorage`.
- **Show** → Retrieves and displays the stored value.
- **Clear** → Removes the data.

### 2️⃣ Using sessionStorage (Data disappears when the tab is closed)

Example: Storing and Retrieving Session Data

```html
<input type="text" id="email" placeholder="Enter your email">
<button onclick="saveSession()">Save</button>
<button onclick="showSession()">Show</button>
<button onclick="clearSession()">Clear</button>
<p id="sessionOutput"></p>

<script>
    function saveSession() {
        let email = document.getElementById("email").value;
        sessionStorage.setItem("email", email);
        alert("Data saved in sessionStorage!");
    }

    function showSession() {
        let email = sessionStorage.getItem("email");
        if (email) {
            document.getElementById("sessionOutput").textContent = `Your email: ${email}`;
        } else {
            document.getElementById("sessionOutput").textContent = "No session data found!";
        }
    }

    function clearSession() {
        sessionStorage.removeItem("email");
        document.getElementById("sessionOutput").textContent = "Session data cleared!";
    }
</script>
```

🔹 **How it works:**
- **Save** → Stores data only for the session (until tab is closed).
- **Show** → Retrieves session-stored data.
- **Clear** → Removes the session data.


## 11. Fetching and Manipulating External Data (APIs & AJAX)

Fetching data from external sources (APIs) is crucial for modern web applications. JavaScript provides the `fetch()` API to make network requests and retrieve data from APIs.

### 1️⃣ Fetching Data using the `fetch()` API

The `fetch()` function is used to request data from an API.

Example: Fetching data from an API (JSON Placeholder)

```javascript
fetch("https://jsonplaceholder.typicode.com/posts/1")
    .then(response => response.json()) // Convert response to JSON
    .then(data => console.log(data)) // Log the data
    .catch(error => console.error("Error fetching data:", error)); // Handle errors
```

🔹 **Explanation:**
- `fetch(url)` → Sends a GET request to the API.
- `.then(response => response.json())` → Converts the response into JSON format.
- `.then(data => console.log(data))` → Logs the API response.
- `.catch(error => console.error("Error fetching data:", error))` → Handles errors if the request fails.

### 2️⃣ Handling JSON Responses with `.json()`

APIs often return data in JSON format, which must be converted into a JavaScript object.

Example: Fetching multiple posts from an API

```javascript
fetch("https://jsonplaceholder.typicode.com/posts")
    .then(response => response.json()) // Convert response to JSON
    .then(posts => {
        posts.slice(0, 5).forEach(post => console.log(`Title: ${post.title}`));
    })
    .catch(error => console.error("Error fetching posts:", error));
```

🔹 **Explanation:**
- Fetches an array of posts from the API.
- `.slice(0, 5)` → Limits output to the first 5 posts.
- `.forEach(post => console.log(post.title))` → Loops through and logs post titles.

### 3️⃣ Displaying API Data Dynamically

Let's display API data inside an HTML element.

Example: Displaying data in the DOM

```html
<div id="post-container"></div>

<script>
    fetch("https://jsonplaceholder.typicode.com/posts/1")
        .then(response => response.json())
        .then(data => {
            document.getElementById("post-container").innerHTML = `
                <h2>${data.title}</h2>
                <p>${data.body}</p>
            `;
        })
        .catch(error => console.error("Error fetching post:", error));
</script>
```

🔹 **Explanation:**
- Retrieves a post from the API.
- Inserts the post title and body into the `post-container` div.

### 4️⃣ Handling Errors and Promises (`.then()`, `.catch()`, `async/await`)

Promises help handle asynchronous operations.

Example: Using `async/await` for cleaner syntax

```javascript
async function fetchPost() {
    try {
        let response = await fetch("https://jsonplaceholder.typicode.com/posts/1");
        if (!response.ok) throw new Error("Network response was not ok");
        let data = await response.json();
        console.log(data);
    } catch (error) {
        console.error("Error fetching post:", error);
    }
}

fetchPost();
```

🔹 **Explanation:**
- `await fetch(url)` → Waits for the response.
- `await response.json()` → Converts response to JSON.
- `if (!response.ok)` → Checks for errors.
- `catch (error)` → Catches and logs errors.

## 12. Advanced DOM Manipulations

### 1️⃣ Using `MutationObserver` to Watch for DOM Changes

`MutationObserver` allows detecting when elements are added, removed, or modified.

Example: Observing changes in a div

```html
<div id="observedDiv">Hello</div>
<button onclick="changeContent()">Change Text</button>

<script>
    let observer = new MutationObserver(mutations => {
        mutations.forEach(mutation => {
            console.log("DOM changed:", mutation);
        });
    });

    let targetNode = document.getElementById("observedDiv");
    observer.observe(targetNode, { childList: true, subtree: true });

    function changeContent() {
        targetNode.textContent = "New Content!";
    }
</script>
```

🔹 **Explanation:**
- Observes changes inside `#observedDiv`.
- Logs when text content changes.

### 2️⃣ Performance Optimizations

#### Batching Updates

Updating the DOM multiple times inside a loop is inefficient.

❌ Bad Example: Causes multiple reflows

```javascript
let list = document.getElementById("list");
for (let i = 0; i < 100; i++) {
    let li = document.createElement("li");
    li.textContent = `Item ${i}`;
    list.appendChild(li); // BAD: Updates the DOM in each iteration
}
```

Good Example: Uses Fragment to batch updates

```javascript
let list = document.getElementById("list");
let fragment = document.createDocumentFragment();

for (let i = 0; i < 100; i++) {
    let li = document.createElement("li");
    li.textContent = `Item ${i}`;
    fragment.appendChild(li);
}

list.appendChild(fragment); // GOOD: Updates the DOM once
```

🔹 **Why?**
- Reduces reflows and repaints, improving performance.

### 3️⃣ Lazy Loading Images and Content

Lazy loading defers loading images until they are visible on the screen.

Example: Lazy loading an image

```html
<img data-src="image.jpg" class="lazyload" width="300" height="200" alt="Lazy Image">
<script>
    document.addEventListener("DOMContentLoaded", function () {
        let lazyImages = document.querySelectorAll(".lazyload");
        
        lazyImages.forEach(img => {
            img.src = img.dataset.src;
        });
    });
</script>
```

🔹 **Explanation:**
- Uses `data-src` instead of `src` initially.
- Updates `src` when the page loads.

### 4️⃣ Creating a Virtual DOM for Efficient Updates

Updating a Virtual DOM before applying changes improves performance.

Example: Simple Virtual DOM

```javascript
let virtualDOM = [];

function updateVirtualDOM(newData) {
    virtualDOM.push(newData);
}

function applyUpdates() {
    let container = document.getElementById("app");
    container.innerHTML = virtualDOM.join("");
}

updateVirtualDOM("<p>Hello</p>");
updateVirtualDOM("<p>World</p>");
applyUpdates();
```

🔹 **Explanation:**
- Updates `virtualDOM` first.
- Applies all updates at once, reducing direct DOM manipulations.


