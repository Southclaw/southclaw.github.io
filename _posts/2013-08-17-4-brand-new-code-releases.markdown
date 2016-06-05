---
layout:     post
title:      "4 &#34;Brand New&#34; Code Releases!"
date:       2013-08-17 10:19:17
categories: samp
---
Okay they aren't "brand new" as they were included in the [Scavenge and Survive source code](https://github.com/Southclaw/ScavengeSurvive) for a long time, but they aren't integrated into the gamemode in any way so I thought it would better to release them as standalone libraries. These 4 scripts are aptly named: 
<!--more-->

  * Balloon
  * Line
  * Zipline
  * Ladder

![](http://i.imgur.com/8e5YjLT.png) More explained inside...  All these releases can be found with their relative links on the [Code Releases](http://southclawjk.wordpress.com/releases/ "Code Releases" ) page. 

# Balloon

Not controllable, they just fly from one point to another, set by the constructor function. Very simple usage, each balloon consists of two game world positions, with buttons at them which activate the balloon if it is at that point. 

# Line

Generates a line of objects between start point and destination. Useful for ziplines, tunnels, police tape, funky infinite neon strips, etc. Utilised in the zipline script, this library generates a line of the specified object. In the constructor function, the object length and any offset from the centre must be defined, as well as optional parameters such as object local rotation. 

# Zipline

Create fun and useful ziplines players can use to speed across large areas quickly. Warning: does not work well with laggy players. Takes the same coordinate type parameters as Line, players can enter the zipline from any point, you can even jump from one zipline to another! 

# Ladder

Create simple ascend / descend points in your levels where players can move directly up or down. The animation isn't great and looks a bit stupid, but it's the one I thought looked best! Ladders move directly up and down on the Z, this may change in the future though, which would essentially make it the same as a zipline, just reversed! Hope whoever reads this and uses these libraries enjoys them! Any questions? Email or comment! Full release pages coming soon.
