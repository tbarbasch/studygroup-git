# Lesson 1

## Setting up git

It's good practice to identify yourself to git so that it can keep your commits separate from those of other people. Github also uses this information to associate the commits you make with your Github account. Open up a terminal and enter the following commands, making sure to replace "email@example.com" and "Your Name" appropriately. If you don't want to make your email public, Github has [a way](https://help.github.com/articles/setting-your-email-in-git/) to get around this.

```
git config --global user.email "email@example.com"
git config --global user.name "Your Name"
```

## Obtaining a repository

Git works with things called "repositories" which are basically folders which store all of the stuff you need for your project (code, notes, papers, etc.) along with the version control history of that project. These repositories can live "locally" on your own computer, or they can be hosted on the Internet. Github is a company that hosts git repositories for you (and provides some extra nice features that we'll explore next time).

We're going to do our work in copies of this repository that you'll make and download to each of your own computers. This process of downloading a repository is called "cloning" and you use the command `git clone` to do it. You can clone this repository (`git clone https://github.com/wkearn/studygroup-git`), but it will be easier for later if you first make your own copy on Github. Github calls these copies "forks," but your fork of my repository is its own complete git repository.

So first, sign in to Github and navigate to <https://github.com/wkearn/studygroup-git>. In the upper right corner of the page, you should see a button labeled "Fork." Click that to make your own fork of this repository. By default it will be stored at `https://github.com/USERNAME/studygroup-git`, and Github should take you to that page when you've successfully made your fork.

Your repository currently lives on Github, so to get it to your own computer, you'll need to clone it down. Open up a terminal, navigate to an appropriate directory to store your repository in (let us know if you need help doing this) and type

```
git clone https://github.com/USERNAME/studygroup-git
```

and press enter, where you've replaced `USERNAME` with your Github username. I would do `git clone https://github.com/wkearn/studygroup-git`, for instance. This should show you some details about downloading various things and then return you to the prompt. If you type `ls`, you'll see a new directory called `studygroup-git` sitting there. Let us know if you see something else. Move into that directory (`cd studygroup-git`), and you'll be all set for the next stage of the lesson.

## Getting situated

Now you're in the `studygroup-git` folder. This folder holds your git repository which consists of all the files of your project (like this one, `README.md`) and a hidden folder called `.git` which stores the entire saved history of your project. You can see that it's there by using `ls -a`, but you'll never really need to do anything to the stuff in that folder. Instead, git gives you a bunch of commands for interacting with your version control history. We've seen one already, `git clone` which downloads a remote repository to your local machine.

To help keep you aware about what's going on with your version control history, git provides two commands that you'll find you probably use the most when using git. `git status` provides an overview of the status of all your files in the version control system. Try it out now. You won't see much, now because you haven't made any changes to anything, but we'll use `git status` over and over again to show what we've done.

`git log` displays the history of your project. Each change to the project, as we'll see below, gets recorded as a "commit" which has a label which is a long string of letters and numbers, an author (which comes from the user name and email that we set up earlier) and a date which records when the commit was made. There are fancier ways to use `git log` to display useful information, but for now, we'll just use `git log` to see what happens when we make commits.

## Making your first commit

There should already be a few commits that I made while setting up this lesson. For our example collaborative project, we'll compile a biography of the Study Group attendees. Open a file called `bio.txt` in your favorite text editor, and save it in the main `studygroup-git` folder of your cloned repository. To your biography file, add three lines giving

- Your name
- Your department or program

Save the file and go back to your terminal. If you run `git status` you should see `bio.txt` pop up in a section called "Untracked files." This section lists the files that are in the folder, but that you haven't told git to track yet. To do that, we need to make a commit. There are two steps to this process.

1. Use `git add` to add the file to the "staging area": `git add bio.txt`
2. Use `git commit` to commit the file to the version control history: `git commit -m "Added my bio"`

Don't worry too much about why you have to run `git add` first. If you run `git status` after `git add`, you'll see that it moves `bio.txt` to a "Changes to be committed" section. Note that in `git commit`, we passed a flag `-m` and then wrote a message `"Added my bio"`. This is the "commit message", and it's good practice to say something about what you did in the commit. If you don't use the `-m` flag, git will open up a text editor and prompt you to write your message in there. You can set which editor git opens using `git config --global code.editor EDITOR`.

Congratulations! You've made your first commit. You can run `git status` now to see that there aren't any modified files for git to worry about. `git log` will show you this commit. 

## Making a second commit

We'd also like to know everyone's programming language(s) of choice, so add that on another line in your `bio.txt` file. Now you can run through the same process again. In between, though, we'll use `git diff` to see what changes have been made to your file.

```
git add bio.txt
git diff bio.txt
git commit -m "Added my favorite programming language"
```

Good work! Now you should have a file called `bio.txt` with your name, your department/program and your favorite programming language, along with a couple of commits recording these changes. Next time we'll see how to combine these changes with those of other people and generally build up a collaborative workflow using git.

## Getting back to an older version of a file

For now, this `studygroup-git` repository is yours, so play around with adding files, making commits, checking the logs until you're comfortable with the process. The whole point of git is to store your version control history, so we'll show you how to get to an older version of a file.

If you've made changes to a file, and haven't committed the changes yet, you can use `git checkout -- <file>` where `<file>` is the name of the file whose changes you want to discard. Conveniently, when you modify a file, and run `git status`, git reminds you that `git checkout -- <file>` is the right way to discard changes.

If you have committed a bunch of changes to a file, but want to go back to an earlier version of that file, you can use `git checkout <commit>` where `<commit>` identifies the particular commit. There are a few ways to specify the commit, but the easiest is to run `git log`, find the commit that you want to go back to and write down the first 5 or so letters and numbers in the id. You don't need to write down the whole thing. For instance, the first commit in this repository is `d5fd77`, so if I use `git checkout d5fd77`, git will reset everything back to the way it was when I made that commit (which is just the README.md) file.
