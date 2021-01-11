# Lab 1: Getting started

In this lab session we introduce the three software tools that will be used in this module.

- [Google Chrome](https://www.google.com/intl/en_uk/chrome/) (web browser)
- [Atom](https://atom.io/) (text editor)
- [GIT](http://git-scm.com/) (version control system)

If you need to, use the links above to install the software.

## Google Chrome and the developer tools

Open Google Chrome and visit the [Atom](https://atom.io/) website.
Scroll down the page and notice the structure.
There is a menu at the top, followed by a series of distinct sections and a footer at the bottom of the page.

Press `F12` to open the developer tools panel in Chrome.
Alternatively, in the Chrome menu, select `more tools` and `developer tools`.

Under the `Elements` tab, within the developer tools panel you should find a nested structure containing all the elements of the page.
This is a developers representation of the `Document Object Model`.

Try to find elements within the nested structure that correspond to the visible parts of the page.
Notice that when elements are selected in the developer tools, they are highlighted on the page.
Also notice that the style rules of the selected element are also provided.

Find the element with `class="hero-logo-circles"`, it should contain a series of images.
Select some of the images, the animation is controlled entirely by the browser using CSS rules.

Explore the site, understand how it is structured and ask questions if you have them.

## Atom text editor

Now we are going to create our first project.

Create a folder where you will store all the module code and *within* that folder, create a folder called **lab-01**.

Its best to keep the code for each lab session separate.
We will be creating git repositories from some folders, its important to keep them distinct.

Open Atom and select `File -> Open Folder` or `ctrl+shift+O` and select your **lab-01** folder.
This should open a panel on the left side showing your empty folder.

### Create an HTML document

Create a blank file called **index.html** and be sure to save it.
Once saved, the editor will activate auto-complete snippets for HTML.
Now use your existing knowledge to create a simple page with some visible content.
You can refer to [the module slides](https://ctec3905-2020-21.github.io/splash/?file=html.md&slide=3) or [this simple tutorial](https://www.w3schools.com/html/html5_intro.asp) for guidance.

Make sure your code is properly indented.
If you have a question about this, ask it.
Its very important to develop good habits from the beginning.
Good indentation throughout your assignment code is worth 5% of the mark.
A single mistake will cost you 2.5%, multiple mistakes will cost you 5%.

Load the page into Google Chrome by opening the file in your file manager.
If Google Chrome is not your default browser, you may want to set it to be the default (at least during the course of this module).
Alternatively, with the file open in Atom, click and drag the tab at the top of the file and drop it as a new tab in Chrome (i.e. drop onto the tab container at the top of the Chrome window).

Play around a bit.
Make some changes and see how they affect your page.
Use `ctrl-R` to reload the page in your browser each time you make a change.

Check your code in the [HTML validator](https://validator.w3.org/) and correct any errors (repeat by validating each time you add more code).

### Add some CSS styles

Create a **styles.css** file and link it in your HTML file by adding this line in the HTML head section:

```html
<link rel="stylesheet" href="styles.css">
```

Add the following line to your **styles.css** file:

```css
body { background: #f99; }
```

Reload the page in Chrome.
Try some more styles in your **styles.css** file, reloading the page each time.

## Add some javascript

Create a **scripts.js** file inside a **js** folder and link to it in your HTML file just before the closing `</body>` tag like this:

```html
<script src="js/scripts.js"></script>
```

Add the following to your **scripts.js** file:

```js
alert("Hello!");
```

Reload the page in the browser.

If the above works, change it to:

```js
console.log("Hello!");
```

Reload the page, open the developer tools and check the `Console` panel (it should say “Hello!”).

## Git version control

Now we are going to create a git repository from our code.
Git allows us to make incremental improvements to our code whilst also allowing free experimentation.

Open the git command line.
If you are on windows, use the `git bash` console.

Change the current directory to you **lab-01** folder:

```bash
cd path/to/your/CTEC3905/labs/lab-01

```

Make sure you are now in the correct location and convert your folder into a git repository.

```bash
git init
```

Check the situation, you should see three untracked files.

```bash
git status
```

Make sure you **always** check your code with the [HTML validator](https://validator.w3.org/) before committing.
Try not to commit invalid code to your repository.

Before committing, git requires that we place changes into a *staging area* also known as *the index*.

Add the whole project into the staging area.

```bash
git add .
```

The last dot is important, it refers to the current folder.

Finally, commit your work to the repository with a simple message.

```bash
git commit -m "my first commit"
```

Now, make some changes to your project and repeat the steps with a new commit message.

## Conclusion

We have explored the basic workflow which we will use in this module and which you will need to use for your assignment.

- Using Atom to write HTML, CSS and JavaScript code.
- Viewing your document in Google Chrome, using the developer tools.
- Validating your code with online validators
- Committing your updates to a git repository

NOTE: if you've finished, please set up a GitHub account if you don't have one.
