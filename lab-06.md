# Lab 6: Shopping list application

Last week’s exercise demonstrated how to manipulate the Document Object Model (DOM) after receiving user input. This week, you will learn how to store and retrieve data to/from the browser’s local storage data store, to be retained between between browser sessions and used on multiple pages. Think of it as an insecure but 'free' and server-less data store (Chrome has a 5MB limit, whereas cookies can store far less than even 1MB).

## Build a list

First we will get a very basic list working so we can add items to our list using javascript code.

We start with a blank template and add a simple header and a single [unordered list element][ulElement] (use an ordered list if you want numbering).
This list element will become our shopping list.
The list is given the id `shopping` so we can select it by id.

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Shopping list</title>
  <link rel="stylesheet" href="css/styles.css">
</head>
<body>
  <header>
    <h1>Shopping list</h1>
  </header>
  <ul id="shopping"></ul>
  <script src="js/shopping.js"></script>
</body>
</html>
```

## Adding items

Now in the linked file `js/shopping.js` we can get a handle to the list and write a simple function to add items to the list.

```Javascript
const listElement = document.getElementById('shopping');

function addItem(item) {
  const itemElement = document.createElement('li');
  itemElement.textContent = item;
  listElement.appendChild(itemElement);
};

```

The function uses [`document.createElement`][createElement] to create an [`li`][li] element.
It places text in the element using [`node.textContent`][textContent] and finally inserts our new element into the DOM using [`node.appendChild`][appendChild].

We can now add items by calling our function. Try this in the console.

```Javascript
addItem('rice');
addItem('pasta');
```

We can also add multiple items from an array using [`Array.prototype.forEach`][forEach].
This is a method available on all arrays, it takes a callback function as an argument.
Each item of the array is passed in turn as an argument into the callback function.


```Javascript
const list = ['rice', 'pasta', 'tea', 'coffee'];
list.forEach(item => {
  addItem(item);
});
```

[`Array.prototype.forEach`][forEach] is useful for conducting arbitrary operations.
The argument (`item` in this case, but any name is allowed) is set to the value of each element in turn.
In this case, we simply call the `addItem` method with each item in the list.
So `addItem` is called four times, once for each value.

## Clearing the list

We need a function to clear the entire list.
We could do this by replacing the content of the list element with an empty string.

```Javascript
function clearList() {
  listElement.innerHTML = "";
}
```

However, its more efficient to loop over the DOM and remove each element in turn.

```Javascript
function clearList() {
  while(listElement.firstChild) {
    listElement.removeChild(listElement.firstChild);
  }
}
```

Using a [`while` loop][while] we call [`Node.firstChild`][firstChild] to identify the next element and [`Node.removeChild`][removeChild] to remove each element in turn.

Calling this function in the console now clears the list as expected.

Finally, tidy up the whole lot by wrapping the list generation code in a reusable function.

```Javascript
function renderList(list) {
  list.forEach(item => {
    addItem(item);
  });
}
```

We will use this later to load data from local storage.

In your javascript file you should now have one variable declaration (`listElement`) and three functions (`addItem()`, `clearList()` and `renderList()`).

## Add some interaction

Now we have the tools to add items and clear the list, we need to build a simple user interface.

Above the list, add an input element with `id="newItem"` and placeholder "new item" and a button with `id="addBtn"` and "add" as the content.

```html
<input placeholder="new item" id="newItem">
<button id="addBtn">add</button>
```

Below the list, add a button with `id="clearBtn"` and "clear" as the content.

```html
<button id="clearBtn">clear</button>
```

Wrap the list and these new elements in a `main` element.
Your `index.html` file should now look like this.

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Shopping list</title>
  <link rel="stylesheet" href="css/styles.css">
</head>
<body>
  <header>
    <h1>Shopping list</h1>
  </header>
  <main>
    <input placeholder="new item" id="newItem">
    <button id="addBtn">add</button>
    <ul id="shopping"></ul>
    <button id="clearBtn">clear</button>
  </main>
  <script src="js/shopping.js"></script>
</body>
</html>
```

We need to create JavaScript handles to our new elements.
Add these new lines to the top of the file.

```Javascript
const newItem = document.getElementById('newItem');
const addBtn = document.getElementById('addBtn');
const clearBtn = document.getElementById('clearBtn');
```

Now we can add a simple event listener (using [`addEventListener`][addEventListener]) to our 'add' button to insert a new element into our list based on the input value.

Our first version of the event listener can be added at the bottom of the file.

```Javascript
addBtn.addEventListener('click', ev => {
  addItem(newItem.value);
});
```

Type some text into the input and click the add button. This works pretty well but it has some problems.

- What happens when the input is blank?
- What happens when we click the add button more than once?

We need to add a few lines of code to smooth out this interaction.

First, we check that the input has some text and only add the item if it does.

```Javascript
addBtn.addEventListener('click', ev => {
  if(newItem.value) { //<- this
    addItem(newItem.value);
  } //<- and this
});
```

Try it. No more blank entries in our list. Great. But we still add the same value multiple times when we click the button more than once.

So we clear the input by setting its value to `null` each time an item is successfully added to the list.

```Javascript
addBtn.addEventListener('click', ev => {
  if(newItem.value) {
    addItem(newItem.value);
    newItem.value = null; //<- this
  }
});
```

To clear the whole list we add an event listener to the clear button.

```Javascript
clearBtn.addEventListener('click', ev => {
  clearList();
});
```

Try it.
We now have a very basic working list.

## Removing individual items

The list is becoming useful but what if we make a mistake and want to remove an item from the list without starting from scratch?

We need a way to select an individual item for removal. For this, we need a button on each item. So we need to modify our `addItem` function.

```Javascript
function addItem(item) {
  const itemElement = document.createElement('li');
  itemElement.textContent = item;
  const deleteButton = document.createElement('button'); // <- new
  deleteButton.textContent = 'x';                        // <- new
  itemElement.appendChild(deleteButton);                 // <- new
  listElement.appendChild(itemElement);
};
```

We have created a new button for each element and appended it to the list item.
When we add new items, they now also contain a button which we will use to delete the individual list item.

We need the new button to delete the entire `li` element. For this we use a closure.
We add an event listener to each button which removes the parent element from the list.

```Javascript
function addItem(item) {
  const itemElement = document.createElement('li');
  itemElement.textContent = item;
  const deleteButton = document.createElement('button');
  deleteButton.textContent = 'x';
  itemElement.appendChild(deleteButton);
  deleteButton.addEventListener('click', ev => { // <- new
    listElement.removeChild(itemElement);        // <- new
  });                                            // <- new
  listElement.appendChild(itemElement);
};
```

The closure means that the event listener will always have a reference to `itemElement`.
Even after the `addItem` function has completed, the scope it created, including the `const itemElement` is available to the `deleteButton` event listener.

## Tidy up the look and feel

At this point you may want to add some styles.
Begin with something like this.

```css
body {
  max-width: 500px;
  margin: auto;
}
ul {
  padding: 1em 0;
  margin: 0;
}
li {
  display: flex;
  justify-content: space-between;
}

```

We position the body in the center of the page, overwrite the default `ul` padding and margin and justify the `<li>` element content using `display: flex` and `justify-content: space-between`.
This will put the text on the left and the button on the right.

Add a few more styles if you like.

## Saving the list

We now have a fairly functional shopping list app. The only problem is that if we close the page or reload it the list data is lost and we begin with a blank list each time.

We will load the list from [local storage][localStorage] on opening the page and save the list back to local storage on closing the page.

First, we need to save the list to local storage.
We do this in an event listener we add to the window event handler [`onbeforeunload`][onbeforeunload] event.
This even will fire when the window is about to unload its resources in preparation to close the page.

```Javascript
window.addEventListener('beforeunload', ev => {
  const items = [...listElement.childNodes];
  if(items.length) {
    const list = items.map(item => {
      return item.textContent.slice(0, -1);
    });
    localStorage.setItem('shopping-list', list);
  } else {
    localStorage.removeItem('shopping-list');
  }
});

```

Here we are extracting our item data from the DOM.

First, we convert the list child nodes to an array using the [spread operator][spread]. Then we check the length of the array. If the array is empty then we delete our local storage record.

If the list contains data then we extract the item text into an array using the [Array.prototype.map][Array.prototype.map] function. We call [Node.textContent][textContent] and [String.prototype.slice][String.prototype.slice] on each list element within the callback.

Our item text is contained within each list item element along with a delete button. Note that [Node.textContent][textContent] returns the concatenation of the [textContent][textContent] of every child node. So we get an extra 'x' from the delete button concatenated to the end of our string. We remove this with [String.prototype.slice][String.prototype.slice].

## Loading the list

With the list data from previous session stored in local storage we now just need to read these data back into the page when the page loads.

For this, we add an event listener to the window event handler [DOMContentLoaded][DOMContentLoaded] event. This event fires once the DOM is completely loaded so we can be sure the list element will be available.

```Javascript
window.addEventListener('DOMContentLoaded', ev => {
  const shoppingList = localStorage.getItem('shopping-list');
  if(shoppingList) {
    renderList(shoppingList.split(','));
  }
});
```

We extract the data from local storage as a comma-separated string. To convert this to an array we use the [String.prototype.split][String.prototype.split] method and pass the resultant array into our `renderList()` function.

Now the list will be remembered even if we close the page and open it again.

## Upgrade the interface

The list is nice and all but if you want to write a long list then you have to flip between using the keyboard to type and using the mouse to click. This is annoying and inefficient.

The following code adds a handler for the input element `keyup` event. The `keyup` event fires when a key is released.

```Javascript
newItem.addEventListener("keyup", ev => {
  if (ev.keyCode === 13) {
    addBtn.click();
  }
});
```

The handler is very simple. If the enter key (keyCode 13) is being released then we call `addBtn.click()` to trigger the previously defined event handler for adding an item.

So now it is possible to add multiple items to the list without leaving the keyboard.

Another potential improvement is to allow comma-separated values to be entered into the input and separated out into items on the list.

To do this we can adjust the `addBtn` event listener.

```Javascript
addBtn.addEventListener('click', ev => {
  newItem.value.split(',').forEach(v => {
    if(v) {
      addItem(v);
    }
  });
  newItem.value = null;
});
```

Now the input value is split into an array of strings and each string is added to the list individually (but only if it contains text). Try this by entering multiple items separated by commas.

## Tidy up

Now we have a working system we will protect all our code inside a self-executing anonymous function.

```Javascript
(() => {
  // all existing code goes here
})()
```

This keeps all our variables cleanly outside of the global scope.

---

# Challenges

The shopping list app is now fairly functional. However, there are a few scenarios where it could be frustrating to work with and a few possible improvements.

## Multiple tabs

Think about what happens when the app is opened in two tabs simultaneously.

Try this:

1. Open the shopping list in a browser tab and add a few items

2. Open the shopping list in another tab, add a few more items and close the list.

3. Close the original tab.

4. Open the shopping list again.

What happened to your latest additions?

Try to implement an improvement to avoid this problem.

potential solutions:
 - allow a manual load/save option?
 - warn the user before editing the local storage?
 - work with the [`storage`][storageEvent] event?


## Multiple lists

If you have got this far then well done. This one is for experts only as it requires some fairly serious adaptations to the code. Though perhaps not as much as you might think.

Our list data are stored under the 'shopping-list' key in local storage.

Think about how you might allow for multiple shopping lists to be stored and managed.

What user interface changes would be required?

Try refactoring the code to allow the user to create and manage multiple named lists.

[addEventListener]: https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener "AddEventListener - MDN"

[Array.prototype.map]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map "Array.prototype.map - MDN"

[String.prototype.split]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split "String.prototype.split - MDN"

[String.prototype.slice]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/slice "String.prototype.slice - MDN"

[textContent]: https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent "Node.textContent - MDN"

[onbeforeunload]: https://developer.mozilla.org/en-US/docs/Web/API/WindowEventHandlers/onbeforeunload "beforeunload event - MDN"

[DOMContentLoaded]: https://developer.mozilla.org/en-US/docs/Web/API/Window/DOMContentLoaded_event "DOMContentLoaded event - MDN"

[ulElement]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/ul "The unordered list element - MDN"

[li]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/li "The list item element - MDN"

[createElement]: https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement "document.CreateElement - MDN"

[textContent]: https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent "node.textContent - MDN"

[appendChild]: https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild "node.appendChild - MDN"

[forEach]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach "Array.prototype.forEach - MDN"

[while]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/while "while - MDN"

[firstChild]: https://developer.mozilla.org/en-US/docs/Web/API/Node/firstChild "Node.firstChild - MDN"

[removeChild]: https://developer.mozilla.org/en-US/docs/Web/API/Node/removeChild "Node.removeChild - MDN"

[spread]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax "spread syntax - MDN"

[localStorage]: https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage "local storage - MDN"

[storageEvent]: https://developer.mozilla.org/en-US/docs/Web/API/Window/storage_event "storage event - MDN"
