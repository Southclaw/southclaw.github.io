---
layout:     post
title:      "Why Scavenge and Survive Development Is So Limited Right Now"
date:       2013-10-02 10:27:56
categories: samp
---
This is a topic I have been meaning to talk about for a long time now. Scavenge and Survive is going pretty good, from a end-user perspective anyway. But under the bonnet I'm digging myself into a deeper and deeper hole with every update. There's something buried deep inside the fundamental code that's just restricting me so much in terms of expanding the scope of what items can actually be used for. This problem has persisted on and on since alpha and each update I do gets me further and further from the actual solution... This has resulted in updates coming at a snail's pace! (Warning: this post is filled with technical terms such as bytes and stuff) You're probably wondering 'What is this thing? Some super complex problem that would take months to fix?', whereas it's actually rather simple. **Game Saves**! All those precious items you collected on your character, in your boxes and vehicle trunks. Each item slot takes up 8 bytes of storage in whatever file it's stored in (player inventory, safebox, tent, vehicle, etc). 
<!--more-->

# **How Does It Work Currently?**

Right now, saving is dead simple. The save code creates a string of 32-bit integers and shoves them in a file; the load code just reads this string and translates it back into items. An item is stored as two 32 bit cells: one for the item type and one for something called 'extra-data'. This extra-data is a single number that goes with the item, that's it, just one. How this number is used varies from item to item. A weapon, for example, uses this value for ammo whereas a food item will use it for it's cooked state (0 for raw, 1 for cooked) 

# **Why It Sucks**

This system is bad. It limits the amount of data that can be stored with an item a lot compared to how much data they can contain while in the game world. In server run-time, an item still has a single 32 bit cell assigned to it, but that cell can point to a much larger array stored somewhere else in memory with a lot more data about that item. This method could be referred to as a relational database. An example of this would be torsos. A torso item's extra-data points to a "Gravestone ID" a gravestone is a separate object entirely that contains data such as: player name, how they died and what time they died. This data is easily retrievable from the item's perspective as it just involves requesting the gravestone data using the item's extra-data as the ID. However, put a torso in a box over a server-restart and that number suddenly means nothing because the gravestone index has been cleared from memory. 

# **The Solution**

The solution is a simple concept however difficult to implement now that there are over _5000 user accounts registered_. This is an oversight from when I first wrote the file code, one thing I should have put in was file format version numbers. This way, I could write simple converter scripts that switched a file format to a new structure completely automatically. Aside from what's making the solution difficult, the actual solution is much easier to implement. Instead of each item consisting of two 32 bit cells, it should consist of 3 or more: 

  * The first cell is, as before, the item type.
  * Secondly, the size of the extra-data.
  * And lastly, the extra data, any amount of cells.

When the code reads the second value it knows how much to read after that. So, for instance, a torso item would save as: [101] [9] ["Southclaw"]. 101 being the torso item type ID, 9 being the total amount of extra-data cells and finally 9 text character codes. This could also be a packed string consisting of 9 bytes not just 9 cells (1 quarter of the size) This would make file sizes vary rather than be a set size. Before this idea I almost made EVERY item save with 128 cells, no more and no less; this method would have eaten into processing time and file sizes and is completely unnecessary. 

# **So, When?**

I haven't decided yet, there are a couple more small things I want to implement first such as improved building to keep players occupied. This process requires preparation to ensure all data is safe. Because this change will affect all item saving systems (inventories, vehicles, tents and boxes) it's vital that I test it all first. The conversion will be the hardest part, but luckily [I already added in the extra cell for vehicle item data](https://github.com/Southclaw/ScavengeSurvive/blob/master/gamemodes/SS/Core/Vehicle/PlayerVehicle.pwn#L316-L318)!
