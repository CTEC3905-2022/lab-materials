# Lab 3: Introduction to GIT and GitHub

In this lab session we will consolidate what we have learned about the basic usage of GIT and we will introduce `remote repositories` using github.

At this point in the module we should all be getting our assignment repositories set up and cloned.
So we will go through that process too.

## The lab-solutions repository

Hopefully last weeks lab was not too difficult.
But for completeness and as an example, we have released a basic "*solution*".

The [lab-solutions repository](https://github.com/CTEC3905-2020-21/lab-solutions) in the [CTEC3905-2020-21](https://github.com/CTEC3905-2020-21) github organisation is where we will release example solutions to the lab exercises each week.

Notice that since the respository includes a `readme.md` file in the root directory, Github displays the contents of the `readme.md` file on the repository home page.

The `readme.md` file contains an index for the solutions, currently only the solution for the first lab has been released.
In future weeks, we will add more example code to the repository and more links here.

The solution for lab 1 can be viewed in three ways.

1. View the [code on github](https://github.com/CTEC3905-2020-21/lab-solutions/tree/master/lab-01) via a browser
1. View the [result in github pages](https://ctec3905-2020-21.github.io/lab-solutions/lab-01/) via the browser
1. Clone the repository onto your machine using git and play with the code directly.

Review the example code and the working webpage.
If there is anything you think needs further explanation, help others by asking a good questions about it.

# Cloning from github

Open the git command line.
If you are on Windows, use the `git bash` console.

Change the current directory to your **CTEC3905** folder:

```bash
cd path/to/CTEC3905
```

Visit the [repository page on github](https://github.com/CTEC3905-2020-21/lab-solutions).

You should see a green "Code" button.
Click the button and copy the clone url.

> If you have [setup an SSH key](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/connecting-to-github-with-ssh) on your github account then choose the SSH option, otherwise, choose HTTPS.

Cloning the github repository will create a new folder in the current location.
Make sure you are in the correct location before running this command.

> you can paste the link you copied here

```bash
git clone https://github.com/CTEC3905-2020-21/lab-solutions.git
```

>You may need to log in with your GitHub credentials at this stage

Now open **the folder** in Atom and look through the code.

## Pushing existing code to github

Now we will push your code from last week to github.
Sign in to your GitHub account and create a new repository (it should be a big green button).
Name it according to last week's code (e.g. "lab-02" or similar).

> Do not select to add a readme file or change any of the default options.
> You will be pushing your code from last week onto the blank repository

The next GitHub screen will give you the **URL for your new repository** which we’re going to use to add your files from lab-02.
Make a note of this URL or copy it

From the command prompt, inside your 02-lab repository folder, type:

```bash
git status
```

You should see that it is a git repository.

You can also check that there are no **remote** repositories by typing:

```bash
git remote -v
```

It should respond with nothing, showing that there are no remote repositories registered.

Now we can add a **remote repository** called `origin`.

```bash
git remote add origin "your_repo_url.git"
```

> Obviously (?) replace "your_repo_url.git" with the URL from step 2,

Now check that it worked by typing `git remote -v` again.
You should see your new remote listed for both `fetch` and `push`.

> `git status` will check if your repo is ready to go (if not, “add” and “commit” as in the lab-01 instructions).

Now push your code to the master branch of the `origin` repository.

```bash
git push origin master
```

Reload your repository page on GitHub and your code should have appeared

>To change the url of a remote use `git remote set-url "your_repo_url.git"`.




-----
OLD






## Set up the repo for your assignment code

Now **follow the link to the GitHub classroom under the Assessment Tab** (you may be asked to log into your GitHub account).
You must then find your P-number from the (sorry very long) list.
This will generate a repo and simple starter code in the CTEC3905 organisation.
You then need to **clone this repo to the computer on which you are working**.
This is the repo for your assignment code. This is private, so can be viewed only by you and module staff.
You can now push any work you do on your assignment to this repo.
**If you have existing code, please examine the starter files carefully** before adding any of your own code to them - they contain essential code required for the assignment.

## 03 Lab learning outcomes

- Use GIT to clone a repository from github
- use GitHub as a remote source for a local git repository
- create a usable "readme.md" file using Markdown syntax
- get your assignment code repository set up
