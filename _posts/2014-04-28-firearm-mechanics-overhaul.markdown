---
layout:     post
title:      "Firearm Mechanics Overhaul"
date:       2014-04-28 09:23:10
categories: samp
---
A huge update to weapons is rolling out soon which will partly change the way weapons behave as items but more importantly how they will behave in combat. Essentially, I'm outing the traditional health bar mechanics and introducing two new character mechanics: bleed rates and cripples. 
<!--more-->

# Old Weapons and Ammo

The old system simply had an item that correlated to each default GTA weapon. Each weapon had a set of data that determined the total damage done when a player was shot: 

  * Minimum range
  * Maximum range
  * Minimum damage
  * Maximum damage

When at minimum range, maximum damage was dealt; similarly at maximum range, minimum damage was dealt and in between was a simple linear algorithm. Very similar to the mechanics of Battlefield 3 or Modern Warfare 3 (not Black Ops 2 though, that had a stair-step style graph to ensure the bullets-to-kill were more controllable) 

### Basic but Functional

Anyway, this system was rather advanced for SA:MP but pretty basic in comparison to existing games. The damage model was at it's core, still the traditional **health bar** system as seen in games for decades. 

# New Weapons and Ammo

The new system completely removes the dependency for the first 47 items to be defined exactly as weapons. This system allows _any_ item to be declared a weapon-item. This just means when the item is picked up, a weapon is also given to the player (and the item is never removed, allowing for weapons to behave exactly like items do) 

### Ammunition Items

This also brings in ammunition items. Items that are declared as ammunition for specific weapon calibres; weapons are also declared with a calibre. 

### Flexibility

Not only does this make the whole system more flexible, it also means there can be multiple items using the same base weapon (default GTA weapon) but can have whole different mechanics and properties. Think a rifle that only has a magsize property of 1 so you reload after each shot (bolt-action) or an M16 that has an expanded magsize. Swapping the calibre of a gun is also possible, think re-chambering an AK47 to use a different calibre because you have more of that ammunition with you. 

# Damage Mechanics

The new damage mechanics are the most important and interesting change that's coming. The traditional health bar is gone, it will become an actual _blood bar_ and weapons won't remove huge chunks from it when fired. Yes you heard that right, weapons won't do damage any more. But keep reading... 

### Bleed Speed

When a person is shot, their blood doesn't suddenly vaporise. No, they start bleeding and the calibre, bullet type and impact velocity are all factors that affect this. Each weapon will have a muzzle velocity (MV) property and a calibre (C) property which both affect the **bleed rate** of the target: 

  * The calibre directly correlates to the bleed rate.
  * The muzzle velocity affects the range of the weapon which acts as a multiplier for the calibre.



### Example

A weapon with a high MV fires a low C round at a target 50m away. The round is barely affected by the distance but the small C results in minimal bleeding on the target. Now, a low MV weapon fires a very high C round at a target 50m away. The high C value should result in a very damaging impact however the MV means the round is affected by the distance which lowers the resulting bleed rate. However, if the target was only 10m away, the MV wouldn't really have much of an effect and the target would pretty much take the entire force from the round. 

# Gameplay Effects

This change will probably be the most significant to combat mechanics since bandages and medkits stopped giving health. Hopefully this will lengthen gunfights and make combat way more interesting. The old system pretty much meant the first person to spot their target would win as the first few shots would likely be fatal (or at least knock the target out). This will give the target time to react accordingly to an attack and fight back. More ideas include: 

  * A bleed rate for each body part (legs, arms, torso, head)
  * Bandage required for each body part when shot
  * Body part damage effects (arms affect aiming, legs affect agility, head affects consciousness)

![http://puu.sh/8qItv.jpg](http://puu.sh/8qItv.jpg)
