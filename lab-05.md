# Exercise 05-lab: form fields and user input

This week we're using a different format for these instructions, so the exercise is broken up into tasks.

## Introduction

Rather than having a generic text input, there are specific input field types, many of which also determine how mobiles handle input. Some of these were introduced with HTML5:

- color
- date
- email
- number
- range
- search
- tel
- time
- url

Here’s an example of the syntax:

`<input type="color" value="#ff0000">`

The `value` attribute is optional, but can be used to set a default.

These input types will only accept **specific input** so are good for preventing some user errors e.g. an input of type "number" will only accept… you guessed it: numbers! If you try to type in a letter, nothing will show up. A "url" type field needs the full "https://" or "http://" prefix.

These fields also have built-in warnings that show up in the browser, which you can customise using JavaScript.

If you have errors, don’t forget to use `console.log()` to check your code at various points.

## Task 1 - Create an interface

Start with a basic "index.html" template like the sample-code repository. Add an `h1` tag containing the text "HTML5 forms:", with an `id="date"`.

```html
<h1 id="date">HTML5 forms: </h1>
```

Add a `<form>` element containing two `<fieldset>` elements. You use these to contain related input fields, and can style them to help make forms more logical and user-friendly.

In the first `fieldset` add:

1. a `<label>` element with the attribute `for="datePicker"` with the text "Date:" between the tags
2. an `<input>` element of `type="date"` and `id="datePicker"`

Instead of just adding text next to the form field, a `label` tag makes a form field accessible by relating the field's description directly to the field.

In the second `fieldset` add:

1. an input of type "color" with the `value` attribute set to a colour of your choice (e.g. `value="#eeccff"`) and give it an ID of "colour".
2. an input of type "range" with attributes `min="0"`, `max="100"` and `id="range"`.

Finally, below the form, add a paragraph tag containing the text "50" with an id of "the-value" and a class of "value".

```html
<p id="the-value" class="value">50</p>
```

In a "styles.css" file, add:

1. a style block for `.value` that sets its `width` to `50%`, and `text-align` to "center"
2. a style block for `fieldset` that simply adds a bottom margin of `0.5em`.

Validate your HTML and check that the fields are usable.

## Task 2 - Display the input values on the page

In a "scripts.js" file add the line: `"use-strict";`. This will throw up messages in the console that help prevent mistakes and sloppy code.

Below the line above add two `const` references - one to the main heading (with `id="date"`) and the other to the date input (with `id="datePicker"`).

Add an **event listener** to the input of type "date" that listens for a `"change"` event, and calls a function "setDate".

Write a function `setDate` that updates the `h1` tag’s `innerText` with the selected date:

```javascript
function setDate() {
  const d = new Date(getDate.value);
  // update the h1 innerText here
}
```

Hints:

1. for a human readable date (e.g. "Wed Nov 07 2018"), load the date string into a Date object (as above) and use `d.toDateString()`.
2. preserve the `h1` tag `innerText` in a variable before adding the date, and use template literal syntax (inside backticks you can use `${}` variable interpolation) to add the new date after the original text
3. "setDate" could call another function "showDate" that takes a date as a parameter and adds it to the `h1` tag `innerText`  (preserved in the previous step)

To pre-populate the `h1` tag with today's date, you could then also call "showDate" with today’s date as a parameter:

```javascript
let today = new Date();
showDate(today);
```

The date in the `h1` heading should change when the user picks a new date. The date should be formatted as the following example: "Wed Nov 07 2018".

## Task 3 - Modify an interface element using a "color" input

Store `const` references by ID to the `color` input field (`id="colour"` - note the spelling) and to the paragraph (`id="the-value"`).

Create a function `setColor` that simply sets the paragraph's `.style.backgroundColor` property to the `.value` of the `color` input.

Add an event listener to the form element that detects `"input"`, and calls `setColor` (no brackets).

You can then also call `setColor();` separately (with brackets) to set the paragraph background to the `color` field default.

The paragraph’s background colour should change when the user picks a colour from the browser’s colour dialogue panel.

## Task 4 - Modify an interface element using a "range" input

Add an event listener to the "range" input element that captures the element’s value when it detects "input", and calls a function `rangeAction`, that:

1. shows the value on the page immediately in the "innerText" of the paragraph tag
2. applies this value to its width, using `.style.width`.

The paragraph width should now change as the user moves the range slider.

---

If you managed to make these exercises work, experiment with handling and displaying input from other field types, or spend some time styling the inputs and page elements to make them more appealing.

## 05 Lab learning outcomes

- see how HTML5 form fields work by default
- use form fields to collect user input
- handle user input with JavaScript
- reflect user input directly on the page without reloading

Input fields are the primary method for getting user data, so it is essential to choose the correct type, depending on what you want the user to enter. Handling these on the page with JavaScript and providing feedback without (or before) calling any server scripts or reloading the page is one of the *key elements of modern web development*.

Manipulating the Document Object Model (DOM) in this way avoids excessive to-and-fro messages between the client (browser) and the web server, making user interaction more immediate and intuitive. If you use local storage (in a future lab) to retain user preferences between browser sessions, their choices can be made to persist in that user’s browser.
