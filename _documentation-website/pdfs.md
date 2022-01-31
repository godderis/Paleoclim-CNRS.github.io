---
title: Working with PDFs
author: Wesley
excerpt: How to embed PDF and how to open them in a new page
toc: true
---

# Embedding PDFs

Jekyll support for pdfs seems somewhat limited, we are going to use the google drive viewer to display the pdf as an `iframe`

## Instructions

1. Upload the file to Github prefereably in /assets/pdfs or some other place on the internet
1. Go to the file and copy the url eg. `https://github.com/Paleoclim-CNRS/Paleoclim-CNRS.github.io/blob/main/assets/pdf/Advertises-Engineer-2021-1.pdf`
1. Use this below code and change the pdf_url with your link

{% raw %}
```
{% assign pdf_url = 'https://github.com/Paleoclim-CNRS/Paleoclim-CNRS.github.io/blob/main/assets/pdf/Advertises-Engineer-2021-1.pdf' %}

<iframe src="https://drive.google.com/viewerng/viewer?
url={{pdf_url}}?raw=true?
pid=explorer&efh=false&a=v&chrome=false&embedded=true"/>
```
{% endraw %}
<div class='alert alert-info'>
    The `?raw=true` is only needed for Github uploaded files, documents on other websites may not work with this and it might need to be removed
</div>

# Open PDF in new tab

It is possible to create a link to open a pdf in a new tab.

## File already on the internet

If the file is already on the internet you can simply link to it as so, in fact it doesn't even need to be a PDF ...:

```
<a href="https://b792871c-a-62cb3a1a-s-sites.googlegroups.com/site/donnadieuclimate/files/ANNONCE-ERC-MAGIC.pdf?attachauth=ANoY7cpmAqegtHJa4vxbYsMVNtbjXvaC9UmVV7A18TXG9Ty0vB8QqZHsTBPqG6D21DCawoWXM3eaY6T1ExXFUckWPnPqbEWxAlN64tMBxO6-gMXjBng5zEv5P1TtqJUQi1WjrNaD-Esf_QrYCJzcp_B2jOgJbDufUP_26z0Rb11NP_mabra36wqv--E4yVMJFX3uBUlHFlQDa8VJWtHhxXlF2SD-2GV0JletlpwWsDRq17awTTDRAA4%3D&attredirects=0" target="_blank"> Some Description </a>
```
Example here: 
<a href="https://b792871c-a-62cb3a1a-s-sites.googlegroups.com/site/donnadieuclimate/files/ANNONCE-ERC-MAGIC.pdf?attachauth=ANoY7cpmAqegtHJa4vxbYsMVNtbjXvaC9UmVV7A18TXG9Ty0vB8QqZHsTBPqG6D21DCawoWXM3eaY6T1ExXFUckWPnPqbEWxAlN64tMBxO6-gMXjBng5zEv5P1TtqJUQi1WjrNaD-Esf_QrYCJzcp_B2jOgJbDufUP_26z0Rb11NP_mabra36wqv--E4yVMJFX3uBUlHFlQDa8VJWtHhxXlF2SD-2GV0JletlpwWsDRq17awTTDRAA4%3D&attredirects=0" target="_blank">Some Description </a>

<div class="alert alert-info">
    The `target="_blank"` is important and it what will open a new page.
</div>

## File on GitHub

Similar to the First part:

1. Upload the file to Github prefereably in /assets/pdfs or some other place on the internet
1. Go to the file and copy the url eg. `https://github.com/Paleoclim-CNRS/Paleoclim-CNRS.github.io/blob/main/assets/pdf/Advertises-Engineer-2021-1.pdf`
1. Use this below code and change the pdf_url with your link

{% raw %}
```
{% assign pdf_url = 'https://github.com/Paleoclim-CNRS/Paleoclim-CNRS.github.io/blob/main/assets/pdf/Advertises-Engineer-2021-1.pdf' %}

<a src="https://drive.google.com/viewerng/viewer?
url={{pdf_url}}?raw=true?
pid=explorer&efh=false&a=v&chrome=false&embedded=true"> Some Description </a>
```
{% endraw %}

<div class='alert alert-info'>
    The `?raw=true` is only needed for Github uploaded files, documents on other websites may not work with this and it might need to be removed
</div>
