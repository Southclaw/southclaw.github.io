---
layout:     post
title:      "Scavenge and Survive Returns!"
date:       2013-09-22 19:28:23
categories: samp
---
Wow, that was a tiring few days. The reason the server went down for longer than expected was because it was moved to a new host network and thus new machine. This new machine has a shiny new copy of Windows Server 2012 (very much like a minimalist Windows 8) which is a nice OS but had some undesirable side effects on the server's ability to load plugins! ![](http://sites.ssis-suzhou.net/geoffderry/files/2013/04/273643-computer-rage.jpg) The one plugin that failed to load was [FileManager](http://forum.sa-mp.com/showthread.php?t=92246), by [JaTochNietDan](http://jatochnietdan.com/). This is a wonderful plugin, it allows complete control of files as well as directories offering a full range of control functions for both such as checking directories, renaming items, moving items, creating directories, etc. A valuable toolset for any complex mode that relies on files for saving data (which SS does). The plugin has two purposes in the Scavenge and Survive gamemode: 

  1. To load lists of files from directories such as saved entities (vehicles, safeboxes, defences) or object placement files for altering the environment.
  2. To check for and, if necessary, auto-create directories that the mode depends on (those in and including the "/scriptfiles/" directory)

Unfortunately, it failed to load with no reason, likely to be some internal dependency issue or compatibility problem, I still never figured out what was actually wrong! Anyway, I fixed it by downloading the source code for the File Manager plugin and compiling it on the VPS machine that Empire Bay uses, for this I used Remote Desktop Connection to control the VPS. It's similar to Teamviewer and actually not that bad lag-wise, it seems that the Remote Desktop feature has much improved over time.   So there's an explanation, apologies for the downtime and hope you enjoy the return of Scavenge and Survive :-) PS: There is a new IP address for the server due to changing host networks: **94.23.19.43**
