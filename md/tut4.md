# JavaScript DOM and Events

## Code

Create an HTML page using the following code, test it, and try to understand it.

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Shopping List Manager</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@picocss/pico@1/css/pico.min.css">
    <style>
        .completed {
            text-decoration: line-through;
            opacity: 0.7;
        }

        #shopping-list li {
            list-style-type: none;
        }
    </style>

    <script src="script.js" defer></script>
</head>

<body>
    <main class="container">
        <h1>Shopping List Manager - DOM & Events Tutorial</h1>

        <article>
            <h2>1. Load Event Example</h2>
            <p>The page loads with a welcome message and loads saved items from localStorage.</p>
            <select id="theme-selector">
                <option value="light">Light Theme</option>
                <option value="dark">Dark Theme</option>
            </select>
        </article>

        <article>
            <h2>2. Click & Submit Events Example</h2>
            <p>Add items to your shopping list:</p>
            <form id="add-item-form">
                <div class="grid">
                    <input type="text" id="item-input" placeholder="Enter item name" required>
                    <button type="submit">Add Item</button>
                </div>
            </form>
        </article>

        <article>
            <h2>3. Change & Click Events Example</h2>
            <p>Your shopping list (click items to mark as complete):</p>
            <div class="grid">
                <div>
                    <select id="filter-select">
                        <option value="all">All Items</option>
                        <option value="active">Active</option>
                        <option value="completed">Completed</option>
                    </select>
                </div>
                <button id="clear-completed" class="contrast">Clear Completed</button>
            </div>
            <ul id="shopping-list" role="list"></ul>
        </article>
    </main>
</body>

</html>
```

Create the following JavaScript file in the same directory as the HTML file:
```js
// Cookie management functions
function setCookie(name, value, days) {
    let expires = "";
    if (days) {
        const date = new Date();
        date.setTime(date.getTime() + (days * 24 * 60 * 60 * 1000));
        expires = "; expires=" + date.toUTCString();
    }
    document.cookie = name + "=" + value + expires + "; path=/";
}

function getCookie(name) {
    const nameEQ = name + "=";
    const ca = document.cookie.split(';');
    for (let i = 0; i < ca.length; i++) {
        let c = ca[i];
        while (c.charAt(0) == ' ') c = c.substring(1, c.length);
        if (c.indexOf(nameEQ) == 0) return c.substring(nameEQ.length, c.length);
    }
    return null;
}

// Theme management
function setTheme(theme) {
    document.documentElement.setAttribute('data-theme', theme);
    document.getElementById('theme-selector').value = theme;
    setCookie('theme', theme, 365);
}

// Filter management
function filterItems(filterValue) {
    const items = document.querySelectorAll('#shopping-list li');
    items.forEach(item => {
        const article = item.querySelector('article');
        switch (filterValue) {
            case 'active':
                item.style.display = article.querySelector('span').classList.contains('completed') ? 'none' : '';
                break;
            case 'completed':
                item.style.display = article.querySelector('span').classList.contains('completed') ? '' : 'none';
                break;
            default: // 'all'
                item.style.display = '';
        }
    });
}

// Create list item element
function createListItem(text, completed = false) {
    const li = document.createElement('li');
    const article = document.createElement('article');

    article.innerHTML = `
        <div class="grid">
            <span class="${completed ? 'completed' : ''}">${text}</span>
            <div>
                <button class="complete-btn outline ${completed ? 'secondary' : ''}">
                    ${completed ? 'Undo' : 'Complete'}
                </button>
                <button class="delete-btn contrast">Delete</button>
            </div>
        </div>
    `;

    // Complete button event
    article.querySelector('.complete-btn').addEventListener('click', function (event) {
        event.stopPropagation();
        const span = article.querySelector('span');
        span.classList.toggle('completed');
        this.textContent = span.classList.contains('completed') ? 'Undo' : 'Complete';
        this.classList.toggle('secondary');
        saveItems();
        filterItems(document.getElementById('filter-select').value);
    });

    // Delete button event
    article.querySelector('.delete-btn').addEventListener('click', function (event) {
        event.stopPropagation();
        li.remove();
        saveItems();
    });

    li.appendChild(article);
    return li;
}

function addItem(text, completed = false) {
    const list = document.getElementById('shopping-list');
    const li = createListItem(text, completed);
    list.appendChild(li);
    filterItems(document.getElementById('filter-select').value);
}

function saveItems() {
    const items = [];
    document.querySelectorAll('#shopping-list article').forEach(article => {
        items.push({
            text: article.querySelector('span').textContent,
            completed: article.querySelector('span').classList.contains('completed')
        });
    });
    localStorage.setItem('shoppingList', JSON.stringify(items));
}

// Event Listeners
document.addEventListener('DOMContentLoaded', function () {
    // Load theme
    const savedTheme = getCookie('theme') || 'light';
    setTheme(savedTheme);

    // Load items
    const savedItems = JSON.parse(localStorage.getItem('shoppingList') || '[]');
    savedItems.forEach(item => addItem(item.text, item.completed));
});

document.getElementById('theme-selector').addEventListener('change', function (event) {
    setTheme(event.target.value);
});

document.getElementById('filter-select').addEventListener('change', function (event) {
    filterItems(event.target.value);
});

document.getElementById('clear-completed').addEventListener('click', function () {
    document.querySelectorAll('#shopping-list span.completed').forEach(span => {
        span.closest('li').remove();
    });
    saveItems();
});

document.getElementById('add-item-form').addEventListener('submit', function (event) {
    event.preventDefault();
    const input = document.getElementById('item-input');
    const itemName = input.value.trim();

    if (itemName) {
        addItem(itemName);
        input.value = '';
        saveItems();
    }
});
```

## Explination

### 1. HTML Setup
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Shopping List Manager</title>
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@picocss/pico@1/css/pico.min.css">
    <style>
        .completed {
            text-decoration: line-through;
            opacity: 0.7;
        }

        #shopping-list li {
            list-style-type: none;
        }
    </style>
</head>
```
**Explanation:**
- `viewport` meta tag: Makes the page responsive on mobile devices
- Using Pico CSS: A minimal CSS framework for quick, clean styling
- Custom CSS: Defines how completed items look (strikethrough and faded) and remove bullets from list items

### 2. Main Layout Structure
```html
<body>
    <main class="container">
        <!-- Theme Selection -->
        <article>
            <h2>1. Load Event Example</h2>
            <select id="theme-selector">
                <option value="light">Light Theme</option>
                <option value="dark">Dark Theme</option>
            </select>
        </article>

        <!-- Add Item Form -->
        <article>
            <h2>2. Click & Submit Events Example</h2>
            <form id="add-item-form">
                <div class="grid">
                    <input type="text" id="item-input" required>
                    <button type="submit">Add Item</button>
                </div>
            </form>
        </article>

        <!-- Shopping List -->
        <article>
            <h2>3. Change & Click Events Example</h2>
            <div class="grid">
                <select id="filter-select">...</select>
                <button id="clear-completed">Clear Completed</button>
            </div>
            <ul id="shopping-list" role="list"></ul>
        </article>
    </main>
```
**Explanation:**
- Organized in three main sections:
  1. Theme selection: Controls the app's appearance
  2. Item input: Where users add new items
  3. List display: Shows items and provides filtering options
- Uses semantic HTML elements (`main`, `article`, `form`)
- Grid layout for responsive alignment
- ARIA role for better accessibility

### 3. Cookie Management
```javascript
function setCookie(name, value, days) {
    let expires = "";
    if (days) {
        const date = new Date();
        date.setTime(date.getTime() + (days * 24 * 60 * 60 * 1000));
        expires = "; expires=" + date.toUTCString();
    }
    document.cookie = name + "=" + value + expires + "; path=/";
}

function getCookie(name) {
    const nameEQ = name + "=";
    const ca = document.cookie.split(';');
    for(let i = 0; i < ca.length; i++) {
        let c = ca[i];
        while (c.charAt(0) == ' ') c = c.substring(1, c.length);
        if (c.indexOf(nameEQ) == 0) return c.substring(nameEQ.length, c.length);
    }
    return null;
}
```
**Explanation:**
- `setCookie`: 
  - Takes name, value, and expiration days
  - Calculates expiration date if days provided
  - Creates cookie string with proper format
  - Sets path to root ('/') for site-wide access

- `getCookie`:
  - Splits all cookies into array
  - Removes whitespace
  - Finds matching cookie by name
  - Returns value or null if not found

### 4. Theme Management
```javascript
function setTheme(theme) {
    document.documentElement.setAttribute('data-theme', theme);
    document.getElementById('theme-selector').value = theme;
    setCookie('theme', theme, 365);
}
```
**Explanation:**
- Changes theme by setting HTML attribute
- Updates select element to match current theme
- Saves preference in cookie for one year
- Works with Pico CSS's built-in theme system

### 5. Filter Management
```javascript
function filterItems(filterValue) {
    const items = document.querySelectorAll('#shopping-list li');
    items.forEach(item => {
        const article = item.querySelector('article');
        switch(filterValue) {
            case 'active':
                item.style.display = article.querySelector('span').classList.contains('completed') ? 'none' : '';
                break;
            case 'completed':
                item.style.display = article.querySelector('span').classList.contains('completed') ? '' : 'none';
                break;
            default: // 'all'
                item.style.display = '';
        }
    });
}
```
**Explanation:**
- Takes filter value ('all', 'active', or 'completed')
- Gets all list items
- For each item:
  - Checks if it's completed
  - Shows/hides based on filter value
  - Uses CSS display property for visibility
- Preserves item order in DOM

### 6. List Item Management
```javascript
function createListItem(text, completed = false) {
    const li = document.createElement('li');
    const article = document.createElement('article');
    
    article.innerHTML = `
        <div class="grid">
            <span class="${completed ? 'completed' : ''}">${text}</span>
            <div>
                <button class="complete-btn outline ${completed ? 'secondary' : ''}">
                    ${completed ? 'Undo' : 'Complete'}
                </button>
                <button class="delete-btn contrast">Delete</button>
            </div>
        </div>
    `;

    // Event listeners for buttons
    article.querySelector('.complete-btn').addEventListener('click', function(event) {
        event.stopPropagation();
        const span = article.querySelector('span');
        span.classList.toggle('completed');
        this.textContent = span.classList.contains('completed') ? 'Undo' : 'Complete';
        this.classList.toggle('secondary');
        saveItems();
        filterItems(document.getElementById('filter-select').value);
    });

    article.querySelector('.delete-btn').addEventListener('click', function(event) {
        event.stopPropagation();
        li.remove();
        saveItems();
    });

    li.appendChild(article);
    return li;
}
```
**Explanation:**
- Creates new list item with:
  - Text content
  - Complete/Undo button
  - Delete button
- Sets up event listeners:
  - Complete/Undo: Toggles completion status
  - Delete: Removes item
- Updates storage and filters after changes
- Uses event.stopPropagation() to prevent event bubbling

### 7. Storage Management
```javascript
function saveItems() {
    const items = [];
    document.querySelectorAll('#shopping-list article').forEach(article => {
        items.push({
            text: article.querySelector('span').textContent,
            completed: article.querySelector('span').classList.contains('completed')
        });
    });
    localStorage.setItem('shoppingList', JSON.stringify(items));
}
```
**Explanation:**
- Collects all current items
- Creates array of objects with:
  - Item text
  - Completion status
- Converts to JSON
- Saves to localStorage
- Called after any list changes

### 8. Event Listeners
```javascript
document.addEventListener('DOMContentLoaded', function() {
    // Initial setup
    const savedTheme = getCookie('theme') || 'light';
    setTheme(savedTheme);
    
    // Load saved items
    const savedItems = JSON.parse(localStorage.getItem('shoppingList') || '[]');
    savedItems.forEach(item => addItem(item.text, item.completed));
});

// Other event listeners...
```
**Explanation:**
- DOMContentLoaded: Runs when page loads
  - Restores saved theme
  - Loads saved items
- Theme selector: Updates theme on change
- Filter select: Updates visible items
- Clear completed: Removes done items
- Form submit: Adds new items
