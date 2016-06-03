---
layout:     post
title:      "Scavenge and Survive + SIF + modio = Revolutionary Update"
date:       2014-04-13 12:58:08
categories: binary
---
A while ago [I posted about "Why Scavenge and Survive Development Is So Limited Right Now"](http://southclawjk.wordpress.com/2013/10/02/why-scavenge-and-survive-development-is-so-limited-right-now/) and now all the problems outlined in that post have since been eradicated thanks to three significant new libraries I've written. 

# 1\. ItemArrayData (SIF extension)

This is very simple yet effective update. Instead of storing a single 32 bit cell with each item (itm_extraData in the SIF/Item library) this extension stores an array. The default size is 256 cells but each item type also has an individual array size limit to ensure that, when storing the data, space isn't wasted on data that shouldn't be there. Item array data functions can also automatically replace Get/SetItemExtraData with a simple macro in the extension script so devs (and me!) will only have to update the items that will actually utilise the array data. 

## What will it be used for in the future?

This offers infinite possibilities now. Notebooks with editable text, deeper and more advanced weapon modifications such as ammo types, advanced food and health mechanics such as degradation and rotting. 

# 2\. modio (binary file reader/writer)

Next on the list is how the data will be stored. If you haven't read about modio yet go check out the post [here](http://southclawjk.wordpress.com/2014/03/10/modio-a-binary-file-system-designed-specifically-for-modular-gamemodes/) and the repository [here](https://github.com/Southclaw/modio). modio is a file IO library at its core but abstracts away from the basic binary IO with a structured head/body style file with data blocks and tags. A data block can be named with a 4 letter (4 byte) tag and be of any size. Modularity was in mind from the start so it fits perfectly into the SS gamemode. modio requires no opening/closing of files, just one simple function call and everything else is handled in the background. 

# 3\. ItemList (SIF extension)

Now we have array data for items and a method to store them, all that's left is some way to compress items into a nice big 1 dimensional array ready for writing. An ItemList is an encodable/decodable structured list of items that contains item type, world information and array data. A list of itemids go in and a big string comes out and is written to a modio tag. The string is read, decoded and ready for access where a loop can run through the retrieved data and recreate the items accordingly. 

# How it all works together now

Very elegantly, that's how! Here's an example of a player reconnecting: 

  * Player hits the /q command after a long night of scavenging.
  * ItemList runs through their inventory and bag to generate two itemlists consisting of their items and array data (if there is any).
  * modio writes the player's character data such as health, clothes, etc in one tag ("CHAR").
  * Then stores the inventory list in another ("INV0"),
  * and finally bag data in the final tag ("BAG0").
  * Whatever other scripts will also call "modio_push" to the player file if they have any data to save.
  * modio waits for a little while to see if any more scripts are writing to the same file.
  * No? file header is generated and all the data is written to the file.

  * Player reconnects next morning.

  * modio reads his data file, loads the "CHAR" tag and applies character data.
  * The next call of "modio_read" accesses the already read data without opening the file again and loads "INV0" and "BAG0" into memory.
  * The inventory and bag data is passed to the ItemList decode function which prepares the data.
  * A loop runs through each list and creates each item with its associated array data.
  * modio waits for any other scripts that might want to read that file for tags.
  * No? modio frees the session on that file ready for another read to take up the slot (multiple modio sessions can run at once).



Expect to see very interesting use of item array data in the future! The current only use of it is to store the victim name and death reason with torsos which in itself is a nice touch that I think will make a "hitman" type job a lot easier to prove someone's death to the paying party.
