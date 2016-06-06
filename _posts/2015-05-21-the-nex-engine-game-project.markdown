---
layout:     post
title:      "The 'Nex' Engine/Game Project"
date:       2015-05-21 21:11:49
categories: c++
---
In my first year of Computer Science at NTU, I decided to undertake a rather ambitious project for my end-of-year module. Despite the craziness, my lab tutor signed off the idea and agreed that it was feasible (I must say she had more faith in my C++ ability than I did back then!) so I got to work researching the idea. The project idea was to write a small game engine without ever touching a graphics library or the graphics card. This meant I had to poke the pixel data on the console window, this gave me a 320x240 canvas to play with, it took a good few weeks to get that far but once that was done, I began coding the rest of the project.
<!--more-->

I soon discovered that getting pixels to render was the easy thing, the hard part was learning all the mathematical operations I had missed out on over the years. Simple stuff like rotating a bitmap resulted in hilarious failure:

![failed rotation](https://dl.dropboxusercontent.com/u/45512231/ShareX/rot.gif)

Some great people over at Stackoverflow helped me achieve what I wanted. Since I had trouble explaining it, a gif tells a thousand words:

![rotation example](https://dl.dropboxusercontent.com/u/45512231/ShareX/rot2.gif)

Anyway, there's a lot more to say about this project (such as collision detection, the class design, the actual *game* I was going to build, etc) but I'll leave it at that for now. [The source code for this is available on my GitHub](https://github.com/Southclaw/nex-game) and one day I will "finish" it (but really, coding projects never truly finish, they just grow more ideas).

Update: In my second year of Computer Science, we learnt a lot about rendering! I decided to apply that knowledge and make my engine render polygons:

![polygon rendering](https://dl.dropboxusercontent.com/u/45512231/ShareX/triang.gif)

