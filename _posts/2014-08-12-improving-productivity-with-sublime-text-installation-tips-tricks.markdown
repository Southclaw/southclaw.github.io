---
layout:     post
title:      "Improving Productivity with Sublime Text (Installation, Tips, Tricks)"
date:       2014-08-12 15:34:40
categories: guides
---
# What is Sublime Text?

In short, Sublime Text is an extremely feature-rich and customisable plain-text editor. It's customisability is powered by python scripting and there are a huge amount of extensions available. Sublime Text gives you an amazing toolset tailored to speeding up your writing workflow whether that is code, articles or just quick notes. (Fun fact: I'm writing this entire article in Sublime using an Evernote + Markdown extension) 

# A Quick Tour

Here's a quick overview of my favourite features: 

  1. Multiple selection By far my favourite feature. Place as many carets as you want, select as much text as you want. Hold the CTRL button and tap the LMB to place a caret. Or click-drag MMB to select a 'rectangle' of text. CTRL+D will select the next instance of whatever text you have selected and ALT+F3 instantly selects every instance. ![https://dl.dropboxusercontent.com/u/45512231/ShareX/features_multiselect0.gif](https://dl.dropboxusercontent.com/u/45512231/ShareX/features_multiselect0.gif) ![https://dl.dropboxusercontent.com/u/45512231/ShareX/features_multiselect1.gif](https://dl.dropboxusercontent.com/u/45512231/ShareX/features_multiselect1.gif) ![https://dl.dropboxusercontent.com/u/45512231/ShareX/features_multiselect2.gif](https://dl.dropboxusercontent.com/u/45512231/ShareX/features_multiselect2.gif)

  2. The mini-map A zoomed out version of your code that you can use to scroll around. Very handy for large files. ![https://dl.dropboxusercontent.com/u/45512231/ShareX/features_minimap.gif](https://dl.dropboxusercontent.com/u/45512231/ShareX/features_minimap.gif)

  3. Snippets Snippets are templates of commonly used phrases that you can trigger by typing a certain set of characters. For instance, I can type "ALS" and all the code for an ALS hook will be inserted. Then I can tap TAB to cycle through each editable part of the template (prefix, function name and parameters) ![https://dl.dropboxusercontent.com/u/45512231/ShareX/features_snippets.gif](https://dl.dropboxusercontent.com/u/45512231/ShareX/features_snippets.gif)

  4. Convert to tabs, tabsize, encoding and syntax buttons Okay, not exactly unique to Sublime but all handily placed at the bottom right. I code with tabs, but a lot of the time I need to push somewhere that only accepts spaces so conversion is useful. ![https://dl.dropboxusercontent.com/u/45512231/ShareX/features_tabsize.gif](https://dl.dropboxusercontent.com/u/45512231/ShareX/features_tabsize.gif)

  5. Everything is JSON, Python or XML Settings and keybinds are all stored in JSON format files and can be overwritten with user specific sets of settings. As soon as a change is made, Sublime reloads the settings and updates before your eyes! Extension scripts are written in Python and can expand the editor a lot. There's even a plugin that turns ST into an IRC client!




# Installation

Install like any other program for Windows or Linux. Personally, I went with the portable installation as I preferred keeping all the packages and user data in the installation folder. [Sublime Text site](http://sublimetext.com) The software is available for free evaluation without any restrictions or hindrance aside from a small message box that pops up when saving sometimes. I encourage you support the development of this software if possible though! 

# Pawn Extension

I created and maintain a [Pawn language pack for sublime text](https://github.com/Southclaw/pawn-sublime-language) which includes a _ton_ of useful stuff such as a build config, syntax highlighting (modified C syntax) 

## Installation

You can quickly install this if you have [Package Control](https://sublime.wbond.net/) installed. Simply open the command palette, type "Package Control: Install Package" (you won't even need to type the entire thing) and once the list has loaded, search for the ["Pawn Syntax"](https://sublime.wbond.net/packages/Pawn%20syntax) package and hit enter! [sublime.wbond.net/packages/Pawn%20syntax](https://sublime.wbond.net/packages/Pawn%20syntax) _(Open up a Package Manager panel, enter command "Package Control: Install Package" then search "Pawn Syntax" and hit enter.)_ [github.com/Southclaw/pawn-sublime-language](https://github.com/Southclaw/pawn-sublime-language) _(Install manually, drop files from the repo into ".\Sublime Text 3\Data\Packages\Pawn-Syntax\".)_

## Setup

To set up the Pawn compiler, open "Preferences &gt; Package Settings &gt; Pawn Compiler Settings &gt; Build Settings" Type the path to your Pawn compiler in the input panel that pops up, example: "C:\SA-MP\Server\pawno\" The file will be automatically named and prompt to be saved, save it in .\Sublime Text 3\Data\Packages\User\ (the save window may automatically open here anyway). ![https://dl.dropboxusercontent.com/u/45512231/ShareX/features_setup.gif](https://dl.dropboxusercontent.com/u/45512231/ShareX/features_setup.gif) The file that's generated is a ".sublime-build" file and I'll go through each line explaining what it means here. 

  * "cmd": is the command to pass. You can include compiler flags such as "-d3" in their own argument strings after this.
  * "file_regex": is a regex used to parse error/warning output. This allows you to double-click errors/warnings to jump directly to the file and line.
  * "working_dir": is the path to the directory where "pawncc.exe" is stored. This is the string that's set by your input.



## Auto-Complete Libraries

The Pawn Syntax package includes auto-complete files for all SA:MP natives as well as a lot of popular libraries. [Head over to this thread to read more about auto-complete and contribute.](http://forum.sa-mp.com/showthread.php?t=511195) ![https://dl.dropboxusercontent.com/u/45512231/ShareX/features_autocomplete.gif](https://dl.dropboxusercontent.com/u/45512231/ShareX/features_autocomplete.gif)

# Customisation

Sublime is all about customising. An immense amount of it too! Extensions of the program come in the form of "Packages" which can be installed manually or via the handy add-on Package Control. There are thousands of add-ons available for a variety of uses from programming tools and productivity like [HexViewer](https://sublime.wbond.net/packages/HexViewer) to quirky and experimental packages such as [ASCII art generator](https://sublime.wbond.net/packages/ASCII%20Decorator) or [IRC](https://sublime.wbond.net/packages/IRC). It's not just for writing code though; Sublime's tools have proved valuable in taking notes, managing lists and writing articles (such as this!) either with vanilla Sublime or with extensions such as [Evernote](https://sublime.wbond.net/packages/Evernote). 

## Mapping Keys

Key bindings are stored in JSON format inside ".sublime-keymap" files. There are default key bindings, user key bindings and package specific key binds which conveniently overwrite each other in that reverse order. In the Pawn Syntax package, I've included a small set of key bindings some of which emulate Pawno and others I just find useful: 

  * "f3": Find next
  * "f4": Find previous
  * "ctrl+r": Open the output panel (where warnings and errors appear)
  * "f5": Compile the current file
  * "pause": Cancels compilation (_very_ useful if you realise you forgot something just after compiling!)



# How I Use Sublime Text

I make use of the projects feature while writing modes as well as having two build systems. The Pawno folder and includes are treated as "global" installations meaning there is only one copy available. This prevents confusion with different versions of SA:MP and different versions of libraries. Folder Structure: (A practical example of this can be seen in the [ScavengeSurvive source](https://github.com/Southclaw/ScavengeSurvive)) 
    
    
        SAMP
        |-- pawno/
        |   |-- include/ < always stable libraries and SA:MP files (from sa-mp.com/download.php)
        |   |-- libpawnc.dll
        |   |-- pawnc.dll
        |   `-- pawncc.exe
        |
        |-- gamemode1/
        |   |-- filterscripts/
        |   |   `-- ...
        |   |
        |   |-- gamemodes
        |   |   |-- gamemode.pwn < main script, includes files from the folder below
        |   |   `-- gamemode/ < gamemode modules go here
        |   |       `-- ...
        |   |
        |   |-- scriptfiles
        |   |-- plugins
        |   |-- announce.exe
        |   |-- samp-npc.exe
        |   `-- samp-server.exe
        |
        |-- gamemode2/
        |   |-- filterscripts/
        |   |   `-- ...
        |   |
        |   |-- gamemodes
        |   |   |-- gamemode.pwn
        |   |   `-- gamemode/
        |   |       `-- ...
        |   |
        |   |-- scriptfiles
        |   |-- plugins
        |   |-- announce.exe
        |   |-- samp-npc.exe
        |   `-- samp-server.exe
        |
        `-- etc...
    

My guidelines: 

  * Only _one_ copy of the compiler and includes, no copies of the "pawno/" directory*.
  * Each gamemode has it's own folder, scriptfiles and filterscripts for that gamemode are completely separate from others.
  * "pawno/includes/" ONLY contains external dependencies, nothing created for a specific gamemode.
  * "&lt;gamemodename&gt;/gamemodes/&lt;gamemodename&gt;" contains modules for specific gamemodes.

Tips: 
  * This method allows you to have as many branches of the same project running on different versions. I sometimes download older commits of my ScavengeSurvive repository if something goes wrong on the latest version.
  * Keeping the gamemode specific scripts WITH the gamemode is just logical, if anything goes wrong I know exactly where to find it.
  * _Never_ edit external dependencies (includes) unless you really have to!

  * Multiple Build Systems:




I have two Pawn build systems on Sublime Text and two pawno folders. One is a stable installation of Pawno, SA:MP natives, YSI 3.1, etc. The second contains YSI 4.0 and SA:MP RCs if there are any. Why? I can test new dependencies but always fall back to my stable build simply by changing the build system from the Sublime Text menu and recompiling my code.
