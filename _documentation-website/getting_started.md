---
title: Getting started with contributing to the website
author: Wesley
excerpt: How to contribute to this website
toc: true
---

# Overview

This website is hosted using [GitHub Pages](https://pages.github.com/). GitHub Pages allows users and/or organisations to host websites for them. The code for this website is open-source meaning anyone can see it, adapt it and recopy it to use for another website.

GitHub pages can render static websites but it can also be used with other tools like [Jekyll](https://jekyllrb.com/) a tool to create websites from simple markdown and html files, this is what we have chosen to use.

To make the blog more appealing a certain amount of [preconfigured themes](https://github.com/topics/jekyll-theme) are availible. After looking through a few I decided to go with [minimal-mistakes](https://github.com/mmistakes/minimal-mistakes). Using a theme allows us to save a lot of time with some of the nitty gritty parts but being open source it also means we cna change parts of theme as we want.

# GitHub

GitHub is the defacto code storage solution used for opensource projects. It works with a command line tool called `git` which version controls files (and folders).

As the code is hosted on GitHub I recommend you create a new github account, you can sign up [here](https://github.com/join?ref_cta=Sign+up&ref_loc=header+logged+out&ref_page=%2F&source=header-home).

# Cloning the repository

Once you have your github account open a terminal and type:

```
git clone https://github.com/CEREGE-CL/CEREGE-CL.github.io.git
```

This sets up the repository, meaning it clones the latest version (at the time of execution) from the server to your machine.

# Editing files

Before editing files it is good practice to ensure you have the latest version (if you havent worked on the project in a while other collaborators could have written something / modified a file you are going to work on). 

Running 
```
git pull
```

updates your local folder with the server version.

You can now edit you files as you wish

# Pushing changes from local to server -> Updating the server

When you are happy with your changes run:
```
git commit -m "YOUR UPDATE MESSAGE GOES HERE"
```
to _save_ your changes. You now need to push your _saved_ changes to the server to do this run
```
git push
```

Your changes should now be on the server, wait a minute or two for GitHub to rebuild and then your changes should be live at [https://cerege-cl.github.io/](https://cerege-cl.github.io/).

# Viewing changes locally before pushing

It is possible to _test_ your work before deploying to the server.

Full documentaiton can be found [here](https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/testing-your-github-pages-site-locally-with-jekyll)

The installation of Jekyll and ruby should be trivial the documentation is well explained
{: .notice--info}

Building your site locally doesn't work off the bat from memory
{: .notice--info}

1. Open a terminal
1. Run `bundle install` this install all the needed packages (this step is not written in the documentation website)
1. Run `bundle exec jekyll serve` this builds your site and starts a webserver
1. Open `http://localhost:4000`

You can edit files and save them and the updates will occur automatically on the web server (you still need to refresh the page)
{: .notice--info}