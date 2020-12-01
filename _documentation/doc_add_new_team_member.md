---
author: Wesley
title: New Team Member
description: How to add a new team member
toc: true
---

# Add the person to site authors

All the site authors are stores in `_data/authors.yml` this file holds all the information to create the author profiles in the side bar, as seen below. This only needs to be done once per person.

<figure style="text-align: center;display: block;">
    <img src="/assets/images/side_bar_example.png" style="width: 40%">
</figure>

## Example
You will find examples already in the file:

``` yaml
Wesley:
  name        : "Wesley Banfield"
  # This is how you do multilines
  bio         : >
    Research Engineer passionate 
    about bringing cutting edge 
    technology to geosciences
  avatar      : "/assets/images/wesley_banfield.png"
  location    : "Aix-en-Provence, France"
  links:
    - label: "Email"
      icon: "fas fa-fw fa-envelope-square"
      url: "mailto:banfield@cerege.fr"
    - label: "Website"
      icon: "fas fa-fw fa-link"
      url: "https://wesleythegeolien.github.io/random_raves/"
    - label: "GitHub"
      icon: "fab fa-fw fa-github"
      url: "https://github.com/wesleythegeolien"
    - label: "Twitter"
      icon: "fab fa-fw fa-twitter-square"
      url: "https://twitter.com/banfieldwesley"
    - label: "LinkedIn"
      icon: "fab fa-fw fa-linkedin"
      url: "https://www.linkedin.com/in/wesleybanfield/"
```

## Set lookup name
The first line is used to define a unique name that can be looked up, this will not be visible on the website it is only used internally, notably with `author: ` keyword in the Front Matter (Top of files).

Good practice is to use your *first name* unless there are duplicates. 

## General information
The next lines in the file is for general information.
* **name** is the name that will be shown
* **bio** a short text that talks about yourself, this is shown underneath your name in the side panel
* **location** Name of Lab or city you are in
* **avatar** this is a link to the file of your profile picture. These should be placed in `assets/images/firstname_surname.EXT`. 

It is best practice not to make the avatar files massive which will slow down the loading of webpages, a couple of Mb is more than enough.
{: .notice--info}

## Links
The next part setups the links at the bottom of the panel, you can have as many as you want.
* **label** name that is shown in the sidebar
* **url** hyperlink when clicked on.
* **icon** link to an icon we use [Font awesome](https://fontawesome.com/icons?d=gallery) which have a lot of choice. 

Leave the `fab fa-fw` at the start it specifies how we want the icon rendered (`fab` is the style and `fa-fw` is fixed width)
{: .notice--info}

# Create page
Now that the author profile is setup we can start creating your webpage!

## Create file
The first step is to create a new file `firstname_surname.md` in `_team` (example: `_team/wesley_banfield.md`)

`.md` is a markdown file, a lightweight markup language with plain text formatting (it is used extensively thoughout the website) see [https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) for more information
{: .notice--info}

## File contents

### Front Matter
[Front matter](https://jekyllrb.com/docs/front-matter/) is used to specify information about the file, this is not shown in the end file but used to create the website (links + magic). Front Matter is placed between `---` as in the example below.

``` yaml
---
author: Wesley
position: Research Engineer
type: engineer
title: " "
header:
    overlay_image: "/assets/images/background_wesley_banfield.jpeg"
    # overlay_color: "#5e616c"
excerpt: " " # This is to remove the content from the image
---
```

* **author** refers to the key we setup in the `_data/authors.yml` file, so it should just be your firstname unless duplicates.
* **position** is the current position held
* **type** (used for layout in team homepage) one of:
    * fellow
    * postdoc
    * phd
    * engineer
* **title** if you want a title to appear on image, this will be a header
* **excerpt** small writing that appears in header
* **header** here you can set a link up to a background image in `assets/images` or choose a solid color.

### Contents 

Rights the contents of your file in Normal Markdown this is what is going to appear in the center of the page.