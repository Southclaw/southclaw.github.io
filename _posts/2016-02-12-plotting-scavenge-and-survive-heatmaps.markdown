---
layout:     post
title:      "Plotting Scavenge and Survive Heatmaps"
date:       2016-02-12 10:32:44
categories: samp
---
Data visualisation has been an interest of mine ever since I saw a DDoS attack map ([similar to this one](http://map.norsecorp.com/)) years ago. I've always wanted to play around with the data I have from my [Scavenge and Survive](https://github.com/southclaw/scavengesurvive) project but never really delved into it until recently. Back when my language knowledge was purely Pawn, C, C++, c# and some web stuff (in that order!) I didn't really know how to output image files let alone paint on them with procedures!
<!--more-->

I once tried this a long time ago when node.js was still in its infancy, there was a handy heatmap.js library on npm which I played around with and got a very basic heatmap of where players had died on my Scavenge and Survive game server. The preparation for the data was awkward as I had no concept of grepping source files with regex.

Nowadays with Python under my belt I decided to bring this idea back to life and write a module to generate a set of maps to display static data from the Scavenge and Survive source code using [this heatmap library](http://jjguy.com/heatmap/) which I updated to Python 3 on my GitHub (oh how I love open source!). This data includes loot spawns (loot spawns are areas of the map that items spawn for players to scavenge and collect to help them survive in the game, different types items are weighted according to their value in the game).

![gtasa-blank-1.0-ss-map-heat-loot.jpg](https://dl.dropboxusercontent.com/u/45512231/SS/gtasa-blank-1.0-ss-map-heat-loot.jpg)

The above map displays loot spawns, these are lifted straight from the source code using Regular Expression searching since loot spawns are defined in-code (I do want to change this so they load from a file instead). I initially wanted something like this to visualise where I had placed loot spawns (there are over 8000, hand placed, unfortunately it couldn't be automated effectively!) so I could guage which areas needed tweaking in terms of item rarity.

![gtasa-blank-1.0-ss-map-heat-vehicle.jpg](https://dl.dropboxusercontent.com/u/45512231/SS/gtasa-blank-1.0-ss-map-heat-vehicle.jpg)

The above map displays vehicle spawn locations. These locations are far more evenly spread across the map and less dense as the loot spawns (loot spawns are pretty much in front of every door on the street, vehicles are more sparse). Luckily, the heatmap library I was using had an option for adjusting the "weight" of the points. This meant that points that were more spread out could still be connected to other points to create that flowing "blob" shape of a nice heatmap instead of lots of tiny blobs dotted around everywhere.

![gtasa-blank-1.0-ss-map-heat-objs.jpg](https://dl.dropboxusercontent.com/u/45512231/SS/gtasa-blank-1.0-ss-map-heat-objs.jpg)

Finally, this image shows just custom objects added onto the base map by the server. This data would probably benefit from having the point weights turned up a bit! This was done mainly to see if I had any areas of the map that were getting a bit dense in terms of object streaming (SA:MP object streaming is a very interesting topic, and very unique in terms of game development as far as I know). A good friend of mine does some level design for my Scavenge and Survive project in his free time and he wanted me to generate a map of his objects just so he could see what areas of the world he had made modifications to so this module came in handy for that.

![gtasa-blank-1.0-ss-map.jpg](https://dl.dropboxusercontent.com/u/45512231/SS/gtasa-blank-1.0-ss-map.jpg)

This final map is just a collection of all the data (without any heatmaps). This data includes the polygon regions I created by hand to help separate entities in the world (and may be used for spatial indexing one day) along with the region names. The circle dots represent loot spawns of various types (loot spawn types refer to the category of object that spawn there, for example civilian loot spawns will create items such as food and tools whereas police loot spawns will create weapons and body armour etc).

