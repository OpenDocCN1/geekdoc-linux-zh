
# An Introduction to the vi Editor

| | | | | |
|---|---|---|---|---|
| md | ttusU | Dec 2 08:45 | (muller) |
| jac | ttysa | Dec 3 18:18 | (localhost) |
| eichsted | ttsyb | Dec 3 23:21 | (pc1) |
| sweett | ttysc | Dec 3 22:40 | (dov) |
| wellman | ttsyd | Dec 3 23:01 | (dov) |

Notice that a new line of information has been pulled onto the screen at the top to replace the blank line you removed.

If you try using the u command, what happens?

I'm almost done. A few presses of the Return key and I'm down to the entry for the janitor account. Using ed removes that line, too:

| | | | | |
|---|---|---|---|---|
| Dec 1 18:27 | | Dec 3 22:38 | (expert) |
| tuyhinwa | ttyRX | Dec 3 22:14 | (dov) |
| hollest | ttyrb | Nov 28 23:03 | (age) |
| holmes | ttyj | Dec 3 21:59 | (age) |
| yuxi | ttyrn | Dec 1 14:19 | (pc1) |
| frodo | ttyrc | Dec 3 22:01 | (mentor) |
| labeck | ttyrt | Dec 3 22:02 | (dov) |
| chenx2 | ttyru | Dec 3 21:53 | (mentor) |
| leungct | ttus0 | Nov 28 15:51 | (gold) |
| cdmmert | ttys5 | Dec 3 23:00 | (mentor) |
| yuenca | ttys6 | Dec 3 23:17 | (dov) |
| mathishb | ttys8 | Dec 3 18:18 | (age) |
| janitor | ttys9 | Dec 2 15:16 | (solaria) |
| cs541 | ttycC | Dec 1 14:34 | (math) |
| yansong | ttyLs | Nov 30 19:39 | (localhost) |
| md | ttusU | Dec 2 08:45 | (muller) |
| jac | ttysa | Dec 3 18:18 | (localhost) |
| eichsted | ttsyb | Dec 3 23:21 | (pc1) |
| sweett | ttysc | Dec 3 22:40 | (dov) |
| wellman | ttsyd | Dec 3 23:01 | (dov) |
| janitor | ttyse | Dec 3 23:03 | (indy) |

Each line below the one deleted moves up to fill the blank space, and a new line, moves from the following screen. I want to return to the file to remedy some of the horrendous errors! I don't really care whether I save the changes I've made to this file, so I'm going to use :q to quit, discarding these changes to the output file. Entering vi starts again:

I found myself stealing a peek at my own watch and overheard
General Catbird's
aide him the latest.
"He's not even here," went the conversation.
"Banzai."
"Where the hell is he?"
"At the hospital in El Paso."
"What? Why weren't we informed? with him?"

There are a couple of fixes you can make in short order. The first is to change the conversation on the fourth line. To move there, press the Return key twice, and then use w to forward until the cursor is at the first letter of the word you're editing:

I found myself stealing a peek at my own watch and overheard
General Catbird's
aide him the latest.
"He's not even here," went the conversation.
"Banzai."
"Where the hell is he?"

Then use the dw command:

I found myself stealing a peek at my own watch and overheard
General Catbird's
aide him the latest.
"He's not even here," went the conversation.
"Banzai."
"Where the hell is he?"

Now enter insert mode by typing i, type the correct spelling of the word, and then press Escape.

I found myself stealing a peek at my own watch and overheard
General Catbird's
aide him the latest.
"He's not even here," went the conversation.
"Banzai."
"Where the hell is he?"

6. That's one fix. Now move down a couple of lines to fix the misspelling of the hospital:

"Banzai."
"Where the hell is he?"
"At the hospital in El Paso."
"What? Why weren't we informed? with him?"

Again, dw to delete the word, type i to insert mode, type hospital, and then press Escape. Now all is well on the line:

"Banzai."
"Where the hell is he?"
"At the hospital in El Paso."
"What? Why weren't we informed? with him?"

Well, almost all is well. The first letter of Paso needs to be capitalized. Move to by typing w to move forward a few words:

"Banzai."
"Where the hell is he?"
"At the hospital in El Paso."
"What? Why weren't we informed? with him?"

7. It's time for a secret vi command! Instead of typing x to delete the letter, i to enter insert mode, p as the correct letter, and then Escape to return to command mode, there's a much faster way to transpose case: the ~ (tilde) command. Type ~ once, and here's what happens:

Correct, isn't it? Back up to the beginning of the word again, and type ~ a few times to see what happens. Notice each time you type ~, the character's case switches—transposes—and the cursor moves to the next character. Type four times, and you should end with this:

"Banzai."
"Where the hell is he?"
"At the hospital in El Paso."
"What? Why weren't we informed? with him?"

Back to the beginning of the word and type ~ until the word is correct.

8. One more slight change, and the file is fixed! Move to the last line of the file, the extra apostrophe in the word weren't, and type x to delete the offending character. The screen should now look like this:

```
I found myself stealing a peek at my own watch and overheard
General Catbird's
aide him the latest.
"He's not even here," went the conversation.
"Banzai."
"Where the hell is he?"
"At the hospital in El Paso."
"What? Why weren't we informed? with him?"
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_237_0.png)

That looks great! It's time to save it for posterity. Use :wq, a shortcut that has written out the changes and immediately quit. Not only have you learned about the variety of deletion options in vi, but you also learned a few shortcut commands: to transpose case and :wq to write out the changes and quit in one step. You should feel pleased; you're a productive and knowledgeable user, and you can modify files, making easy or tough changes. Go back to your system and experiment further, modifying some of the other files. Be careful, though, not to make changes in any of your files (for example, leave least that would be difficult to fix!).

## Searching a File

With the addition of two more capabilities, you'll be ready to face any vi expert, demonstrating your skill and knowledge of the editor, and much more, you will be able to fly through files, moving immediately to the information. The two new capabilities are for finding words or phrases in a file and moving to a specific line in it. Similar to searching for patterns in page, the / command searches forward in the file for a specified pattern, and ? searches backward for the specified pattern. To repeat the previous search, use the command to tell vi to search again in the same direction, for the next instance of the pattern. You can easily move to any line in a file, using G, or go-to-line command. If you type a number before G, the cursor will move to that line in the file. If you type G without a line number, the cursor will jump you to the very last line of the file (by default).

1. Start vi with the big output:

| | | | |
|---|---|---|---|---|
| leungtc | ttrV | Dec 1 18:27 | (magenta) |
| tuyinhwa | ttyX | Dec 3 22:38 | (expert) |
| hollenst | ttrZ | Dec 3 22:14 | (dov) |
| brandt | ttyb | Nov 28 23:03 | (age) |
| holmes | ttyj | Dec 3 21:59 | (age) |
| yuskl | ttyn | Dec 1 14:19 | (pci) |
| frodo | ttyr | Dec 3 22:01 | (mentor) |
| labeck | ttyt | Dec 3 22:02 | (dov) |
| chenitx | ttyru | Dec 3 21:53 | (mentor) |
| leungtc | tty9 | Nov 28 15:11 | (gpld) |
| chinese | ttys | Dec 3 22:53 | (excalibur) |
| cdmemert | tty5 | Dec 3 23:00 | (mentor) |
| yuenca | tty6 | Dec 3 23:00 | (mentor) |
| janitor | ttyS | Dec 2 15:18 | (age) |
| mathisb | ttysp | Dec 3 23:17 | (dov) |
| janitor | ttys | Dec 3 23:18 | (dov) |
| cs541 | ttyAc | Dec 2 15:16 | (solaria) |
| yansong | ttySl | Dec 1 14:44 | (satin) |
| mdpds | tty0 | Nov 30 19:39 | (localhost) |
| md | ttyU | Dec 2 08:45 | (muller) |
| jac | ttya | Dec 3 18:18 | (dov) |
| eichstaed | ttyba | Dec 3 23:21 | (localhost) |
| sweett | ttyc | Dec 3 22:40 | (dov) |

Remember that I used :q to quit early, so some changes were not retained. To move to the last line of the file, I go to G and see this:

| | | | | |
|---|---|---|---|
| cdmmert | ttysk | Dec 3 22:37 | (xsun) |
| jlree | ttysn | Dec 3 22:53 | (mac1) |
| fitggejs | ttyso | Dec 3 23:18 | (dov) |
| doernh | ttysp | Dec 3 23:20 | (dov) |
| cdmmert | ttysq | Dec 3 23:01 | (xsun) |
| frazierw | ttyrw | Dec 3 23:01 | (dov) |
| buckey | ttyss | Dec 3 23:20 | (mac2) |
| ntaylor | ttyst | Dec 3 23:22 | (dov) |
| took | ttysu | Dec 3 22:12 | (age) |
| janitor | ttyew | Dec 3 18:29 | (age) |
| ajones | ttysx | Dec 3 23:23 | (rassilon) |

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_239_0.png)
