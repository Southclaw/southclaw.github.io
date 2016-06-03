---
layout:     post
title:      "SA&#58;MP Crafting / Item Combination finally written!"
date:       2012-11-27 15:17:56
categories: samp
---
After much procrastinating over the past few weeks I finally wrote the code for the crafting system, it was a lot simpler than I expected! ![](http://cdn2.planetminecraft.com/files/resource_media/screenshot/1232/Crafting-Table_3191918.jpg) When I first conceived the idea I was thinking about good old Minecraft a lot and it's simple crafting mechanic, and mostly about the bits of Java code I had seen while poking around a decompiled version! If you've not played it, the crafting is pretty simple, probably derived from older systems from older games. On a workbench, there is a 3 x 3 grid, you put items in the grid either in specific sequences or just somewhere on the grid to craft things, the game works around recipes so only some items can be crafted into other items. On the coding side of things, this is pretty simple: 
    
    
    addRecipe(
     new ItemStack(Block.example, 1),
     new Object[]
      {
       "##",
       "##",
       Character.valueOf('#'), Block.dirt
      } );
    

This code is relatively simple and easy to understand when spread out like this. The first parameter is the item it will create, the second parameter is basically a string of characters that correspond to block types, in this case dirt blocks. It's a very nice system, and I almost spent a while designing some new UI but thought it was unnecessary for my usage. I wasn't basing the gameplay around this, it was just a side-feature of something more fundamental. ![](http://www.minecraftcrafting.info/imgs/craft_torch.png) Crafting a torch in minecraft I've gone for something more straightforward, and also decided to move away from the term "craft", it seemed a little out of context for my usage so I went with "combining" items. The idea is simple: two items make one item, and is defined quite easily: First we define three item types, two for "ingredients" and one for the result: 
    
    
    item_timer = DefineItemType("Timer Device", 19273, ITEM_SIZE_SMALL);
    item_explosive = DefineItemType("Explosive",  1576, ITEM_SIZE_SMALL);
    item_timebomb = DefineItemType("Time Bomb",  1252, ITEM_SIZE_SMALL);
    

Then I can simply use these three item types in this function: 
    
    
    DefineItemCombo(item_timer, item_explosive, item_timebomb);
    

The first two parameters are the two "ingredient" items and the last one is the result. This function saves the three items to a global index of "combos", this index has 3 fields of data: item1, item2, and result. When a player accesses his inventory and clicks an item he now has "Options" instead of just "Equip Item", this options menu contains "Eqiuip" and "Combine". ![](http://southclawjk.files.wordpress.com/2012/11/187ad-inv1.png) ![](http://southclawjk.files.wordpress.com/2012/11/4ad21-inv2.png) Upon clicking combine, the inventory is shown again, when another item is selected (providing it isn't the same item or an empty slot) a function called GetItemComboResult loops through the "combo-index" and checks if any of the combinations contains both item IDs that the player selected. ![](http://southclawjk.files.wordpress.com/2012/11/37ad6-inv3.png) ![](http://southclawjk.files.wordpress.com/2012/11/420cf-inv4.png) If it finds one, it returns the ID of the result, the two items are deleted from the player's inventory and and new one is added. If not, an invalid item ID is returned and the code ends. This library will be released with the upcoming "Adventure API" (When I finally get round to removing all my code dependencies and getting some documentation written!) If you want to check out the entire source for this framework, it's still in development with the other frameworks but I will be happy to share! Just email me! :)
