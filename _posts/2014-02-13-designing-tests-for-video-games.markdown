---
layout:     post
title:      "Designing Tests for Video Games"
date:       2014-02-13 17:09:41
categories: guides
---
In this article, I'll be discussing video game testing. This includes test types, issue labels, defect triggers, operating regions and testing phases. 
<!--more-->

# Types of issue

It's important to categorize issues by type so the developer can quickly know how bad a problem is and prioritize workload accordingly. Generally, there are 5 categories of problem within most software development fields, notably video games as they have more interactive and aesthetic features to consider. 

### Crash

The ever annoying CTD (crash to desktop) that usually leaves the user with no information to go on. These issues generally cause a stack/heap collision or similar memory related issue that completely ruins the stack structure resulting in memory problems cropping up all over the software. Because the entire stack/heap becomes effective this will most likely stop the program completely. ![http://abload.de/img/ctdmsu0m.gif](http://abload.de/img/ctdmsu0m.gif) San Andreas is a bit touchy about garage door models and garages. So in my Scavenge and Survive mod, carrying a certain type of barricade building material near a garage results in an instant game crash! I plan to fix this as soon as possible by disallowing players who are holding these types of model from walking near garages. ![http://i.imgur.com/uWlZmKv.png](http://i.imgur.com/uWlZmKv.png) Minecraft has always been a bit of an unstable game; mostly suffering from memory related problems. This screen would appear right after a crash of some sort. These are common on machines with low amounts of RAM (like on my old machine where I ran a 6 person server AND the game on 1GB RAM). 

### Severe

This is a little more forgiving than a crash. The problem will likely stay within the stack frame or around the same area instead of affecting the entire block resulting in a feature not working at all. It won't stop the software from working and it won't crash the process but it will most likely stop the user from being able to use the software completely. ![http://i.imgur.com/N0sJ1hul.png](http://i.imgur.com/N0sJ1hul.png) I myself have experienced this bug before but I didn't have a screen so I grabbed one from [here](https://www.youtube.com/watch?v=QCr3ydBPV0I). This is an annoying problem that results in your character falling through the game world and landing in the water below. The only way to fix this is to find somewhere to climb out (I never did, it's probably impossible) or just quit the game and reload the last saved game. ![http://i.imgur.com/Ej05Imgl.jpg](http://i.imgur.com/Ej05Imgl.jpg) Call of Duty Ghosts displayed an odd problem with the new dual-render scopes feature. Upon aiming with the scope, the optic area appears completely black. A severe issue that makes use of the scope (and thus all the rifles that use this sort of scope) very dangerous in a multiplayer game. Credit to Sethious with [this thread](http://community.callofduty.com/thread/200795376#.Uvy7Mvl_sg8) for noticing this. 

### General

Now we're moving away from the technical issues and more to just development mistakes. A general bug probably won't cause any severe memory issues or crashes but it will be very noticeable by the user. In a game, this is something that would affect their gameplay in a huge way but not completely prevent them from progressing through the game. ![http://i.imgur.com/krbS0Ztl.jpg](http://i.imgur.com/krbS0Ztl.jpg) This was a funny occurrence that happened to me while playing Left 4 Dead 2. Bill (AI controlled) got stuck under a rock and couldn't get out. It didn't stop us from playing as he teleported to us by the time we reached the safehouse however it hindered the gameplay a bit with one less gun covering our backs with hordes of zombies clawing at us! ![http://stream1.gifsoup.com/view6/20140213/4977747/dayz-crouch-walk-bug-o.gif](http://stream1.gifsoup.com/view6/20140213/4977747/dayz-crouch-walk-bug-o.gif) This is an issue in DayZ; which is expected as it's still in alpha. Crouching and walking while aiming down the sights would result in clothing popping through the camera near-clipping-plane resulting in a very distracting effect that makes aiming very difficult. This could get you killed and ruin your game session! Credit goes to [Dofazi over on youtube.](https://www.youtube.com/watch?v=EynnramD3mI)

### Minor

A minor bug is what you'd expect really, it's something small and not really significant to the end user's experience. A minor bug in a game would be something that is noticeable but that didn't affect gameplay much. ![http://i.imgur.com/fOG4WXo.jpg](http://i.imgur.com/fOG4WXo.jpg) This was an odd issue I experienced in Sanctum 2. It would have been a cosmetic bug but the model actually had a collision and almost got me killed when I tried to jump and got pushed back down because of it! Not a huge issue and rather comical but slightly irritating nonetheless. ![http://i.imgur.com/NEtqF98l.jpg](http://i.imgur.com/NEtqF98l.jpg) A common issue in DayZ: when climbing up a ladder, other players will see your character model reversed. This doesn't seem like much of an issue at first glance, rather comical in fact. However, in certain situations the body offset from the building/structure the ladder is attached to could offer an advantage or disadvantage to the player. 

### Cosmetic

Even less significant than a minor bug. Purely cosmetic and only noticeable from looking/listening. A video game example would be a missing or incorrect texture while the mesh/collision remains right, it's not going to affect the experience much apart from having a bit of a laugh at a gun plastered with some poor character's face texture map. ![http://i.imgur.com/jFsRptO.jpg](http://i.imgur.com/jFsRptO.jpg) This happened during the Arma 3 beta test. I entered a vehicle and my friend got in the passenger seat. Despite him looking directly forward on his screen, I could see him pulling a neck breaking pose. ![http://i.imgur.com/oeUKCZT.jpg](http://i.imgur.com/oeUKCZT.jpg) After being killed in Planetside 2, I noticed the fellow who took me out was missing his head! I never saw this bug again and it doesn't really have any effect on the gameplay. 

# Operating Regions

This is a categorising system for stages at which a piece of software or an element within a piece of software can operate. This method of division can help developers focus on specific areas of the software as well as distribute the development between regions. For instance, the game probably won't work if there is an issue with the _Game Start_ region so that area should be prioritised first. 

### Pre-Game

This is the period before the software is initiated. Problems here will be entirely due to external dependencies. Building the software is based on the assumption that the operating environment pre-game works completely. If this is not the case then the operating environment should be debugged until it is in working order. For a console, this would be the time while the console is activated but before the disk is inserted and the game executed. On a PC, this would be the time while the PC is idle before the application is launched. In this time period, actions that the user takes can have an effect on the operation of the software. Which is why this is an operating stage for defect classification. 

### Game Start

This period covers the time that the game is initiated until when it is ready to be played (in other words, once the menu is usable, "press start" screen appears, etc). In this time, the game executes vital code and loads all the required resources into memory. This will include the game engine core, the main menu or start screen data but not likely any level / environment data (this is typically done when the player loads a level and starts playing). There are exceptions to this for example a game that loads you straight into the game world without any sort of start screen or main menu such as the console versions of many Grand Theft Auto games. Most initiation periods display a series of branding logos / videos or an introduction cutscene relating to the game. Sometimes, game related cutscenes can't be skipped the first time the game starts. 

### In-Game

The in-game period is probably the largest region as this includes the entire time the game is being played. This involves the main menu / start screen interaction and any level preparation and loading as well as playing. 

### Post-Game

Once the game play period ends, post-game processing and unloading sequences begin. This can also include saving a player's progress in the game. Many modern games feature an auto-save functionality allowing players to quit without needing to worry about saving their progress; this cuts down on unloading/closing times 

# Games Test Life Cycle

When developing and testing, the methods must be structured to ensure a steady flow of work and communication between the team members. Tests are divided into phases and issues are given labels to help categorise things and distribute workload. 

## Testing Phases

Tests are planned and everything is documented in order to keep track of what works, what is broken and what needs testing. 

### Planning

Once a new build is available to test, the QA team will look at the changelog and determine what tests to perform on the new build. This planning stage is based on the changelog and tests will either be performed on new features. Often, new features will affect existing ones and those must also be tested to ensure something hasn't been broken by a recent change. 

### Preparing

Documentation for the tests are prepared. Developers should mark previous build issue states in case they need further testing or verification that they are fixed. The QA team can then test the issues to ensure they are fixed and close the issue. In this stage, the QA team will determine who tests what and in what environment. Sometimes different operating systems/hardware/dependencies will affect the outcome of a piece of software. 

### Performing Tests

This is the stage when the tests are performed on the new build. The team will: \- Verify that issues from the last build that were marked as 'fixed' are actually fixed. \- Test existing features that may have been affected by changes in the new build. \- Test newly added features and list defects with them. Tests should be taken from different angles to ensure the cause is pinpointed which helps the developer find and fix the source of the issue. 

### Report

Compile a report for each defect and test from the list acquired from the testing stage. A report would contain some way to reproduce a bug, details on when it does/doesn't happen as well as any other pieces of vital information that would help the developer fix it. 

### Repair

The stage where the developers look over the test reports and fix any issues. The QA team can be involved in this by offering additional feedback and work directly with the developers. Often, QA members will have some form of software/programming knowledge which helps in identifying and offering solutions for issues. 

### Repeat

Repeat the entire process for the next build. Test changes made and re-test previous issues to ensure they are fixed. 

## Issue Labels

Issues are assigned labels to help categorise them and provide fast feedback to testers or developers. Depending on the bug tracking software used, there are different sets of labels but generally the same concepts. These labels are taken from GitHub, an online service that hosts the Git version control system. 

  * BUG A bug, usually sub-categorised into the actual issue types (discussed at the top of this post).

  * DUPLICATE An issue that has already been submitted. Duplicates sometimes aren't deleted immediately in case they contain some extra information that the original issue didn't. A lead/admin can merge the duplicates into one issue.

  * ENHANCEMENT A suggested improvement to an existing feature or issue. Almost like a suggestion but generally made by a developer or tester with more in depth technical information.

  * INVALID Any sort of issue that doesn't belong in the issue report system or does not fit into another category. Labeled invalid for the QA or developer lead to check and delete.

  * QUESTION A question about a certain feature or issue. Often used for questions about undocumented API or for some more specific information on a feature for testing. Can also be used to ask if something is a bug or intentional.

  * WONTFIX Not a bug or won't be fixed due to technical limitations. Used on an issue report if it is either a false bug report of something that is intentional or on a bug that can't actually be fixed possibly due to a problem with some external dependency.




## A Test Cycle Example

![http://gametesterlife.files.wordpress.com/2012/03/bug-life-cycle11.jpg](http://gametesterlife.files.wordpress.com/2012/03/bug-life-cycle11.jpg) An issue report comes in usually as confirmed or unconfirmed. The bug must be confirmed in order to be taken any further, there is no point in developers taking their time to reproduce a bug in case it was a false report and the bug doesn't actually exist. Now that a bug has been confirmed, it is entered into the database as a new bug. The issue is now under the developer's possession meaning it's their responsibility to document any updates. The issue is assigned to a member of the development team and they address the issue and post results back into the issue system. At this point, the assignment can change depending on the outcome. If the test is inconclusive, it might be assigned to a different team member. Once the testing is complete, the issue is marked as "Resolved". Possible resolutions include: 

  * FIXED The issue is fixed and works fine.

  * DUPLICATE The issue has already been reported and processed, discard.

  * WONTFIX The bug can't or won't be fixed, either due to being an intended feature or technical limitations,

  * WORKSFORME The issue couldn't be reproduced by the tester, appears fully operational.

  * INVALID Not a bug, not a properly formatted report or not enough information.

  * REMIND Requires more testing or further inspection from another team member.

  * LATER Not a priority now, test/resolve/fix later.




Depending on the outcome of the resolution, the issue can be reopened and assigned to another tester or verified as fixed by the QA team and the issue can be closed if there are no further problems. 

# Triggers

Triggers are another way of categorising defects. More specifically, classifying the sources of problems to help developers narrow down the exact cause in order to fix a problem. When a trigger is displaying a large amount of defects in comparison to others, it may be the source of an issue and should be tested more. Here is a list of trigger categories: 

  * _Configuration_ : Settings of the software, a config file or compile flags.
  * _Startup_ : When the software is initialising and loading into memory.
  * _Exception_ : A memory or computation error happening in low level code area of the software.
  * _Stress_ : Result of a heavy load put on the software, a lot of characters on screen for example.
  * _Normal_ : A regular feature in the software.
  * _Restart_ : Performing a reset or reboot of the software.



# Testing Life Cycle

Developing a game or other piece of software is split in to three periods: 

## Pre-Alpha

The stage before development fully initiates. Software is acquired and assessed for use, dependencies are set up as well as the development environment and all required software. Tools and software specific for the project is also developed mostly in this phase. 

## Alpha

The alpha phase is the early part of development when the mechanics, architecture and fundamental elements of the project are built. In this phase, there is little need nor use for content such as models, textures and levels. This phase is mostly for laying the foundations and building frameworks for adding content later on. This phase is sometimes open for public testing but is generally behind a registration and choosing process. More technical responses and reports are desired at this point; something which the average gamer probably won't know enough about to help. An NDA (Non Disclosure Agreement) is usually enforced to keep major problems and secret features away from press coverage. 

## Beta

The beta phase is when the base of the game should be mostly completed to an extent where content can be put into it. Content includes levels, models, textures and other more game related items. Testing on this phase usually involves testing map design for holes, models for collisions, etc. This is the most common time that the public is allowed to come and test. The tests are usually less technical in comparison to alpha so regular gamers can come and report issues and suggest improvements based on the available content rather than more fundamental aspects. As well as open the game up for marketing and journalism. 

## Gold

Gold phase is release. This is when the project is completed and deemed in working order by the team. After this stage, no more changes to the software should be required as it should be in working order.
