---
layout:     post
title:      "Scavenge and Survive&#58; The Next Step"
date:       2013-09-12 12:09:52
categories: samp
---
As many of you SS players probably know, I reached a major milestone recently and thus slowed down on development (which is odd as I had the longest [GitHub commit streak](https://github.com/Southclaw) or 10 days this week...), I've been exploring some other things, such as [drawing](http://southclawjk.deviantart.com/art/Wolf-Redraw-Colour-396030354), and [more drawing](http://i.imgur.com/RlObt8qh.jpg)! The time has come to start thinking about what future plans I have for SS now that I've had a bit of a rest. I've also started back at college so I don't have all the time in the world but still a good deal. ![](http://i.imgur.com/lKF9QEe.jpg)

# **Overview**

Right, onto the next step, I've had this planned for a while but the idea keeps expanding and eventually got too big for just a minor thing, now I think is the right time to start talking about it. For a while now, there has been an elusive item in the game called a [Receiver](http://scavenge-survive.wikia.com/wiki/Receiver), it's solem use is as a crafting component for some unimportant device that no one uses (Okay, not quite, it's the single most sought after device in the game) but I always thought it would make a very nice building component. The idea started with the ability to send door-codes for defences through radio channels so you can remotely operate doors. You specify a frequency for a transmitter that is separate from chat frequencies BUT there would be some counter-item to jam/intercept these transmitters. [![RadioPole](http://southclawjk.files.wordpress.com/2013/09/radiopole1.png)](http://southclawjk.files.wordpress.com/2013/09/radiopole1.png)

# **Expanding on the Idea**

I started thinking more about these recently, it would be even better to add different flavours that do different things. I would separate them up into two main categories: Transmitters and Receivers. I will rename the item actually named a "Receiver" to something more general, like "Radio Unit" then I will make different crafting combinations determine what category it falls into. For instance, you combine a "Motion Sensor" with a "Radio Unit" to get a "Motion Transmitter" then you combine a "Lantern" with a "Radio Unit" to get a "Alert Receiver", set them onto the same frequency and you end up with a player detection system! Editing the frequency will be done by using a screwdriver at the radio pole, which will bring up a dialog menu prompting you to enter a frequency between 87.5 and 108.0 just like chat frequencies. 

# **Transmit Chain**

The initial idea revolved around sending a transmit to all masts on the same frequency at the same time, but I figured a chain based transmit would be more interesting. The transmit chain will be the order of radio masts to which a message or 'packet' is sent. This order chain will be determined by the distance of the next radio mast, that way different masts can be used to manipulate the message along the route. Here is a basic list of some ideas I've had for different types of radio mast: 

  * Transmitter - Transmits when a player interacts (presses F/Enter/Whatever you have bound to interact)
  * Motion Transmitter - Transmits when someone walks near
  * Door Receiver - Opens/closes a door upon input
  * Lamp Receiver - Lights upon input
  * EMP Receiver - Emits an EMP blast upon input, reusable (unlike the EMP set of mines)
  * Transmit Delay - Delays the chain of transmitting

I have many other plans for this system and by looking at what awesome things players have been doing with the constructible defences, I think this feature will be very well received (see what I did there) and I can't wait to see what people make with it!
