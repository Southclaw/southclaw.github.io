---
layout:     post
title:      "Bitmap Object Placement"
date:       2014-06-01 00:09:04
categories: samp
---
A while ago I was asking around for a bitmap loader. I eventually stumbled across this plugin: http://forum.sa-mp.com/showthread.php?t=254710 which was exactly what I wanted! I decided to speed up object placement a bit for the Scavenge and Survive project as the map is still pretty bare for the intended desolate representation of what once was San Andreas. I'm pretty lazy and spending hours placing trees and bushes is not in my best interests so I wrote the bitmap object placement tool to solve that problem! 

# How does it work?

First, a virtual canvas is created across the map. This makes getting a position from a resolution easier. That library is somewhere on Gist/GitHub. Next, the EasyBMP plugin reads a bitmap file and runs some code for each pixel read. Depending on the colour of the pixel, a different model will have a chance of spawning there. Each pixel colour has a list of possible objects for instance, dark green is mostly trees and light green is brushes and shrubbery. Blue water pixels just spawn buoys at the moment. The loader supports any size bitmap since the virtual canvas abstraction means any resolution will translate to a world position. Here are some example bitmaps I used while developing this idea: 

## Example #1

[![https://i.imgur.com/oSQfU4Hl.png](https://i.imgur.com/oSQfU4Hl.png)](https://i.imgur.com/oSQfU4H.png) My first attempt. Green pixels are bushes, black pixels are trash piles. Mainly to test the virtual canvas layer. A canvas was created over bayside 900m square. The resolution of the canvas matches the image size (which is 450px) so each pixel represents 2 square metres and the virtual canvas library matches that up perfectly. 

## Example #2

[![https://i.imgur.com/ki2m52Fl.png](https://i.imgur.com/ki2m52Fl.png)](https://i.imgur.com/ki2m52F.png) This is a map of just the black pixels which is mostly roads. However, I'd rather use node data for getting road coordinates for vehicle/loot spawns as it will be more accurate. 

## Example #3

[![https://i.imgur.com/zRkpi4Ul.png](https://i.imgur.com/zRkpi4Ul.png)](https://i.imgur.com/zRkpi4U.png) This is just the foliage pixels. Different shades of green spawn different types of tree/shrub which match the region (Red County and some of Flint County have darker pixels. The lighter green pixels are the small shrub areas by roads, tree lines and the edges of fields) 

## Example #4

[![https://i.imgur.com/ZMViy0ll.png](https://i.imgur.com/ZMViy0ll.png)](https://i.imgur.com/ZMViy0l.png) I created that map using the default SA map. This one is 1000 pixels square so there isn't a pixel for each square metre in the game. The image was posterised which effectively truncates the amount of colours in the image, merging sets of pixels of similar colours to an interpolated sum of each. This gives me a flat colour to easily extract the pixel data from without needing to write the approximation code into the parser. 

## Example #5

[![https://i.imgur.com/KJrnAArl.jpg](https://i.imgur.com/KJrnAArl.jpg)](https://i.imgur.com/KJrnAAr.jpg) This version is a slightly larger posterised 6000 square image used for more precise placement. The problem with this image (The famous high resolution map from Ian Albert) is that it's shaded with a lightmap so there are light and dark areas of the same surface material. The best solution is to use the low resolution map but manually paint over it (painting is still quicker than manually placing trees!) 

# Results

The results are quite beautiful. A lush abundance of foliage reclaiming the urban areas of San Fierro and trees sprouting through crops and engulfing Flint Range Farm. It makes the ground a much darker and scarier place with trees shrouding the sky from view. Invading San Fierro [![https://i.imgur.com/oi9rtkVl.png](https://i.imgur.com/oi9rtkVl.png)](https://i.imgur.com/oi9rtkV.png) You could ambush someone from those trees! [![https://i.imgur.com/qzj9sigl.jpg](https://i.imgur.com/qzj9sigl.jpg)](https://i.imgur.com/qzj9sig.jpg) This area needs some more trees [![https://i.imgur.com/IRuyZbgl.png](https://i.imgur.com/IRuyZbgl.png)](https://i.imgur.com/IRuyZbg.png) Different pixel colours at work, farmland grows mostly bushes rather than trees. [![https://i.imgur.com/GW34TtIl.jpg](https://i.imgur.com/GW34TtIl.jpg)](https://i.imgur.com/GW34TtI.jpg) Makes dirt tracks much more mysterious... [![https://i.imgur.com/Kiyf7XAl.png](https://i.imgur.com/Kiyf7XAl.png)](https://i.imgur.com/Kiyf7XA.png) Flint Range Farm is now surrounded by trees! (Yes that's a glitchy bush on the roof) [![https://i.imgur.com/cdfzz0Vl.jpg](https://i.imgur.com/cdfzz0Vl.jpg)](https://i.imgur.com/cdfzz0V.jpg) The only downside to this is the object limit / stream range :( [![https://i.imgur.com/XpTjI4kl.png](https://i.imgur.com/XpTjI4kl.png)](https://i.imgur.com/XpTjI4k.png)

# Maps in 3D

This idea came from using bitmaps in Autodesk 3ds Max. For those of you who don't know, that's a 3D meshing, animation and rendering tool (and many other things). Bitmaps are generally used to add colouring ("textures") to 3D models but Max lets you use maps for a huge range of things. You can displace geometry (give it shape) with a bitmap. You can make light react differently in different parts of a surface. You can create shadows and highlights without even modifying the geometry of the model (bump/normal maps)! One map type will use monochrome pixel data to distribute a mesh or list of meshes across a surface. Darker pixels mean more chance of a mesh appearing at that position on the model which is determined by translating from pixel XY to mesh UV to world XY. 

# Development

I'd love to hear some ideas or discussion to push this idea further! I have already integrated MapAndreas for the height obviously but I must write a height check so huge height differences cancels object placement in case a pixel slightly overlaps a building. Texture mapping can be used for loads of things other than just object placement. Smaller in scope too, we've already seen textdraws but I always thought that was a bit gimmicky due to the textdraw limit. I'm sure this plugin has far more practical uses than just textdraws. The Virtual Canvas means you don't have to apply this to just the entire map, you can make a bitmap for a custom map or a specific area in San Andreas (like the bayside example). Code is here on GitHub: https://gist.github.com/Southclaw/16c972c8504fbc347f48 Unfinished due to lack of time and my server dying. I'll probably make a proper library out of it at some point.
