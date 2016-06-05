---
layout:     post
title:      "Zipline in SA&#58;MP Script Overview (Part 1&#58; Line Segments)"
date:       2012-10-04 00:24:09
categories: samp
---
I recently uploaded a video of my latest creation, this one is a Zipline mod for SA:MP. Something I've wanted to do for a long while, I tried once before but couldn't get some maths right. This time, I gave it a full day of coding and finally got there, and surprisingly fast with minimal bugs (Which is a rarity for me!)
<!--more-->

Anyway, without going further, check out the video of the end result here: [youtube=http://www.youtube.com/watch?v=bdFGF7CtmpA]  So, how does it work? I'll start with the basics, which was the line part of the zipline. I actually developed this as a separate library the day before I worked on the actual zipline-y part. Basically I created a function that created a line of objects from one point to another (that object can be anything, but for the zipline I used rope), the function takes various parameters to do this: 
    
    
    The 3 start coordinates</pre>
    The 3 end coordinates
    Object model ID (The in-game item that the line will be made of)
    The model's length (to correctly space the objects apart from each other)
    3 rotation offsets, for tweaking the object rotation
    

Now, how I calculated the positions of the objects is a very long-way-around method, but it was mostly for the learning experience rather than absolute efficiency. Firstly I get the rotation and elevation angles from the start position to the end position. I now have the Z (rotation) angle which is also known as 'heading' as in which direction the object is facing and the X value, or elevation angle and a negative elevation angle could also be called the angle of depression (sadface!) I obtained the angles by using the function atan2() which is a sort of alternative for atan() when finding angles between points (I think, correct me if I'm wrong) the input values are the X Y and Z vectors of the line segment (The destination XYZ minus the origin XYZ) 
    
    
    rotation = -(atan2(VectorY, VectorX)-90.0);
    elevation = -(floatabs(atan2(floatsqroot( (2.0 * 2.0) + (2.0 * 2.0)), VectorZ))-90.0);
    

Okay, so I have these two angles, using some trigonometry functions I can "project" a new position so many units in front of the origin point of the line, this is as simple as adding the return values from these trig functions to the X Y and Z values of the new "projected" object: 
    
    
    OriginX + (distance * floatsin(rotation, degrees) * floatcos(elevation, degrees))
    OriginY + (distance * floatcos(rotation, degrees) * floatcos(elevation, degrees))
    OriginZ + (distance * floatsin(elevation, degrees))
    

The distance value there denotes how far away from the origin point the new projected position will be, all I have to do is put this through a loop, on each iteration I multiply the length of the object by the amount of iterations. The amount of iterations is a simple task of dividing the distance between the points by the length of the object, if it's a distance of 12 and the object is 4 units long, there will be 3 objects along the line. But, what happens if the distance isn't divisible into an integer? Well, if the loop is on the last iteration and creating the last object, it make the distance of the projection equal to the distance between the ends of the line segment (minus the length of the object, to make sure it fits) the last object just gets shifted back into the object before it, but the intersection is not even noticeable by z-fighting on the small rope object. In the end, the line looks something like this: [youtube=http://www.youtube.com/watch?v=ScmfPqW94kE] In part two, I will talk about how this is implemented to make the actual zipline.
