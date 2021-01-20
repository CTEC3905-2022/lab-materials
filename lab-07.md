# Exercise 07-lab: data APIs

- JavaScript: use `console.log()` to check your code
- HTML: [validate your code](https://validator.w3.org/) every few changes

## Introduction

This week’s lab follows on from the lecture material covering external data APIs. The [example repository](https://github.com/CTEC3905/07-lab-json-ajax) shows how to get data from Wikipedia and has 3 *GIT branches* with additional API examples.

## Task 1 - run the code and inspect it

The master branch shows how to use the public Wikipedia API.

Navigate to the folder where you store your CTEC3905 work, then:  
`git clone https://github.com/CTEC3905/07-lab-json-ajax.git`  
and change directory into the repo folder:  
`cd 07-lab-json-ajax`.

Create a new repository on your own GitHub account and copy its remote URL (from the green "Clone or Download" button) then on your command-line, change the remote to your new repo with

`git remote set-url origin YOUR_NEW_REPO` and check it with `git remote -v`.

You can then experiment with the code, make changes, and push your version to *your own account*.

## Task 2 - experiment with the code and look up API documentation

Play with the existing code and try to change some of the query parameters.

Explore the Wikipedia [API sandbox](https://en.wikipedia.org/wiki/Special:ApiSandbox#action=query&titles=Main%20Page&prop=revisions&rvprop=content&format=jsonfm).

Check the [help pages](https://en.wikipedia.org/w/api.php?action=help) for the Wikipedia API.

The master branch code runs without needing to change anything.

Read through the comments and try and understand what is happening.

Look at the `gatherData` function to see how the list of responses is formatted.

Comment in the `console.log` statement on line 41. Then inspect the JavaScript console and look through the `response` object. Locate the items that are displayed on the results page. If you copy the url shown on line 37 and enter it in your browser you can see the raw JSON data. Run it through a [JSON beautifier](https://codebeautify.org/jsonviewer) to make it more readable.

## Task 3 - Look at the different branches

First, **commit any changes you've made** and **close Atom!** When Atom runs in CloudPlayer, GIT can't store changes properly. Now reopen the exercise folder again in Atom.

Enter `git branch -a` to see the list of available branches.

Now enter `git checkout flickr` to change to the Flickr branch.

Note how the **files in your local repository have changed**. Inspect the new code and run it in the browser. Use the guide in the readme file for this branch, and follow the links to get a Flickr API key, etc.

When you're ready to check out another branch, first:

- **add** and **commit** all your changes
- close Atom
- enter `git branch -a` to see the other branches
- then `git checkout …` another branch

## 07 Lab learning outcomes

- clone a GIT repository and push it to a new repository of your own
- understand how to obtain external API data from differing APIs
- use JavaScript to parse and navigate through JSON data
- navigate between and checkout GIT branches from a cloned repository
