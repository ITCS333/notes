---
title: "Client Side Programming Using JavaScript"
author: "Abdulla Ebrahim Subah"
institute: "University of Bahrain"
topic: "Introduction"
theme: "CambridgeUS"
colortheme: "beaver"
fonttheme: "professionalfonts"
fontsize: 10pt
linkstyle: bold
aspectratio: 169
dpi: 300
navigation: frame
# titlegraphic: 
# logo: 
date: \today{}
lang: en-US
section-titles: false
header-includes:
  - \usepackage{setspace}
  - \setstretch{1.5}
---

# Introduction

JavaScript is a core web programming language alongside HTML and CSS, used by 99% of websites for client-side behavior.

JavaScript engines in web browsers execute client code and are also used in servers and applications, with Node.js being the most popular non-browser runtime.

Key characteristics of JavaScript:

- High-level programming language
- Follows ECMAScript standard
- Features dynamic typing
- Supports prototype-based object-orientation
- Enables multiple programming paradigms (event-driven, functional, imperative)
- Provides APIs for text, dates, regular expressions, data structures, and DOM manipulation

The language itself doesn't include I/O capabilities (networking, storage, graphics) - these are provided by browsers or runtime systems through APIs.

Note: Despite similar names and syntax, JavaScript is entirely different from Java in design and purpose.

[source](https://en.wikipedia.org/wiki/JavaScript)

# Where to Write JavaScript?

## Basic Script Tag Example
```html
<script>
document.getElementById("demo").innerHTML = "Welcome to JavaScript";
</script>
```
The code changes the content of an HTML element with id "demo" using JavaScript placed directly in the HTML file between script tags.

## JavaScript in Head Section
```html
<!DOCTYPE html>
<html>
<head>
<script>
function showMessage() {
  document.getElementById("message").innerHTML = "Text has been updated.";
}
</script>
</head>
<body>
<h2>JavaScript in Head Demo</h2>
<p id="message">Original text</p>
<button type="button" onclick="showMessage()">Click here</button>
</body>
</html>
```
Places JavaScript code in the head section. When the button is clicked, it calls the showMessage function that changes the paragraph text. Placing scripts in the head section means they load before the page content.

## JavaScript in Body Section
```html
<!DOCTYPE html>
<html>
<body>
<h2>JavaScript in Body Demo</h2>
<p id="message">Original text</p>
<button type="button" onclick="displayText()">Click here</button>
<script>
function displayText() {
  document.getElementById("message").innerHTML = "Text has been updated.";
}
</script>
</body>
</html>
```
Places JavaScript code at the bottom of the body section. This improves page load performance since the content loads before the scripts.

## External JavaScript File (myScript.js)
```javascript
function updateContent() {
  document.getElementById("message").innerHTML = "Text has been updated.";
}
```
The code is saved in a separate .js file and can be reused across multiple web pages.

## Including External JavaScript
```html
<script src="myScript.js"></script>
<script src="/scripts/myScript.js"></script>
<script src="https://www.example.com/scripts/myScript.js"></script>
```
Three different ways to include external JavaScript files: without path, with a folder path, and with a full URL. External scripts keep code organized and enable browser caching for better performance.

# Common Use Cases

## Changing HTML Content
```javascript
document.getElementById("message").innerHTML = "Welcome to Our Website";
```
This code finds an HTML element with id="message" and changes its content to the specified text. You can use either single or double quotes for the text.

## Changing HTML Element Source
```javascript
function turnOnLight() {
    document.getElementById("bulb").src = "bulbon.gif";
}

function turnOffLight() {
    document.getElementById("bulb").src = "bulboff.gif";
}
```
These functions modify an image source attribute, creating an interactive effect like switching a light bulb on and off.

## Modifying CSS Styles
```javascript
document.getElementById("textBlock").style.fontSize = "28px";
```
Changes the font size of an HTML element with id="textBlock". You can modify any CSS property using this approach.

## Hiding Elements
```javascript
function hideContent() {
    document.getElementById("content").style.display = "none";
}
```
Makes an HTML element invisible by changing its display property to "none".

## Showing Elements
```javascript
function showContent() {
    document.getElementById("content").style.display = "block";
}
```
Makes a hidden HTML element visible by changing its display property to "block".

## Complete Interactive Example
```html
<!DOCTYPE html>
<html>
<body>
<div id="content">
    <h1>Welcome</h1>
    <p id="message">Hello Visitor</p>
    <button onclick="changeText()">Click Me</button>
</div>

<script>
function changeText() {
    let element = document.getElementById("message");
    element.innerHTML = "Welcome to JavaScript";
    element.style.fontSize = "24px";
}
</script>
</body>
</html>
```
This example combines multiple JavaScript features: changing content, modifying styles, and handling a button click event. When the button is clicked, it changes both the text and its size.

# Output

## Using innerHTML
```html
<!DOCTYPE html>
<html>
<body>
<h2>Welcome Message</h2>
<p id="greeting"></p>
<script>
document.getElementById("greeting").innerHTML = "Welcome " + (10 + 5);
</script>
</body>
</html>
```
Modifies the content of an HTML element by accessing its innerHTML property. The example adds text and performs a calculation to display "Welcome 15".

## Using document.write()
```html
<!DOCTYPE html>
<html>
<body>
<h2>Daily Report</h2>
<p>Sales Summary</p>
<script>
document.write("Total Sales: $" + (1500 + 2300));
</script>
</body>
</html>
```
Writes content directly to the HTML document. Note that using document.write() after the page loads will overwrite the entire document.

## Using Alert Box
```html
<!DOCTYPE html>
<html>
<body>
<script>
let name = "Hassan";
window.alert("Welcome back " + name);
// The window prefix is optional:
alert("Your balance is $" + (2000 - 500));
</script>
</body>
</html>
```
Displays pop-up alert boxes with messages. Both window.alert() and alert() work the same way since window is the global object.

## Using Console Log
```html
<!DOCTYPE html>
<html>
<body>
<script>
let user = "Malik";
console.log("User logged in: " + user);
console.log("Session started at: " + new Date());
</script>
</body>
</html>
```
Outputs messages to the browser's console, useful for debugging and development purposes.

# Syntax

1. Literals (Direct Value Representation):
    ```javascript
    // Number Literals
    const integer = 42;
    const float = 3.14;
    const scientific = 2.998e8;
    const binary = 0b1010;      // Binary (10)
    const octal = 0o756;        // Octal (494)
    const hexadecimal = 0xFF;   // Hexadecimal (255)

    // String Literals
    const single = 'Hello';
    const double = "World";
    const template = `Hello ${double}`;
    const multiLine = `
        This is a
        multi-line
        string
    `;

    // Boolean Literals
    const isTrue = true;
    const isFalse = false;

    // Array Literals
    const emptyArray = [];
    const numbers = [1, 2, 3];
    const mixed = [1, "two", true, [4, 5]];

    // Object Literals
    const person = {
        name: "Amina",
        age: 30,
        "likes coding": true    // Property name with space
    };

    // Regular Expression Literals
    const regex = /[A-Z]+/g;
    ```

2. Declarations and Assignments:
    ```javascript
    // Variable Declarations
    let x;                  // Declaration only
    let y = 5;             // Declaration with initialization
    const PI = 3.14;       // Constant declaration (must be initialized)
    var oldStyle = "old";  // Old-style declaration

    // Multiple Declarations
    let a, b, c;
    let d = 1, e = 2, f = 3;

    // Function Declarations
    function normalFunction(a, b) {
        return a + b;
    }

    // Function Expression
    const multiply = function(a, b) {
        return a * b;
    };

    // Arrow Function
    const add = (a, b) => a + b;
    ```

3. White Space and Formatting:
    ```javascript
    // White space is flexible
    let result=1+2;            // Valid but hard to read
    let result = 1 + 2;        // Better readability

    // Line breaks are flexible
    let longString = "This is a very long string" +
                    " that spans multiple lines" +
                    " in the code";

    // Semicolons are optional (but recommended)
    let a = 1     // Valid
    let b = 2;    // Also valid

    // Object formatting
    const user = {
        name: "John",
        age: 30,    // Trailing comma is allowed
    };

    // Function call formatting
    someFunction(
        argument1,
        argument2,
        argument3
    );
    ```

4. Comments:
    ```javascript
    // Single-line comment

    /* Multi-line
    comment
    block */

    /** 
     * Documentation comment
     * @param {string} name - The name parameter
     * @returns {string} A greeting message
     */
    function greet(name) {
        return `Hello, ${name}!`;
    }
    ```

5. Statement Types:
    ```javascript
    // Expression Statement
    x = 5;
    functionCall();

    // Conditional Statement
    if (condition) {
        // code
    }

    // Loop Statement
    for (let i = 0; i < 5; i++) {
        // code
    }

    // Label Statement
    loop1: for (let i = 0; i < 5; i++) {
        continue loop1;
    }

    // Exception Handling
    try {
        // code that might throw error
    } catch (error) {
        // handle error
    } finally {
        // cleanup code
    }
    ```

6. Operator Precedence:
    ```javascript
    // Arithmetic
    let calculation = 2 + 3 * 4;    // 14, not 20

    // Assignment with operation
    let number = 5;
    number += 3;    // Same as: number = number + 3

    // Comparison and Logical
    let result = (5 > 3) && (10 <= 10);  // true

    // Conditional (Ternary) Operator
    let status = temprature >= 30 ? "Hot" : "Nice";
    ```

## Valid and Invalid Names

```javascript
// Valid variable names
let firstName = "Khalid";      // Camel case
let last_name = "Husain";      // Snake case
let _private = "hidden";     // Leading underscore
let $price = 99.99;         // Dollar sign
let π = 3.14159;            // Unicode characters allowed
let ترحيب = "مرحبا";    // Non-Latin characters allowed
let \u0061 = "a";           // Unicode escape sequence
let café = "coffee";        // Accented characters
let x1 = 1;                 // Numbers allowed (not at start)
let $_$ = "valid";          // Multiple special chars
let _123 = "valid";         // Underscore with numbers

// Invalid variable names
// let 1name = "invalid";    // Can't start with number
// let my-name = "invalid";  // Hyphens not allowed
// let my name = "invalid";  // No spaces
// let class = "invalid";    // Reserved keyword
// let for = "invalid";      // Reserved keyword
// let @email = "invalid";   // @ not allowed
// let my.name = "invalid";  // Dots not allowed

// Reserved Keywords (cannot be used as identifiers)
// break     case      catch     class     const     continue
// debugger  default   delete    do        else      export
// extends   finally   for       function  if        import
// in        instance  new       return    super     switch
// this      throw     try       typeof    var       void
// while     with      yield
```

## Examples

1. Functions:
    ```javascript
    // Regular function
    function add(a, b) {
        return a + b;
    }

    // Arrow function
    const multiply = (a, b) => a * b;

    // Function with default parameters
    function greet(name = "Guest") {
        return `Hello ${name}`;
    }
    ```

3. Conditionals:
    ```javascript
    // If statement
    if (age >= 60) {
        console.log("Senior Discount");
    } else if (age >= 22) {
        console.log("No Discount");
    } else {
        console.log("Student Discount");
    }

    // Switch statement
    switch (fruit) {
        case "banana":
            console.log("Yellow");
            break;
        case "apple":
            console.log("Red");
            break;
        default:
            console.log("Unknown");
    }
    ```

4. Loops:
    ```javascript
    // For loop
    for (let i = 0; i < 5; i++) {
        console.log(i);
    }

    // While loop
    let i = 0;
    while (i < 5) {
        console.log(i);
        i++;
    }

    // For...of loop (arrays)
    const numbers = [1, 2, 3];
    for (const num of numbers) {
        console.log(num);
    }

    // For...in loop (objects)
    const person = {name: "John", age: 25};
    for (const key in person) {
        console.log(`${key}: ${person[key]}`);
    }
    ```

7. Error Handling:
    ```javascript
    try {
        // Code that might throw an error
        throw new Error("Something went wrong");
    } catch (error) {
        console.error(error.message);
    } finally {
        // Always executes
        console.log("Cleanup");
    }
    ```

# `let` VS `var`
1. Scope:
    ```javascript
    // var is function-scoped
    function example() {
        var x = 1;
        if (true) {
            var x = 2;     // Same variable as above
            console.log(x); // 2
        }
        console.log(x);     // 2
    }

    // let is block-scoped
    function example() {
        let x = 1;
        if (true) {
            let x = 2;     // Different variable
            console.log(x); // 2
        }
        console.log(x);     // 1
    }
    ```

2. Hoisting:
    ```javascript
    // var is hoisted and initialized with undefined
    console.log(x);     // undefined
    var x = 5;

    // let is hoisted but not initialized (Temporal Dead Zone)
    console.log(y);     // ReferenceError
    let y = 5;
    ```

3. Global Object:
    ```javascript
    // var creates property on global object (window in browsers)
    var globalVar = 'Hello';
    console.log(window.globalVar); // 'Hello'

    // let doesn't create property on global object
    let globalLet = 'Hello';
    console.log(window.globalLet); // undefined
    ```

4. Redeclaration:
    ```javascript
    // var allows redeclaration
    var x = 1;
    var x = 2; // OK

    // let prevents redeclaration
    let y = 1;
    let y = 2; // SyntaxError
    ```

These differences make `let` generally safer to use because it:
- Prevents accidental variable leakage
- Makes scope more predictable
- Catches potential errors earlier
- Follows better block-scoping practices

This is why modern JavaScript development typically favors `let` (and `const`) over `var`.

# Coding Style

1. Case Sensitivity:
    ```javascript
    // Variables - case sensitive
    let name = "Ahmed";
    let Name = "Omar";
    let NAME = "Sarah";
    // These are three different variables

    // Functions - case sensitive
    function sayHello() {}
    function sayHELLO() {}
    // These are two different functions

    // Properties - case sensitive
    const user = {
        name: "John",
        Name: "Jane",
        firstName: "John",
        firstname: "Jane"
    };
    // These are all different properties
    ```

2. Common Naming Conventions:
    ```javascript
    // camelCase - for variables, functions, methods
    let firstName = "Rashid";
    let isUserActive = true;
    function calculateTotal() {}

    // PascalCase - for classes and constructors
    class UserAccount {
        constructor() {}
    }
    const DateFormatter = class {};

    // UPPERCASE_WITH_UNDERSCORES - for constants
    const MAX_COUNT = 100;
    const API_BASE_URL = "https://api.example.com";
    ```

# JavaScript and HTML DOM

## DOM Definition
The Document Object Model (DOM) is a programming interface for HTML documents. It represents the document as a tree-like structure where each node is an object representing a part of the document.

## HTML DOM
The HTML DOM is created by the browser when a web page loads. It models HTML documents as a tree of objects:
```
document
    └── html
        ├── head
        │   ├── title
        │   └── meta
        └── body
            ├── div
            ├── p
            └── span
```

## JavaScript and HTML DOM
JavaScript uses the DOM to access and manipulate HTML documents. It can:
- Find elements
- Change elements
- Add elements
- Delete elements
- React to events

## Finding Elements

### document.getElementById(id)
Finds an element by its ID:
```javascript
const element = document.getElementById("myId");
```

### document.getElementsByTagName(name)
Finds elements by tag name:
```javascript
const paragraphs = document.getElementsByTagName("p");
```

### document.getElementsByClassName(name)
Finds elements by class name:
```javascript
const elements = document.getElementsByClassName("myClass");
```

### document.querySelectorAll()
Finds all elements matching a CSS selector:
```javascript
// All paragraphs with class "highlight"
const elements = document.querySelectorAll("p.highlight");
// All elements with specific attribute
const inputs = document.querySelectorAll("[data-type='special']");
// Complex selectors
const nested = document.querySelectorAll("div > p:first-child");
```

## Document Collections

### document.links
Returns all `<a>` and `<area>` elements:
```javascript
const anchors = document.links;
console.log(anchors.length);
```

### document.forms
Returns all `<form>` elements in the document:
```javascript
const forms = document.forms;
const firstForm = forms[0];
```

### document.images
Returns all `<img>` elements in the document:
```javascript
const images = document.images;
console.log(images.length);
```

## Changing HTML Content

### element.innerHTML
Changes the HTML content of an element:
```javascript
element.innerHTML = "New content";
```

## Changing Attributes

### Direct method
```javascript
element.attribute = "new value";
element.src = "image.jpg";
```

### setAttribute method
```javascript
element.setAttribute("class", "highlight");
```

## Changing Styles

### Using style property
```javascript
element.style.property = "new style";
element.style.backgroundColor = "red";
element.style.fontSize = "16px";
```

## Creating Elements

### document.createElement()
```javascript
const div = document.createElement("div");
```

### document.appendChild()
```javascript
parent.appendChild(newElement);
```

## Removing Elements

### removeChild()
```javascript
parent.removeChild(element);
```

## Replacing Elements

### replaceChild()
```javascript
parent.replaceChild(newElement, oldElement);
```

## Nodes and NodeLists

### Nodes
A node is any DOM object in the document tree. Common node types:
- Element nodes (tags)
- Text nodes (text content)
- Comment nodes (HTML comments)
- Document node (the document itself)

Node properties:
```javascript
node.parentNode
node.childNodes
node.firstChild
node.lastChild
node.nextSibling
node.previousSibling
```

### NodeLists
A NodeList is a collection of nodes. It's similar to an array but isn't one:
```javascript
const nodeList = document.querySelectorAll("p");
// Convert to array if needed
const array = Array.from(nodeList);
```

## Script Loading Strategies

### defer
Delays script execution until HTML document is fully parsed:
```javascript
<script defer src="script.js"></script>
```
- Downloads in parallel with HTML parsing
- Executes in order
- Only works for external scripts
- Best for most scripts that need the entire DOM

### async
Loads and executes script asynchronously:
```javascript
<script async src="script.js"></script>
```
- Downloads in parallel with HTML parsing
- Executes as soon as downloaded (can interrupt HTML parsing)
- Order of execution not guaranteed
- Best for independent scripts (analytics, ads)

Comparison:
![This image is from the HTML spec, copied and cropped to a reduced version, under CC BY 4.0 license terms.](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script/async-defer.jpg)

# JavaScript Events

## What are events

> Events are fired to notify code of "interesting changes" that may affect code execution. These can arise from user interactions such as using a mouse or resizing a window, changes in the state of the underlying environment (e.g. low battery or media events from the operating system), and other causes.

[https://developer.mozilla.org/en-US/docs/Web/Events](https://developer.mozilla.org/en-US/docs/Web/Events)

## Anonymous (Headless) Functions

```javascript
// Traditional named function
function greet(name) {
    return `Hello, ${name}!`;
}

// Anonymous function expressions
const greet1 = function(name) {
    return `Hello, ${name}!`;
};

// Arrow function (also anonymous)
const greet2 = (name) => `Hello, ${name}!`;
```

## Callables
```js
// Basic operator functions
function add(a, b) {
    return a + b;
}

function subtract(a, b) {
    return a - b;
}

// Higher-order function that takes an operator function as argument
function calculate(operatorFn) {
    return operatorFn(5, 3);
}

console.log(calculate(add));
console.log(calculate(subtract));
```

## Event Handlers Examples

1. Traditional DOM Event Handlers:
```javascript
// HTML Element
<button id="btn1">Traditional Handler</button>

// JavaScript
const btn1 = document.getElementById('btn1');
btn1.onclick = function() {
    alert('Button clicked!');
};

// Alternative syntax
btn1.onclick = handleClick;
function handleClick() {
    alert('Button clicked!');
}
```

2. addEventListener Method:
```javascript
// HTML Element
<button id="btn2">Modern Handler</button>

// JavaScript
const btn2 = document.getElementById('btn2');
btn2.addEventListener('click', function() {
    alert('Button clicked!');
});

// With named function
btn2.addEventListener('click', handleClick);
function handleClick(event) {
    alert('Button clicked!');
    console.log(event); // Access event object
}
```

3. Multiple Event Handlers:
```javascript
// HTML Element
<div id="myDiv">Hover and Click me</div>

// JavaScript
const myDiv = document.getElementById('myDiv');

// Multiple events on same element
myDiv.addEventListener('click', function() {
    console.log('Element clicked');
});

myDiv.addEventListener('mouseover', function() {
    console.log('Mouse over element');
});

// Multiple handlers for same event
myDiv.addEventListener('click', function() {
    console.log('First click handler');
});

myDiv.addEventListener('click', function() {
    console.log('Second click handler');
});
```

4. Removing Event Listeners:
```javascript
// HTML Element
<button id="btn3">Click me</button>

// JavaScript
const btn3 = document.getElementById('btn3');

function handleClick() {
    console.log('Button clicked');
}

// Add event listener
btn3.addEventListener('click', handleClick);

// Remove event listener
btn3.removeEventListener('click', handleClick);
```

5. Event Object Properties:
```javascript
// HTML Element
<input id="textInput" type="text">

// JavaScript
const textInput = document.getElementById('textInput');

textInput.addEventListener('keydown', function(event) {
    console.log('Key pressed:', event.key);
    console.log('Key code:', event.keyCode);
    console.log('Shift key pressed:', event.shiftKey);
    console.log('Target element:', event.target);
});
```

6. Event Delegation:
```javascript
// HTML Element
<ul id="parentList">
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>

// JavaScript
const parentList = document.getElementById('parentList');

parentList.addEventListener('click', function(event) {
    if(event.target.tagName === 'LI') {
        console.log('Clicked on:', event.target.textContent);
    }
});
```

7. Preventing Default Behavior:
```javascript
// HTML Element
<form id="myForm">
    <input type="submit" value="Submit">
</form>

// JavaScript
const form = document.getElementById('myForm');

form.addEventListener('submit', function(event) {
    event.preventDefault(); // Prevents form submission
    console.log('Form submission prevented');
});
```