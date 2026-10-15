Click here to view code image

```
Excerpt from "Buckaroo Banzai" by Earl MacRauch
I found myself stealing a peek at my own watch and overheard
General Catbird's
aide give him the latest.
"He's not even here," went the conversation.
```

# 4. Okay, those are the easy ones. Now it's time to see what the c command can do. In fact, it's incredibly powerful. You can change just about any range of information from the current point in the file in either direction!

To start, move to the middle of the file, where the second copy of the passage is located:

Click here to view code image

```
Excerpt from "Buckaroo Banzai" by Earl MacRauch
I found myself stealing a peek at my own watch and overheard
General Catbird's
aide give him the latest.
"He's not even here," went the conversation.
"Who?"
"Banzai."
"Where the hell is he?"
"At the hospital in El Paso."
"What? Why weren't we informed? What's wrong with him?"

aide give him the latest.
"He's not even here," went the conversation.
"Who?"
"Banzai."
"Where the hell is he?"
"At the hospital in El Paso."
"What? Why weren't we informed? What's wrong with him?"
~
~
~
~
~
"buckaroo.confused" 17 lines, 546 characters
```

Say that you want to change the word aide that the cursor is sitting on to The tall beige wall clock opted to instead. Type c and note that, as with many other commands in vi, nothing happens. Now type w to change just the current word. The screen should look like this:

Click here to view code image

```
"At the hospital in El Paso."
"What? Why weren't we informed? What's wrong with him?"

aid$ give him the latest.
"He's not even here," went the conversation.
"Who?"
"Banzai."
```

The editor has replaced the last character in the affected range to a $ so that you can see what's going to be changed when you're done. Now type The tall beige