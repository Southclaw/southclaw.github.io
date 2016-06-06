---
layout:     post
title:      "Converting to ALS 4 (Hook Method 7) Very Quickly With Regular Expressions"
date:       2013-12-29 20:00:13
categories: samp
---
A while ago, I stumbled upon the [ALS 7 topic](http://forum.sa-mp.com/showthread.php?t=441293) and I set out to convert SIF and SS to use this method but SS has 195 files alone, a search found 230 hooks _woah!_ I ain’t doing all those by hand! **Update: Fixed replacements for function calls to have compile-time #if checks and else cases.** Luckily, [Sublime Text 2](http://www.sublimetext.com/2) supports [Regular Expression](http://www.regular-expressions.info/) search and replace. So in this post, I will guide you through the regex queries needed to convert from the old ALS method to the new (faster) version. 
<!--more-->

# Regular Expressions

If you're not familiar with Regular Expressions, they are _extremely_ useful! Especially when you want to search for patterns in code. But regex isn't just a neat text-editor feature, you can grab a library and embed regex functionality into a piece of software (there are libraries for a huge variety of languages). 

# Step 1. Identify the Differences

This is an old hook: 
    
    
    public OnSomething()
    {
    	return CallLocalFunction("lib_OnSomething", "");
    }
    #if defined _ALS_OnSomething
    	#undef OnSomething
    #else
    	#define _ALS_OnSomething
    #endif
    #define OnSomething lib_OnSomething
    forward lib_OnSomething();
    

And this is a new one: 
    
    
    public OnSomething()
    {
    	#if defined lib_OnSomething
    		return lib_OnSomething();
    	#else
    		return 0;
    	#endif
    }
    #if defined _ALS_OnSomething
    	#undef OnSomething
    #else
    	#define _ALS_OnSomething
    #endif
    #define OnSomething lib_OnSomething
    #if defined lib_OnSomething
    	forward lib_OnSomething();
    #endif
    

There are two differences here: Firstly, the return line returns an actual function call instead of CallLocalFunction (read the topic about ALS7 for why): 
    
    
    return CallLocalFunction("lib_OnSomething", "");
    

becomes 
    
    
    #if defined lib_OnSomething
    	return lib_OnSomething();
    #else
    	return 0;
    #endif
    

Secondly, the forward for the new callback is nested under a compile-time #if check: 
    
    
    forward lib_OnSomething();
    

becomes 
    
    
    #if defined lib_OnSomething
    	forward lib_OnSomething();
    #endif
    

There is another thing to take into account here: hooked callbacks _may or may not_ have parameters. This means we need a regex query for catching either just an empty parameter format string or a full one with the parameters too. The parameters must be in a separate capture since those are all we need for the replacement: 
    
    
    return CallLocalFunction("lib_OnSomething", "d", arg);
    

becomes 
    
    
    #if defined lib_OnSomething
    	return lib_OnSomething(arg);
    #else
    	return 0;
    #endif
    

and 
    
    
    forward lib_OnSomething(arg);
    

becomes 
    
    
    #if defined lib_OnSomething
    	forward lib_OnSomething(arg);
    #endif
    

# Step 2. The Search Queries

The first part is the return of CallLocalFunction which is no longer needed as a simple compile time if check works. This search regex will catch functions with or without parameters: [code] return CallLocalFunction\\("([A-Za-z_][A-Za-z_0-9]*)", (""\\)|"[a-z]*", ([A-Za-z_0-9\, ]*)\\)); [/code] The second part searches specifically for a 'forward' that followed a 'define' line because not all 'forward' lines are hooks. [code] #define (On[A-Za-z_][A-Za-z_0-9]*) ([A-Za-z_]*_On[A-Za-z_0-9]*) forward [A-Za-z_][A-Za-z_0-9]*\\(([A-Za-z_0-9\, ]*)\\); [/code] You can test these out to ensure they work by just doing a simple regex search with ST2/Pawno/Notepad++ 

# Step 3. The Replacement Queries

RegEx has a feature called 'captures' which is used for search+replace. To define a capture field, part of the query is enclosed in brackets. Look at the above queries for example, the word after '#define' is the raw function name, this is captured using brackets and can be used in the replacement query. Each capture is sequentially numbered and in the replacement query these captures can be inserted with a '$' followed by the number that identifies the capture you want to insert. Note: these replacement queries were done in Sublime Text 2. In other editors, the indentation may be different. 

## Replacement 1: The return value

#### Search:

[code] return CallLocalFunction\\("([A-Za-z_][A-Za-z_0-9]*)", (""\\)|"[a-z]*", ([A-Za-z_0-9\, ]*)\\)); [/code] Replace: [code] #if defined $1 return $1($3); #else return 0; #endif [/code] The parameters use capture $3 since $2 actually surrounds the entire set of parameters including the format string and capture $3; pseudo-code example: 2:("dd", 3:(int1, int2)). 

## Replacement 2: The forwarding

Search: [code] #define (On[A-Za-z_][A-Za-z_0-9]*) ([A-Za-z_]*_On[A-Za-z_0-9]*) forward [A-Za-z_][A-Za-z_0-9]*\\(([A-Za-z_0-9\, ]*)\\); [/code] Replace: [code] #define $1 $2 #if defined $2 forward $2($3); #endif [/code] 

# Conclusion

I may have made some mistakes here and it may not be compatible with all coding styles or hooking styles. RegEx is a powerful tool though and if there are incompatibilities, play around with the expressions and reply to this post with fixes. I hope this has helped you save hours or work manually converting to ALS 7!
