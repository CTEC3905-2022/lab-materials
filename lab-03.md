# Lab 3: Introduction to GIT and GitHub

In this lab session we will consolidate what we have learned about the basic usage of GIT and we will introduce `remote` repositories using github.

At this point in the module you should be getting your assignment repository set up and cloned.
So we will go through that process too.

## The lab-solutions repository

Hopefully last weeks lab was not too difficult.
But for completeness and as an example, we have released a basic "*solution*".

The [lab-solutions repository](https://github.com/CTEC3905-2020-21/lab-solutions) in the [CTEC3905-2020-21](https://github.com/CTEC3905-2020-21) github organisation is where we will release example solutions to the lab exercises each week.

The solution for lab-01 can be viewed in three ways.

1. View the [code on github](https://github.com/CTEC3905-2020-21/lab-solutions/tree/master/lab-01) via a browser
1. View the [result in github pages](https://ctec3905-2020-21.github.io/lab-solutions/lab-01/) via the browser
1. `Clone` the repository onto your machine using git (explanation to follow) and play with the code directly.

Review the [example code](https://github.com/CTEC3905-2020-21/lab-solutions/tree/master/lab-01) and the [working webpage](https://ctec3905-2020-21.github.io/lab-solutions/lab-01/).
If there is anything you think needs further explanation, help others by asking a good question about it.

Notice that the lab-solutions repository includes a `readme.md` file in the root directory and Github displays the contents of the `readme.md` file on [the repository home page](https://github.com/CTEC3905-2020-21/lab-solutions).
The `.md` file name indicates this file is in **markdown** format.
Markdown is a simple text format that easily converts to HTML.
> These lab materials are also written using markdown - see [github](https://github.com/CTEC3905-2020-21/lab-materials)

The `readme.md` file contains an index for the solutions, currently only the solutions for the first two labs have been released.
In future weeks, we will add more example code to the repository and more links here.

## Cloning from github

Open the git command line.
If you are on Windows, use the `git bash` console.

Change the current directory to your **CTEC3905** folder:

```bash
cd path/to/CTEC3905
```

> On **Windows** you will need to include the drive name and use backslashes rather than forward slashes.
> ```bash
> cd c:\path\to\CTEC3905
> ```


Note that if you have spaces in the path, then you will need to wrap the path in "double quotes".
```bash
cd "path/to/Front End Web Dev"
```
> or on **Windows**
> ```bash
> cd "c:\path\to\Front End Web Dev"
> ```

Visit the [lab-solutions](https://github.com/CTEC3905-2020-21/lab-solutions) repository on github.
You should see a green *Code* button.
Click the button and copy the url.

> If you have [setup an SSH key](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/connecting-to-github-with-ssh) on your github account then choose the **SSH** option, otherwise, choose **HTTPS**.

**Cloning** the github repository will create a new folder in the current location.
Make sure you are in the correct location before running this command.
>You should be at the location in which your **lab-work** folder was created (**NOT** inside the **lab-work** folder).


Clone the github repository.

```bash
git clone https://github.com/CTEC3905-2020-21/lab-solutions.git
```
> You can paste the link you copied here.

This will have created a folder called **lab-solutions** in your current directory.
Open the **folder** in Atom and look through the code.

### Remote repositories

Git repositories are linked to each other through references known as **remotes**.
A **remote** is basically just a pointer to another git repository.

Cloned repositories alays have a **remote** called `origin` pointing to the source repository.

We are going to check the remotes set up on the **lab-solutions** repository you just cloned.
They should point back to the origin.
Start by changing into the newly created directory.

```bash
cd lab-solutions
```

We can now list the remote repositories like this.

```bash
git remote -v
```

> here the *-v* means *verbose*, this shows the uris for *fetching* and *pushing* to the remote. They should be the same.

We can pull commits from remote repositories using `git pull` and push commits to remote repositories using `git push`.

However, in this case, you don't have write permissions for the **lab-solutions** repository, so you will **not** be able to `push`.

## Pushing existing code to github

If you have *existing code* then the steps to get the code onto github are slightly different.
We will use your **lab-work** repository as an example.

First, we need to create a blank repository on github.
Sign in to your GitHub account and create a new blank repository called **ctec3905-lab-work** (using the green **new** button on [github.com](github.com) or the **new repository** option in the **+** menu [top right]).
This is where you will eventually *push* your code.

> You can select either *public* or *private* but do not select to add a readme file, .gitignore or license.
> You will be pushing your code from last week into the blank repository

The next GitHub screen will give you the **URL for your new repository** which we’re going to use to add your files from lab-02.
Make a note of this URL or copy it

Now change directories up one level and into your lab-work folder.

```bash
cd ../lab-work
```

Check you are in a git repository using `git status`.

```bash
git status
```

You should see that it is a git repository.
> If not, `add` and `commit` as in the lab-01 instructions before continuing.


You can also check that there are no **remote** repositories by typing:

```bash
git remote -v
```

It should respond with nothing, showing that there are no remote repositories registered.

Now we can add a **remote repository** called `origin`.

> Obviously (?) replace "your_username" and "your_repo_url.git" to match the URL from github.

```bash
git remote add origin "https://github.com/your_username/your_repo_url.git"
```

> If you have set up SSH then it might look more like this:
> ```bash
> git remote add origin "git@github.com:your_username/your_repo_url.git"
> ```

Now check that it worked

```bash
git remote -v
```

You should see your new remote listed for both `fetch` and `push`.

Now push your code to the `master` branch of the `origin` repository.

```bash
git push origin master
```

Reload your repository page on GitHub and your code should have appeared

>To change the url of a remote repository use `git remote set-url path/to/your_repo_url.git`.

>If you had code in the github repository (e.g. you added a readme.md file) then you may have a problem at this stage. One solution is to force the push:
> ```bash
> git push -f origin master
> ```
> This would overwrite the code on github.

## Create and clone your assignment repository

You may have already created your assignment repository, if not then **follow the link to the GitHub classroom under the Assessment Tab**.
Find your P-number from the (sorry, very long) list.
This will generate a repo with simple starter code.

The repo for your assignment code is private and is owned by the CTEC3905-2020-21 organisation.
Your github user has permissions to edit it, so it can be viewed only by you and module staff.

Now **clone this repo to the computer on which you are working**.
You can now push any work you do on your assignment to this repo.

## 03 Lab learning outcomes

- Use GIT to clone a repository from github
- use GitHub as a remote source for a local git repository
- get your assignment code repository set up
