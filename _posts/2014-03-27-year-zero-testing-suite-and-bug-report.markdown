---
layout:     post
title:      "Year Zero - Testing Suite and Bug Report"
date:       2014-03-27 17:34:47
categories: projects
---
# Testing Suites

A detailed planned approach to structuring a test prior to performing the test. Confining the test to a specific area of the software resulting in a more organised procedure. These testing suites below were performed on Legendary Games' Year Zero. 

## Pre-Game Test

Original problem: Game crashes upon logging in/booting while in Firefox. Test: Log in to the game on Firefox, Chrome, Maxthon and Internet Explorer. Then log in again and turn on "remember me", then log in for a third time so the game automatically logs in. Check if issues arise in any of these circumstances. Result: Fixed. Logging in works fine on all browser with "remember me" turned off and on. ![Imgur](http://i.imgur.com/BwlWUY7.png)

## Game Start Test

Original problem: upon logging into the game, the messages list wouldn't show any updates to the game despite getting email notifications regarding game events. Test: boot up the game in a regular playing environment that is known to work. This is Firefox on Windows 7 (the same machine used to test previously). After logging in Result: Fixed. Logging in displayed the messages screen correctly with the newest messages at the top. ![Imgur](https://i.imgur.com/DxHcxm1.png)

## In-Game Test

Original problem: On some occasions, loading into 'Mountain Pass' caused texture errors and map merging from the previous map. Test: Load into 'Mountain Pass' battlefield after visiting each other location. So far, this happens after loading 'Eastern Wastes' and that map becomes merged and displays missing textures on rocks and dead units. Result: Not fixed. Loaded into the map with 4 units and 'Eastern Wastes' objects were also on the map. ![Imgur](http://i.imgur.com/YNA89ax.png)

## Post Game Test

Original problem: Closing the browser while in the 3D battlefield view crashed the browser and resulted in data loss on the account. Test: Close the game while in the battlefield on all browsers. Test on battlefields with units present and without, while terrain is and isn't disputed. Result: Fixed, no crashes were found while logging out and all data was saved properly. ![Imgur](http://i.imgur.com/Vud3udN.png)

# Bug Report

  * **Bug Type** Cosmetic (E)

  * **Details** Upon loading into the 'Mountain Approach' battlefield, some of the terrain objects had blank textures. Upon clicking some of these objects, the information panel on the left side said 'terrain' however some textureless objects had the actual name of the item that was supposed to be there. On further investigation a lot of the objects on the map just said 'terrain' in the info box (buildings, rocks and trees) even those that had textures. I also noticed there were two harvesters in the map (a broken one and a working one that I couldn't select) I returned to the map screen then entered the 'Mountain Approach' battlefield again and noticed that half the map (all the objects that didn't have proper names in the info panel and just said 'terrain') had vanished (including the working harvester). However, the objects with no texture still had no texture. I returned to the map screen once again and entered the map that I viewed before 'Mountain Approach' which was 'Eastern Waste' I noticed that this was the map that got merged with 'Mountain Approach'. When I loaded 'Eastern Waste' the ground texture was missing along with rocks and dead units. 

These screenshots show the bugged objects. ![Imgur](http://i.imgur.com/XSaXSvY.png) ![Imgur](http://i.imgur.com/F0LRfTS.png) ![Imgur](http://i.imgur.com/rx0cQa5.png) ![Imgur](http://i.imgur.com/SPit77D.png)

  * **Triggers Involved** This was a normal feature triggered problem while in runtime.

  * **Operating Region** This bug appears in the in-game region and can only be reproduced in there.

  * **Repeatability** This bug only seems repeatable by accessing the 'Mountain Pass' area for the first time. Rebooting the browser and accessing both maps results in all textures working as-expected and no map merging.



