---
layout:     post
title:      "Scavenge and Survive Log Markov Chains"
date:       2016-05-22 20:12:25
categories: projects
---
This was a fun project that I've wanted to attempt for a long time. I've been a Twitter user for a number of years and like every social network, Twitter has some "just twitter" things that are pretty unique to the format and the site. One of these things is the age-old "horse_ebooks" which started the trend of using [Markov Chains](https://en.wikipedia.org/wiki/Markov_chain) to create novelty twitter accounts that automatically generate and post (sometimes) hilarious sentences.
<!--more-->
I attempted this in Python but after utterly failing to install SciPy I resorted to use the [marky_markov](https://github.com/zolrath/marky_markov) Ruby gem. Probably a good thing since I really need to write more Ruby! You can find the bot here at [@ScavengeSurvive](https://twitter.com/ScavengeSurvive).

I do however want to rewrite this. It only took an evening to write because the hard part is done for me. When building software with deadlines that is usually great but I want to learn more about Markov Chains and to an extent, natural language processing. I want to write an "English-aware" Markov Chain generator since some of the sentences don't actually make gramatical sense and I feel I can fix this with some basic rules. It doesn't need to be perfect, just a little better. I will probably write this project in Python since I'm much more fluent with that language even though I do want to get to grips with Ruby more.
