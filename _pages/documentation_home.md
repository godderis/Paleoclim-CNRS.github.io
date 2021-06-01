---
layout: splash
permalink: /documentation
read_time: false
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/mm-home-page-feature.jpg
  # actions:
  #   - label: "<i class='fas fa-download'></i> Install now"
  #     url: "/docs/quick-start-guide/"
title: Documentation
excerpt: "This is where you are going to find all of our know-how"

feature_rowl2:
  - image_path: /assets/images/mm-responsive-feature.png
    alt: "Tools"
    title: "Tools"
    excerpt: >
      Want to know what tools we are currently using or have used in the past? Take a look at out tools sections
    url: "/documentation/tools"
    btn_label: "Read More"
    btn_class: "btn--primary"
feature_rowr2:
  - image_path: /assets/images/mm-responsive-feature.png
    alt: "Website Toolkit"
    title: "Website Toolkit"
    excerpt: >
      Need to know how to get things up and running? Maybe we have already encountered the problem in this case head
      over to our documentation
    url: "/documentation/website-toolkit"
    btn_label: "Read More"
    btn_class: "btn--primary"

---

{% include feature_row id="feature_rowl2" type="left" %}

{% include feature_row id="feature_rowr2" type="right" %}