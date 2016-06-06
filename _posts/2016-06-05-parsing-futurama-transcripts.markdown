---
layout:     post
title:      "Parsing Futurama Transcripts"
date:       2016-06-05 09:25:12
categories: projects
---
A friend and I are planning to start a Futurama YouTube channel since we love the show so much and both watch it almost religiously. One thing I wanted to bring to the table aside from the video editing was some tools to help us get some interesting facts about the character dialogue. I had originally thought of a very awkward way to do this involving running some kind of voice recognition engine over the episodes and getting the transcripts that way but I found that the hard work has already been done by the amazing Futurama fanbase over at [The Infosphere](https://theinfosphere.org/Episode_Transcript_Listing). Now I can concentrate on the fun part: textual analysis!
<!--more-->
The first task is to actually acquire the transcripts, with some BeautifulSoup and wget magic, I automated the download process for all 144 episodes and four straight-to-dvd movies (that includes the episodic versions of the four movies). Next, more BeautifulSoup magic will help my convert the downloaded HTML pages into some form of structure. The plan is to dump every line of dialogue into an SQLite database so I can perform SQL queries on the data.

Any Futurama fan will know my first exploit of this data: Bender's top 10 most used words from the season 2 episode "War is the H-Word". No doubt lots of interesting things will come of this. Of course I will probably make a [markov chain](/samp/2016-06-06-parsing-futurama-transcripts) bot for Twitter because that's always fun!
