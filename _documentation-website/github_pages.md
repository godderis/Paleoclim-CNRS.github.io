---
title: Building a Site with GitHub pages
author: Wesley
excerpt: How to create and host web pages with GitHub pages whether it be a personal site or Documentation 
toc: true
---

# Introduction

Github allows users (even Free users) to host publically facing websites. This can be very useful to host the documentation of a given tool or create a personal website. This very website uses Github pages.

By default pages are hosted at www.XXXX.github.io but if you buy a domain name it is also possible to use that.

The [Documentation](https://pages.github.com) is excellent and should allow any user to get their site up and running. If you don't understand soemthing in this tutorial please refer to the official documentation.

Github Pages can host static websites (written in HTML) BUT using tools like [Jekyll](https://jekyllrb.com) makes blogging simple by applying templates allowing the end user to write in markdown AND NOT HTML. See [GitHub + Jekyll Docs](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll) 

Other tools like [wowchemy](https://wowchemy.com) and [Hugo](https://gohugo.io) also exist

# Tips

- When using github pages in a larger project (not just for a personal website) it is a good idea to have a branch called `gh-pages` that holds the documentation and launches the site of from this. When using it as a personal website using the `main` branch is fine.
- You can choose from a list of themes to get started:
    - [Official Themes](https://pages.github.com/themes/) These are easiest to start with
    - [Jekyll Themes on Github](https://github.com/topics/jekyll-theme)
    - [Jeykll Themes on website](https://jekyllrb.com/resources/)
    - [Hugo Themes](https://themes.gohugo.io)
    - [wowchemy Themes](https://wowchemy.com/templates/)

# Instructions

## Activating Github Pages on a Website

To create a personal / organisation website make sure to use (USERNAME_OR_ORGANISATION_NAME.github.io).

1. On the repository pages click `settings` (up the top)
1. In settings click `pages` (near the bottom on the left)
1. Choose branch and directory (leave this as `main` and `root` for a personal page but maybe something like `gh-pages` and `docs` for documentation, you will need to create them first)
1. Click save

## wowchemy

[Documentation](https://wowchemy.com/docs/getting-started/install/)

## Github pages

[Documentation](https://pages.github.com)