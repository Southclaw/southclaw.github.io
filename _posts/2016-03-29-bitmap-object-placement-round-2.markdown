---
layout:     post
title:      "Bitmap Object Placement Round 2"
date:       2016-03-29 20:12:24
categories: samp
---
I last wrote about this proof-of-concept back in 2014 but I'm back again, this time with more knowledge! Over the past two years or so, I've been loving the Python language and the ability to quickly create prototypes for ideas then progress them to fully fledged, structured, documented projects. The amount of libraries available for Python is amazing and really makes developing easy (most of the time!).
<!--more-->
For those of you who don't know what the original project was, it was an automatic object placement script for the San Andreas Multiplayer project. I wanted to be able to place rocks, bushes and trees all over the six square kilometres of the [San Andreas](http://ian-albert.com/games/grand_theft_auto_san_andreas_maps/) map. It's one of those automation projects that results in taking longer than actually performing the task manually but is much more interesting and fun!

I recently decided to revive the [Bitmap Object Placement](/samp/2014/06/01/bitmap-object-placement.html) project and rewrite it as a set of Python scripts. You can find the end result of this project and various other fun scripts in the `./misc` directory of the [Scavenge and Survive](https://github.com/southclaw/scavengesurvive) repository.

My first objective was to mimic the functionality of the MapAndreas plugin, which uses a large (70MB!) heightmap database to lookup the height in metres at any square metre point on the map. This task was simpler than I thought, the database is simply a flat file which unwrapped the two-dimentional grid of height values into one long line, row first. That was a huge 36 million individual values which did eat RAM but it wasn't much of a problem. It could have been better but Python objects add a bunch of overhead to the existing data (partly why I used a Python Array instead of a List).

Once that was done, I could retrieve a height value for every square metre in the game. Perfect for hills and grassy planes, not so perfect for land underneath bridges and cliff overhangs but that requires a completely different process than height maps.

The next objective was to write the actual mapping part. This was pretty easy since the hard work was already done for me thanks to the [Python Imaging Library](https://pypi.python.org/pypi/Pillow/2.2.1). With this, I simply load a bitmap into memory, get the colour value for each pixel and use that colour code to decide what kind of tree to place on that square metre of land.

I still have a few small issues to fix, such as trees sometimes getting placed ontop of trees that are on the default map (and are thus included in the heightmap data) but that will just involve getting an average height difference of nearby squares and ensuring it's close to 0. The results are fantastic and a few players have already said the map looks amazing with added trees. The project went perfectly with an open source contribution made by [Kadaradam](https://github.com/kadaradam) which added an entire tree species system and chopping mechanic to the Scavenge and Survive project!
