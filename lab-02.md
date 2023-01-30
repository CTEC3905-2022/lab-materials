# Lab 2: A bit more of everything

This week we will continue with a gradual introduction to CSS layout and introduce JavaScript event handling.

> These instructions are maintained on github and you can help improve them.
If you find a problem with this document, if there is any ambiguity or confusion, we can update it right now, during the lab session.
For small changes, updated version can be available to everyone within a few minutes.


Try to understand every step in this lab.
Please **ask questions** if you are confused by any of the steps.
Your tutors are **happy to explain** anything in as much detail as necessary (this is what we are here for).


If you complete everything today, well done!

If not, don't worry - use your **Self-directed Learning Time (SDL)** to work on your code before next week's lab. If you get stuck, **keep trying**! A solution will be provided next week.


## A simple menu

> For all exercises, [validate](https://validator.w3.org/) your HTML.

Create a folder **lab-02** next to your **lab-01** folder from last week.
In your folder, create a file `index.html` with a basic HTML template and add a `<nav>` tag to your document with **five links** nested inside it.

```html
<nav>
  <a href="#">Home</a>
  <a href="#">Blog</a>
  <a href="#">Gallery</a>
  <a href="#">Contact</a>
  <a href="#">About</a>
</nav>
```

Create a CSS file `styles.css` and add a `link` into the `head` of your document.

```html
<link rel="stylesheet" href="styles.css">
```

Style the menu to appear horizontally across the top of the page using **CSS flexbox**. This should be pretty simple as this is the default behaviour for flexbox (see this [Flexbox cheat sheet](http://flexbox.malven.co/) for more info).

```css
nav {
  display: flex;
}
```

### Colours and box-model parameters

Give the `nav a` and `nav` rulesets different values for `background-color` (using named colours such as `red` or `#rgb` values) so you can see exactly where they are positioned.
Set the `color` property of the `nav a` ruleset to a colour which is clearly visible against your chosen background.

There are many ways to specify colours in CSS (see [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Applying_color)).

Experiment with the **box-model** properties of the `nav a` ruleset to determine the size of your menu items. Use `em` units (e.g. `margin: 1em`).

```css
nav {
  display: flex;
  background-color: aValueChosenByYou;
}

nav a {
  background-color: aValueChosenByYou;
  color: aValueChosenByYou;
  padding: aValueChosenByYou;
  margin: aValueChosenByYou;
}
```

Keep playing until you are broadly happy with the look of your menu.
To set different `margin` or `padding` values top/bottom and left/right, give two, space-separated values (e.g. `padding: 0.25em 0.5em`).

Notice there is a space around your `nav`.
This is the default `margin` of the `body` element, it can be removed by setting it to zero.
For hyperlinks the default underline and text colour is important to identify any links within regular text but for navigation menus is not necessary.
Consider changing the `text-decoration` property of your links.

### Hover and transition

Create a `nav a:hover` ruleset to change the `background-color` when the mouse hovers over your links.

Include a CSS [`transition`](https://developer.mozilla.org/en-US/docs/Web/CSS/transition) declaration to your `nav a` ruleset to make the menu item fade between the default state and the hover state.

```css
nav a {
  background-color: aValueChosenByYou;
  color: aValueChosenByYou;
  padding: aValueChosenByYou;
  margin: aValueChosenByYou;

  /* try different values - e.g. 3s */
  transition: background-color 0.7s;
}

nav a:hover {
  background-color: aValueChosenByYou;
}
```

Note that due to the cascading algorithm, the CSS `transition` declaration goes in the `nav a` ruleset, **not** the `nav a:hover` ruleset).
If you add it to the `nav a:hover` ruleset then the transition will only apply when transitioning to the hover state, not when transitioning back to the default state.
Make sure you understand this.
Experiment with different values of the transition duration.

If you don't understand exactly what's going on, ask a question that will help you (and others) to rule out some possibilities.

## Expand the page structure

Add a `header` element above the `nav` element, containing a top-level heading (`h1` element) with a few words.
Add a `main` element below the `nav` element, containing a paragraph (`p` element) with some text.

```html
<header>
  <h1>Your page title</h1>
</header>
<nav>
  <a href="#">Home</a>
  <a href="#">Blog</a>
  <a href="#">Gallery</a>
  <a href="#">Contact</a>
  <a href="#">About</a>
</nav>
<main>
  <p>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
    Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
    Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
    Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
  </p>
</main>
```

Use the Chrome developer tools to see how your elements are positioned.
Notice that the `h1` margin overflows the edges of the `header` element.
The same happens with the `p` within the `main` element.

Apply suitable `background-color` values for the new `header` and `main` elements.
Notice the problem?

Fix this by setting the `overflow` property on both the `header` and the `main` elements.

```css
header, main {
  overflow: auto;
}
```

## An alternative layout

Now we are going to completely change the layout.
We want to arrange the menu as a sidebar on the right hand side and stack it vertically.

First, use [flex-direction](http://flexbox.malven.co/) to stack the `a` elements in the `nav` vertically.
Your menu should still appear above the main element and take the full width of the viewport.

Set the `width` of the `nav` element to 15vw and set the `width` of the `main` element to 85vw (1vw is 1% of the viewport's width).
Now there should be room for the elements to sit next to each other.

If you have not yet done so, consider adding some left/right padding to keep the paragraph text away from the edge of the main element.

> Warning: Any left/right padding on either element will increase their width and so will cause the `main` element to wrap below the `nav`
> This can be fixed by setting the `box-sizing` property to `border-box` so the given width *includes* the padding.

Now, we need to take the `nav` element out of the normal flow.
First, we will do this by setting its `float` property to `right`.
This moves the `nav` to the right-hand edge of its container (in this case, the `body` element) and causes other elements to wrap around it.

You should see the main and nav elements squeeze onto one row.
If your site does not do this, speak to your tutor to find out why.

> Using `float` for layout like this was very common until *flexbox* was introduced.
> In general, `float` is not a good idea for layouts, `flex` or `grid` is *always* much better.

## Use flexbox to achieve a similar result

Remove the `float: right` rule from the `nav` ruleset.
Your `main` and `nav` elements should be each on their own row.

To use flexbox, we will need to adjust the structure of the HTML because flexbox needs to be applied to the containing element.
We can't set the `display` property of the `body` element because this would organise the header too (though you could try using `flex-wrap` for this).

Convert your `main` element into a `section` element and wrap the `nav` and the `section` in a new `main` element.

```html
<main>
  <nav>
    <a href="#">Home</a>
    <a href="#">Blog</a>
    <a href="#">Gallery</a>
    <a href="#">Contact</a>
    <a href="#">About</a>
  </nav>
  <section>
    <p>
      Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
      Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
      Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
      Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
    </p>
  </section>
</main>
```

Now in your CSS file, change the selector of the `main` ruleset to `section`.
Also adjust your `overflow: auto` ruleset so it applies to sections too.
This should bring you back to a roughly similar looking page.

Now add a ruleset for `main` and make it `display: flex`.
You should see the menu and section are lined up horizontally.

You can remove the `width` rules or adjust them.

By default, flex items will shrink to fit (if they can).
In this case there is plenty of scope for the `section` to shrink.
Notice that the `nav` will stop shrinking when it hits the size of the longest link.
We can stop the `nav` from shrinking by adding `flex-shrink: 0` to its ruleset.
This will force it to obey any `width` (or better, `flex-basis`) rules you give it.

Notice that the order in the HTML is determining the order within the flex container.
This can be overcome in two main ways.
Either set the `order` property of the `nav` to `2` or set the `flex-direction` property of the `main` to `row-reverse`;

## Add a simple JavaScript interaction

We will end with a bit more JavaScript.
We want to write some code that will be triggered when a particular event fires.
In this case we will handle the `click` event of an element.

First, create a file `scripts.js` and add a `script` element into your document **inside** the `body` element, after your `main` element.

```html
<script src="scripts.js"></script>
```

Write a function that does something that you will be able to detect in the page (or in the developer console) somehow.
Anything will do, for example the below function writes a simple log message to the console.
You can name your function however you like (in *lowerCamelCase* please).
In this case the function name is `greetMe`.

```js
function greetMe() {
  console.log("Hello!!");
}
```

Now we need to trigger the function to run when a `click` event fires.
So we need to access an element in the page.
The easiest way to do this is to add an element with an `id="value"` attribute into the page.
Constants will automatically be declared in the JavaScript context for all elements with **single word** (i.e. no spaces) `id` attributes.

Add an element with an `id` attribute to your document.
For example, add a second paragraph to your `section` element with a `button` element inside it.

```html
<p>
  Clicking <button id="myTrigger">here</button> should trigger the event handler.
</p>
```

Reload the page.
Notice the `button` element has the attribute `id="myTrigger"`.
This will create a global `myTrigger` variable in the JavaScript context.

Type `myTrigger` into the Chrome developer tools console.
You should see the button is identified.

We can now connect the `click` event to our event handling function by calling `addEventListener` on our `button` element.

```js
myTrigger.addEventListener('click', greetMe);
```

When the `click` event fires, the browser will call the `greetMe` function.
Though we are not using it, an object containing information about the event will be passed as an argument to our function.
Try adding an argument to the event handler function and use `console.log` to print its value to the console.

Try linking another function that sets `myTrigger.textContent` to a value of your choice.

## Validate and commit

If you got this far, well done.

Check your code with the [HTML validator](https://validator.w3.org/) before committing the code to your *lab-work* repository.
Refer to the *lab 1* instructions or ask your tutors as necessary.
Remember that to use the VSCode git integration, you would need to open the *lab-work* **folder** in VSCode.

## 02 Lab learning outcomes

- Link a stylesheet to an HTML file
- Successfully add styles to change HTML elements
- Understand basic CSS syntax and flexbox
- Use different CSS selectors to target specific tags and states
- Create HTML semantic markup that can be re-arranged using CSS
- Handle a simple user interaction using a JavaScript event listener
