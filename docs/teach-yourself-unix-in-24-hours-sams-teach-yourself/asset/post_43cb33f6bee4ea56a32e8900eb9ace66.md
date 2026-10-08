
```
"buckaroo.confused" 16 lines, 542 characters
```

I think I'll just change the word aide that the cursor is sitting on. The tall beige wall clock opted to instead. First, I type c and note that, like many other commands in vi, nothing happens. Now I type w because I want to change just the first word. The screen should look like this:

* At the hospital in El Paso.
* What? Why weren't we informed? What's wrong with him?
* aid give him the latest.
* He's not even here," went the conversation.
* Banzai.

Again, the program has replaced the last character in the range of the change to a, so I eyeball the situation. Now I type The tall beige wall clock opted to. Once I reach the s, the editor stops overwriting characters and starts inserting them instead; the screen now looks like this:

* At the hospital in El Paso.
* What? Why weren't we informed? What's wrong with him?
* The tall beige wall clock opted to give him the latest.
* He's not even here," went the conversation.
* Banzai.

Press Escape and you're done (though you can undo the change with the u or U command, of course).

5. Tall and beige or not, this section makes no sense now, so change this entire line by using the s motion command you learned in the previous hour. First, use o to move to the beginning of the line, then type c:

* At the hospital in El Paso.
* What? Why weren't we informed? What's wrong with him?
* The tall beige wall clock opted to give him the latest.
* He's not even here," went the conversation.
* Banzai.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_259_0.png)

# Advanced vi Tricks, Tools, and Techniques

This is working. The last character changed to $. Press Escape, and the entire line is deleted:

> "At the hospital in El Paso."
> "What? Why weren't we informed? What's wrong with him?"
> "He's not even here," went the conversation.
> "Banzai."

6. There are still five lines below the current line. I could delete them and then type in the information I want, but that's primitive. Instead, the e command comes to the rescue. Move down one line, type ce, and press Return. Watch what happens:

6 lines changed

In general, you always can change the current and next lines using e followed by a Return (because the Return key is a motion key, too, remember). By prefacing the command with a number, I changed the range from two lines to five.

> You might be asking, "Why two lines?" The answer is subtle. In essence, whenever you use the e command, you change the current line plus any additional lines that might be touched by the command. Pressing Return moves the cursor to the following line; therefore, the current line (starting at the cursor location) through the following line are changed. The command probably should change just to the beginning of the following line, but that's beyond even my control!

JUST A MINUTE

Now press Tab four times, type (page 8), and then press the Escape key. The screen should look like this:

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_261_0.png)

7. What if I change my mind? That's where the u command comes in handy. Typing u once undoes the last command:

> Excerpt from "Buckaroo Banzai" by Earl MacRauch
> found myself stealing a peek at my own watch and overheard
> General Catbird's
> aide give him the latest.
> "He's not even here," went the conversation.
> "Banzai."
> "Where the hell is he?"
> "At the hospital in El Paso."
> "What? Why weren't we informed? What's wrong with him?"

> "He's not even here," went the conversation.
> "Banzai."
> "Where the hell is he?"
> "At the hospital in El Paso."
> "What? Why weren't we informed? What's wrong with him?"

5 more lines

The combination of replace and change commands adds a level of sophistication to an editor that you might have suspected only insert or delete. There's much more to cover in this hour, so don't stop now!

# Task 12.2: Numeric Repeat Prefixes

You have seen two commands that were prefixed by a number to cause a specific action. The g command, in the previous hour, moves you to the very last line of the file, unless you type a number in front. The g command moves to the specified line number. Similarly, in the previous section, you saw that typing a number before the Return key causes vi to repeat the specified number of times.

Numeric repeat prefixes are actually widely available in vi and are the missing piece of navigational tool set.

- 1. I'll move back to the top of the buckaroo.confused file. This time, I use 1g to move there, rather than a bunch of k keys or other steps. The top of the screen now looks like:

> Excerpt from "Buckaroo Banzai" by Earl MacRauch
> found myself stealing a peek at my own watch and overheard General Catbird's
> aide give him the latest.
> "He's not even here," went the conversation.

Now I'll move forward 15 times. Instead of typing w 15 times, I'll type 15w.

> Excerpt from "Buckaroo Banzai" by Earl MacRauch
> found myself stealing a peek at my own watch and overheard General Catbird's
> aide give him the latest.
> "He's not even here," went the conversation.

- 2. Now I'll move down seven lines by typing 7 and pressing Return.

> "Where the hell is he?"
> "At the hospital in El Paso."
> "What? Why weren't we informed? What's wrong with him?"

> "He's not even here," went the conversation.
> "Banzai."

# 12

Much as I try to leave this file, I'm still looking at buckaroo.confused in vi. The screen looks like this:

> Excerpt from "Buckaroo Banzai" by Earl MacRauch
> found myself stealing a peek at my own watch and overheard
> General Catbird's
> aide give him the latest.
> "He's not even here," went the conversation.
> "Banzai."
> "Where the hell is he?"
> "At the hospital in El Paso."
> "What? Why weren't we informed? What's wrong with him?"

- 3. Now I'd like to get rid of all the lines below the current line. There are many ways to do this, but I'm going to try 75dw, and the screen looks like this:

> Excerpt from "Buckaroo Banzai" by Earl Rauch
> found myself stealing a peek at my own watch and overheard
> General Catbird's
> aide give him the latest.
> "He's not even here," went the conversation.
> "Banzai."
> "Where the hell is he?"
> "At the hospital in El Paso."
> "What? Why weren't we informed? What's wrong with him?"

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_263_0.png)
