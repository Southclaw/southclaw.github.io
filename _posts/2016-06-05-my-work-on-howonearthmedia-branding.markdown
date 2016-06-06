---
layout:     post
title:      "My Work on HowOnEarthMedia Branding"
date:       2016-06-05 21:36:12
categories: design
---
HowOnEarthMedia is a small media project by me and some friends. We're producing an ongoing series of videos and other internet content mostly revolved around travelling and exploring. Content ranges from skateboarding to [urban exploration](https://en.wikipedia.org/wiki/Urban_exploration) and I am currently in charge of branding the content (logos, motion graphics and the like). I'll go over some of the work I've done and some upcoming stuff in this post.
<!--more-->

![hoe-logo-final-0500](/images/hoe-logo-final-0500.png)

This logo was a collaboration between myself and my good friend [James (talented 3D artist, see his work here!)](http://www.acrvsia.com/) who came up with the original concept. Being the Illustrator ninja on the team I took the idea into Illustrator and fleshed it out into the final piece.

When I do logos, I usually stick with flat colours since that's "the craze" right now (plus they are very visually appealing, [Google's design](https://design.google.com/) pages are a great read). James' first draft included a gradient which at first I was against, "gradients are sooo 2008" but in light of the recent [Instagram logo update](http://blog.instagram.com/post/144198429587/160511-a-new-look) I grew to like the idea and was proven that it doesn't always look like a cheesy early iPhone app icon.

Once that was decided, I began working on the globe in the centre. I did a lot of experimentation with this (mostly in After Effects since I prefer the toolset and truly non-destructive workflow) but I ended up deciding to manually trace a world map with polygon shapes (3-5 sided) because I had an idea to animate it.

I usually animate logos I make to ensure they are designed with versitility in mind, if I can't think of a way to animate a logo then it's not good enough (besides, motion graphics has grown in the online and offline advertising industries so much over the past few years).

![hoe-logo-anim](/images/hoe-logo-anim.gif)

The finished product! (ignore how the gif format completely kills the gradient) Each polygon shape element of the Earth layer has this code in it's `scale` property:

{% highlight javascript %}
temp = effect("SCALE")("Slider").valueAtTime(time - (0.01 * thisProperty.propertyGroup(2).propertyIndex));
[temp, temp]
{% endhighlight %}

Which makes the value follow the value of the next element in the list with an offset of 0.01 which is what gives the Earth layer that cascading growing effect with very minimal effort (even thinking about manually animating that makes me tired...).

So there it is! Hopefully this project grows into something cool and I will continue to post behind-the-scenes content here too!
