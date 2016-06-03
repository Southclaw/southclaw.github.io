---
layout:     post
title:      "Avoid '#' Concatenation For Compile-Time Text Embedding!"
date:       2013-11-16 23:23:07
categories: samp
---
I discovered this a while ago, and recently changed every colour embed code (and recently, keycodes) in Scavenge and Survive to not use '#' in embed codes. I will explain how I performed that task on ~30 files and ~180 entries in a few seconds at the end of this post. 

# Compile Time String Concatenation

Is a super useful feature built into the Pawn compiler. And is extended with the '#' character which actually turns raw text into a literal string at compile time.  However, using the '#' type concatenation to perform any sort of constant text embedding/concatenating can be very problematic because if the definitions are removed, the compiler won't throw an error and simply insert the literal text written after the '#' character. Here's an example: 
    
    
    #define COLOUR "{FFFF00}"
    print("far far away in a string "#COLOUR"somewhere");
    // Resultant string: "far far away in a string {FFFF00}somewhere"
    // (Please ignore the fact that console prints don't show colours anyway!)
    

HOWEVER! if 'COLOUR' is undefined, the resultant string would be: 
    
    
    "in a string COLOURsomewhere"
    

And upon compiling, you won't see any errors. This is how you should treat colour embedding or any other sort of compile-time text insertion: 
    
    
    #define COLOUR "{FFFF00}"
    print("far far away in a string "COLOUR"somewhere");
    

If 'COLOUR' is undefined, you will see these errors upon compiling: [code] error 001: expected token: "-string end-", but found "-identifier-" error 017: undefined symbol "COLOUR" warning 215: expression has no effect error 001: expected token: ";", but found ")" fatal error 107: too many error messages on one line [/code] 

# The Search+Replace Regular Expression

I used Sublime Text 2 to scan through my entire project folder and replace any instance of "#C_" with "C_". I used RegEx Capture and Replace, it took 1 second to replace 180 entries. Ensure your "Regular expression" setting is enabled in the "Find in folder" panel, this will give the "Find:" field regex syntax highlighting. Find: \"(C_\w+)\" Replace: "$2" Keep in mind, that's for colour defines that start with "C_". Some modes use "COLOUR_" or "COL_" so alter the Find field if needed. Hope that was helpful! This blog needed a new post after a while... I will probably post more tips and tricks in a new category at some point.
