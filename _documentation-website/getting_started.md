---
title: Getting started with contributing to the website
author: Wesley
excerpt: How to contribute to this website
toc: true
---

---
# Overview

### GitHub Pages
This website is hosted using [GitHub Pages](https://pages.github.com/). GitHub Pages allows users and/or organisations to host websites for them. The code for this website is open-source meaning anyone can see it, adapt it and recopy it to use for another website.

GitHub pages can render static websites but it can also be used with other tools like [Jekyll](https://jekyllrb.com/) a tool to create websites from simple markdown and html files, this is what we have chosen to use.

To make the blog more appealing a certain amount of [preconfigured themes](https://github.com/topics/jekyll-theme) are availible. After looking through a few I decided to go with [minimal-mistakes](https://github.com/mmistakes/minimal-mistakes). Using a theme allows us to save a lot of time with some of the nitty gritty parts but being open source it also means we cna change parts of theme as we want.

### GitHub
GitHub is the defacto code storage solution used for opensource projects. It works with a command line tool called `git` which version controls files (and folders).

As the code is hosted on GitHub I recommend you create a new github account, you can sign up [here](https://github.com/join?ref_cta=Sign+up&ref_loc=header+logged+out&ref_page=%2F&source=header-home).

---
# Set up environment to contribute to the website
### 1) GitHub configuration to be able to push changes to the distant repository

In order to be able to push your local changes to the distant repository, you will need to satisfy two conditions:
-  Having write access on GitHub (check your GitHub account is registered [here](https://github.com/CEREGE-CL/CEREGE-CL.github.io/people))

-  Having your local machine registered for GitHub:

   - If you have not created a SSH key yet on your local machine, do so:
     ```
     ssh-keygen -t ed25519 -C [YOUR_EMAIL_ADDRESS]
     ```
   
   - Copy the content of `~/.ssh/id_ed25519.pub`
   
   - In github clic your top right profile icon > clic `Settings` in the opened panel > then `SSH and GPG keys` > `New SSH key`
   
   - Add a title to reference your key (example Macbook Pro CEREGE Pierre) into `Title` window
   
   - Paste the content of the `~/.ssh/id_ed25519.pub` into `Key` window

### 2) Cloning the repository

To modify some parts of the website you will need to go through few steps.

Once you have your github account open a terminal and type:

```
git clone https://github.com/CEREGE-CL/CEREGE-CL.github.io.git
```

This sets up the repository, meaning it clones the latest version (at the time of execution) from the server to your machine.

### 3) Editing files

Before editing files it is good practice to ensure you have the latest version (if you havent worked on the project in a while other collaborators could have written something / modified a file you are going to work on). 

Running 
```
git pull
```

updates your local folder with the server version.

You can now edit your files as you wish.

### 4) Viewing changes locally before pushing

It is important to test your work before deploying it to the server.

Full documentaiton can be found [here](https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/testing-your-github-pages-site-locally-with-jekyll)

The installation of Jekyll and ruby should be trivial the documentation is well explained
{: .notice--info}

Building your site locally doesn't work off the bat from memory
{: .notice--info}

1. Open a terminal
1. Run `bundle install` this installs all the needed packages (this step is not written in the documentation website)
1. Run `bundle exec jekyll serve` this builds your site and starts a webserver
1. Open `http://localhost:4000`

You can edit files and save them and the updates will occur automatically on the web server (you still need to refresh the page)
{: .notice--info}
### 5) Pushing changes from local to server -> Updating the server

Once your good with your modifications you will need to push it on the distant repository. 
This needs 3 steps to be done:
- You can add your modified files to the *staging area* (check GitHub [doc](https://coderefinery.github.io/git-intro/04-staging-area/#the-staging-area) for more information):
  ```
  git add . # add all the edited files to the staging area
  ```
  OR
  ```
  git add [PATH_TO_FILE]/[FILE] # add a specific file
  ```

- Then you will need to commit what you added to the *staging area*:
  ```
  git commit -m "YOUR UPDATE MESSAGE GOES HERE"
  ```

- Finally to push your commit to the server:
  ```
  git push
  ```

Your changes should now be on the server, wait a minute or two for GitHub to rebuild and then your changes should be live at [https://cerege-cl.github.io/](https://cerege-cl.github.io/).
