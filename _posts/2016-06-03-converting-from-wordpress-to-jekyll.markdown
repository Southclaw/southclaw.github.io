---
layout:     post
title:      "Converting from Wordpress to Jekyll"
date:       2016-06-03 08:56:00
categories: projects
---
I've been meaning to start my blog up and write about code for a long time (over two years!) and part of that was meant to be writing my own blog site using [Wagtail](https://wagtail.io) (A Python Django project from Torchbox). I got pretty far with that project, a blog page, portfolio and various other things were completed but I never got around to porting my Wordpress content over and eventually stopped paying for the server.
<!--more-->
Recently I've been looking for a free blog host that supports custom domains (since I still own southclaw.net!) and GitHub Pages + Jekyll was the answer! The only thing left to do was convert my Wordpress .xml export to Jekyll markdown files. My first stop was BeautifulSoup, the Python library for walking HTML/XML/whateverotherML files. Luckily, Wordpress lays out the data quite nicely, each post or attachment is an `<item>` and the tags within it contain more information on exactly what the item is. `<wp:post_type>` shows whether it's an attachment or a post (if there are any more types, I've never used them). `<wp:status>` indicates whether the post has been published or is a draft and Jekyll supports drafts, perfect; I can transfer all those post ideas I never finished and continue to never finish them some more!

Converting the HTML to markdown was my only concern when starting this project, I wrote a node.js module for this a couple of years ago (it wasn't fully markdown or HTML compliant since I only wrote it for my own content) but I didn't fancy doing that again. Luckily, [html2text](https://pypi.python.org/pypi/html2text) exists to do that for me! Annoyingly, I used a Wordpress code highlight plugin that used BBCode syntax so I had to convert `[code lang=cpp]` using some regular expression code (it didn't help that I'd used three different syntaxes of this plugin, `[sourcecode language="cpp"]`, `[code language="cpp"]` and `[code lang=cpp]`).

Loading these items into a `Post` class was pretty trivial and writing them to `.markdown` files in `_posts` and `_drafts` was a pretty quick job. There's just one job left that's unwritten so far and that's to `wget` attachment type `<item>`s and set URLs in posts that used to point to Wordpress attachments to point to the local copies.
