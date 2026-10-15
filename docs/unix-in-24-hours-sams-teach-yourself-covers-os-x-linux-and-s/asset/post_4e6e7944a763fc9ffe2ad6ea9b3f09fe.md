
# Note

One difference to note with colon commands is that unlike with vi commands that you type in command mode, the commands you type at the colon prompt must be followed by a Return for the editor to process them. This is a typical confusion in vi, but you'll get used to it once you try it.

Table 11.1 lists the most helpful colon commands.

| Command | Function |
|---|---|
| :e filename | Stop editing the current file and edit the specified file. |
| :n | Stop editing the current file and edit the next file specified on the command line. Remember, you can always start up vi as vi *txt or similar. |
| :N | Go to the previous specified file. |
| :q | Quit the editor. |
| :q! | Quit regardless of whether any changes have occurred, overriding all warnings. |
| :r filename | Include the contents of the specified file at this position in the file that is currently being edited. |
| :w | Write the file to disk. |
| :w filename | Write the file to disk with the specified filename. |

## TABLE 11.1 Most Helpful Colon Commands

+   1. Start vi again, this time specifying a list of files to edit; vi indicates that you have specified more than one file:

```
$ vi buckaroo big.output
2 files to edit.
```

Then it clears the screen and shows you the first file:

Click here to view code image

```
I found myself stealing a peek at my own watch and overheard
General Catbird's
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
~
~
```

```
buckaroo" 9 lines, 276 characters
```

Typing the command sequence :w and pressing Return results in the file being written to disk with the current name. There’s not much to see in that case.

2. Instead, try writing to a different file, using :w newfile:

```
:w newfile
```

When you press Return, you see this:

> I found myself stealing a peek at my own watch and overheard
> General Catbird’s
> aide give him the latest.
> "He's not even here," went the conversation.
> "Who?"
> "Banzai."
> "Where the hell is he?"
> "At the hospital in El Paso."
> "What? Why weren’t we informed? What’s wrong with him?"

```
:r newfile
```

Pressing Return yields this:

Click here to view code image

```
I found myself stealing a peek at my own watch and overheard
General Catbird’s
I found myself stealing a peek at my own watch and overheard
General Catbird’s
aide give him the latest.
“He’s not even here,” went the conversation.
“Who?”
“Banzai.”
“Where the hell is he?”
“At the hospital in El Paso.”
“What? Why weren’t we informed? What’s wrong with him?”
aide give him the latest.
“He’s not even here,” went the conversation.
“Who?”
“Banzai.”
“Where the hell is he?”
“At the hospital in El Paso.”
“What? Why weren’t we informed? What’s wrong with him?”
~
~
~
~
~
~
~
```

This can be a helpful way to include files within one another or to build a file that contains lots of other files.

4. Now that I’ve garbled the file, I want to save it to a new file, buckaroo.confused:

```
~ 
:w buckaroo.confused_
```

When I press Return, I see this:

Click here to view code image

```
~ 
"buckaroo.confused" [New file] 17 lines, 546 characters
```

5. Now it’s time to move to the second file in the list of files given to vi at startup. To do this, I use the :n, or next-file, command:

```
~ 
:n_
```

Pressing Return results in the next file being brought into the editor to replace the first:

Click here to view code image

```
leungtc ttyrV Dec 1 18:27 (magenta)
tuyinhwa ttyX Dec 3 22:38 (expert)
hollenst ttyrZ Dec 3 22:14 (dov)
brandt ttyrb Nov 28 23:03 (age)
holmes ttyrj Dec 3 21:59 (age)
```

```
yuxi      ttyrn  Dec  1 14:19  (pc)
frodo     ttyro  Dec  3 22:01  (mentor)
labeck    ttyrt  Dec  3 22:02  (dov)
chenlx2   ttyru  Dec  3 21:53  (mentor)
leungtc   ttys0  Nov 28 15:11  (gold)
chinese   ttys2  Dec  3 22:53  (excalibur)
cdemmert  ttys5  Dec  3 23:00  (mentor)
yuenca    ttys6  Dec  3 23:00  (mentor)
janitor   ttys7  Dec  3 18:18  (age)
mathisbp  ttys8  Dec  3 23:17  (dov)
janitor   ttys9  Dec  3 18:18  (age)
cs541     ttysC  Dec  2 15:16  (solaria)
yansong   ttysL  Dec  1 14:44  (math)
mdps      ttysO  Nov 30 19:39  (localhost)
md        ttysU  Dec  2 08:45  (muller)
jac       ttySa  Dec  3 18:18  (localhost)
eichsted  ttysb  Dec  3 23:21  (pcl)
sweett    ttysc  Dec  3 22:40  (dov)
"big_output" 40 lines, 1659 characters
```

6. In the middle of working on this, I suddenly realize that I need to make a slight change to the recently saved buckaroo.confused file. That's where the :e command comes in handy. Using it, I can edit any other file:

```
~
~
:e buckaroo.confused_
```

I press Return and see this:

Click here to view code image

```
I found myself stealing a peek at my own watch and overheard
General Catbird's
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

That's it! You now know a considerable amount about one of the most important, and certainly most used, commands in Unix. There's more to learn (isn't there always?), but
