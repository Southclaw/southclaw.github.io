---
layout:     post
title:      "SA&#58;MP &#34;Adventure API&#34; Project"
date:       2012-11-09 15:01:11
categories: samp
---
This is something I've wanted to release/talk about for a long time! I've been planning it for a while too. On Hellfire server I've been slowly and very subtly adding in 'secrets', it all started with one of my good friends (in-game name Defiance) creating some amazing looking broken down apocalyptic areas in the game world, the original plan was a zombie survival gamemode but after the CNPC plugin was outdated and banned it never happened. Recently, I've been working a lot on actually improving this and making it a game feature, I started by making a simple item script: [youtube=http://www.youtube.com/watch?v=oAf_AdeQ7dw] I've heavily improved this and plan to create an inventory script. But the main point is this is a framework or library, designed to be easy to write scripts that incorporate the features without directly editing the code. There is a callback for pretty much every event, picking up items, putting down items, giving items to other players, using items, using items with other items etc. With these I am making a simple inventory and crafting feature. Expect a release soon (when I get the bugs ironed out!), this is so feature rich I am actually writing a wiki-page to document all the features! In total, the framework includes: 
<!--more-->

  * Button - create trigger zones activated by the F/Enter keys, useful for doors.
  * Door - create moving objects triggered by either buttons, areas or item activities.
  * Item - create world items that can be given, stored, used etc.
  * Inventory - allow multiple items to be stored/saved by a player.
  * Craft - combine items in the inventory to make new items!

With these you can create pretty much any gameplay feature you want without needing to mess around too much! Keys to open specific doors? Easy! Medkits you can use on yourself or other players? Easy! Teleports between interiors/exteriors? Easy!
