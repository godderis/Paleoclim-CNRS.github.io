---
layout: splash
permalink: /resources
read_time: false
header:
  overlay_color: "#5e616c"
  overlay_image: /assets/images/mm-home-page-feature.jpg
  # actions:
  #   - label: "<i class='fas fa-download'></i> Install now"
  #     url: "/docs/quick-start-guide/"
title: Resources

feature_rowl1:
  - image_path: /assets/images/mm-customizable-feature.png
    alt: "Publications"
    title: "Publications"
    excerpt: 'Want to see the latest articles from the group come and check them out here'
    url: "/resources/publications"
    btn_label: "Read More"
    btn_class: "btn--primary"
feature_rowr1:
  - image_path: /assets/images/mm-responsive-feature.png
    alt: "Presentations"
    title: "Presentations"
    excerpt: 'Or maybe you would prefer to look at some of our presentations to see what we have been up to'
    url: "/resources/presentations"
    btn_label: "Read More"
    btn_class: "btn--primary"
feature_rowl2:
  - image_path: /assets/images/mm-responsive-feature.png
    alt: "Tools"
    title: "Tools"
    excerpt: >
      Want to know what tools we are currently using or have used in the past? Take a look at out tools sections
    url: "/resources/presentations"
    btn_label: "Read More"
    btn_class: "btn--primary"
feature_rowr2:
  - image_path: /assets/images/mm-responsive-feature.png
    alt: "Documentation"
    title: "Documentation"
    excerpt: >
      Need to know how to get things up and running? Maybe we have already encountered the problem in this case head
      over to our documentation
    url: "/resources/presentations"
    btn_label: "Read More"
    btn_class: "btn--primary"

---

{% include feature_row id="feature_rowl1" type="left" %}

{% include feature_row id="feature_rowr1" type="right" %}

{% include feature_row id="feature_rowl2" type="left" %}

{% include feature_row id="feature_rowr2" type="right" %}