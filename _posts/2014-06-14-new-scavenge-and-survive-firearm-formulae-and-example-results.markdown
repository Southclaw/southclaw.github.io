---
layout:     post
title:      "New Scavenge and Survive Firearm Formulae and Example Results!"
date:       2014-06-14 01:37:39
categories: samp
---
Fresh off the source code, I've just finished writing prototype formulas for calculating bleeding rates based on 3 prime weapon factors: muzzle velocity, bullet calibre bleed rate and distance to target. ![](http://puu.sh/9sqtY/e60edd73e0.png)

# What are those? Numbers?

In a previous post, I discussed the major changes I was making to the firearm mechanics in the game. Most notably, losing chunks of health from bullets is a thing of the past and I'm going for a completely "blood" oriented health system. I will keep this post short and add a little example for simplicity: In the gamemode now, an AK47 fires a round at 715m/s (theoretically, remember the game is technically still "hitscan"). The calibre it fires has a bleed rate of 0.19 units (this is units of health you lose every tenth of a second when bleeding). With this established information about the weapon and ammo type, lets set up a scenario: A shot is fired at a target at a distance of 50 metres. This results in a bleed rate of 0.106. This means, if you are hit by an AK47 bullet (which, in the game is actually a 5.56 round, purely so the AK and M16 can share ammo) you will start to bleed at a rate of 1.06 units of health per second. This gives you around 94 seconds to live without treating the wound. 

# The Math

You probably came here for the example to see what combat in SS will be like after the update. But if you're interested in the numbers I'll write about that too! First, lets declare our variables: "bleedrate": The base bleed rate of the bullet calibre being fired "muzzlevelocity": The velocity of the bullet as it leaves the barrel "bulletvelocity": The calculated velocity of the bullet at the specified distance. "distance": The distance between the shooter and the target "velocitydegredationrate": The velocity degradation rate (I'll explain shortly) 3 of our values are already known: bleedrate - acquired from the bullet calibre muzzlevelocity - acquired from the weapon type distance - measured between the two players 

## Velocity Degradation

The first value we need to calculate is the velocity degradation rate. This number represents how much the velocity is affected by distance and it's based on the muzzle velocity. Think of it this way: if you throw a ball really hard, it travels a lot further because it left your hand at a higher velocity. If you throw it softly then it doesn't travel very far before hitting the ground. This calculation is very simple: `velocitydegradationrate = 1 - (muzzlevelocity / 1000)` If our muzzle velocity is 715 then we get a value closer to zero because of that "1 -" and if we have a lower muzzle velocity we get a value closer to 1. 

## Bullet Velocity at Distance

Next up, we calculate the velocity of the bullet at the actual hit position not where it left the barrel. To do this, we use a basic formula that any plotter of graphs will know: `bulletvelocity = muzzlevelocity - (distance ^ velocitydegradationrate)` Because that degradation rate is in there as the power, that alters the curve of the graph line based on the previous calculation which is based on the muzzle velocity. When all this is done, a higher muzzle velocity basically means the bullet is affected by the distance a lot less than a bullet fired with a lower muzzle velocity. 

## Final Bleed Rate

Finally, we calculate the bleed rate. Now this might not be the final formula for this part as I still have to do some balance testing with players but at the moment this is how it looks: `finalbleedrate = bleedrate * (bulletvelocity / 1000.0)` I hope you found this interesting! This new model has been very interesting to write (despite doing it at ~1am). I'd love to see existing games move away from the traditional health "chunk" system, especially so-called "realistic" survival games such as DayZ where everything feels really authentic apart from the archaic injury models.
