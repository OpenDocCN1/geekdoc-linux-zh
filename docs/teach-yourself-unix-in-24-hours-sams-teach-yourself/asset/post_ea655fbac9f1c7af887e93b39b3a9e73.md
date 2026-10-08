
# An Introduction to the vi Editor

| Command | Function |
| --- | --- |
| q | Quit the editor. |
| q! | Quit regardless of whether any changes have occurred. |
| r filename | Include the contents of the specified file at this position in the file that is currently being edited. |
| w | Save the file to disk. |
| w filename | Save the file to disk with the specified filename. |

- 1. Start vi again, this time specifying more than one file on the command line; vi quickly indicates that you want to edit more than one file:
  `% vi buckaroo big.output`
  2 files to edit.
Then it clears the screen and shows you the first file:

> I found myself stealing a peek at my own watch and overheard
General Catbird's aide give him the latest.
"He's not even here," went the conversation.
"Banzai"
"Where the hell is he?"
"At the hospital in El Paso."
"What? Why weren't we informed? What's wrong with him?"

"buckaroo" 8 lines, 271 characters

Using :w results in this:

```
~~
~ "buckaroo" 8 lines, 271 characters~
```

- 2. Instead, try writing to a different file, using :newfile:

```
~~
~ :newfile~
```

When you press Return, you see this:

```
~~
~ "newfile" [New file] 8 lines, 271 characters~
```

- 3. Now pay attention to where the cursor is in the file. The :r, or read-file, command always includes the contents of the file below the current line. Just before I press Return, then, here's what my screen looks like:

```
I found myself stealing a peek at my watch and overheard
General Catbird's aide give him the latest.
"He's not even here," went the conversation.
"Banzai."
"Where the hell is he?"
"At the hospital in El Paso."
"What? Why weren't we informed? What's wrong with him?"
```

# An Introduction to the vi Editor

```
~~
~~
~~
~~
~~
:cr r newfile_
```

Pressing Return yields this:

```
I found myself stealing a peek at my own watch and overheard
General Catbird's
I found myself stealing a peek at my own watch and overheard
General Catbird's
aide give him the latest.
"He's not even here," went the conversation.
"Banzai."
"Where the hell is he?"\n"At the hospital in El Paso."
"What? Why weren't we informed? What's wrong with him?"

aide give him the latest.
"He's not even here," went the conversation.
"Banzai."
"Where the hell is he?"\n"At the hospital in El Paso."
"What? Why weren't we informed? What's wrong with him?"
```

"buckaroo.confused" 16 lines, 542 characters

This can be a helpful way to include files within one another or to build a file that contains lots of other files.

- 4. Now that I've garbled the file, I want to save it to a new file, buckaroo.confused:

```
~~
:w buckaroo.confused_
```

When I press Return, I see this:

```
~
~ "buckaroo.confused" [New file] 16 lines, 542 characters
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_249_0.png)

Older UNIX systems have a 14-character filename limit. If yours does, you see buckaroo.confu as the saved filename.

JUST A Minute

- 5. Now it's time to move to the second file in the list of files given to vi at startup.
Do this, I use the :n, or next-file, command:

```
~
:n_
```

Pressing Return results in the next file being brought into the editor to replace the first:

| leungctc | ttyV Dec 1 18:27 (magenta) |
| tuyinha | ttyX Dec 3 22:38 (expert) |
| hollenst | ttyZ Dec 3 22:14 (dov) |
| brandit | ttyB Nov 28 23:03 (age) |
| holmes | ttyY Dec 3 21:59 (age) |
| yuxi | ttyU Dec 11 14:19 (pc) |
| frodo | ttyO Dec 3 22:01 (mentor) |
| leabeck | ttyT Dec 3 22:02 (dov) |
| chenlx2 | ttyU Dec 3 21:53 (mentor) |
| leungtc | ttyU Nov 28 15:11 (gold) |
| chinese | ttyS Dec 3 22:53 (excalibur) |
| cdmmert | ttyS Dec 3 23:00 (mentor) |
| yuencga | ttyS Dec 3 23:00 (mentor) |
| janitor | ttyS Dec 3 18:18 (age) |
| mathisb | ttyS Dec 8 23:17 (dov) |
| janitor | ttyU Dec 3 16:18 (age) |
| cs541 | ttyY Dec 2 15:16 (solaria) |
| yangsong | ttyL Dec 1 14:44 (math) |
| mdps | ttyO Nov 30 19:39 (localhost) |
| md | ttyU Dec 2 08:45 (muller) |
| jac | ttyA Dec 3 15:18 (localhost) |
| eichsted | ttyB Dec 3 23:21 (pc1) |
| sweet | ttyS Dec 3 22:40 (dov) |
| "big-output" | 40 lines, 1659 characters |

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_249_1.png)

# An Introduction to the Editor

- 6. In the middle of working on this, I suddenly realize that I need to make a slight change to the recently saved buckaroo.confused file. That's where the ce command comes in handy. Using it, I can edit any other file:

```
~
: buckaroo.confused_
```

I press Return and see this:

> I found myself stealing a peek at my own watch and overheard
General Catbird's
I found myself stealing a peek at my own watch and overheard
General Catbird's aide give him the latest.
"He's not even here," went the conversation.
"Banzai.",
"Where the hell is he?"\n"At the hospital in El Paso."
"What? Why weren't we informed? What's wrong with him?"

aide give him the latest.
"He's not even here," went the conversation.
"Banzai.",
"Where the hell is he?"\n"At the hospital in El Paso."
"What? Why weren't we informed? What's wrong with him?"

```
"buckaroo.confused" 16 lines, 542 characters
```

SUMMARY That's it! You now know a considerable amount about one of the most important, and certainly most used, commands in UNIX. There's more to learn (isn't there always?), but now you can edit your files with aplomb!

# Summary

Table 10.2 summarizes the basic vi commands you learned in this hour.

| Command | Meaning |
| --- | --- |
| 0 | Move to the beginning of the line. |
| $ | Move to the end of the line. |
| /pattern | Search for the next line using a specified pattern. |
| ?pattern | Search backward for the next line using a specified pattern. |
| a | Append text—enter into insert mode after the current character. |
| ^b | Back up one screen of text. |
| B | Back up one space-delimited word. |
| b | Back up one word. |
| Backspace | Move left one character. |
| ^d | Move down half a page. |
| D | Delete through the end of the line. |
| d—dw | Delete word, dd = delete line. |
| Escape | Leave insert mode and return to command mode. |
| ^f | Move forward one line. |
| G | Go to the last line. |
| nG | Go to the nth line. |
| h | Move left one character. |
| i | Insert text—enter into insert mode before the current character. |
| j | Move down one line. |
| k | Move up one line. |
| l | Move right one character. |
| n | Repeat search. |
| 0 | Open new line above the current line. |
| o | Open new line below the current line. |
| Return | Move to the beginning of the next line. |
| ^u | Move up half a page. |
| U | Undo—restore current line if changed. |

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_251_0.png)

# An Introduction to the Editor

| Command | Meaning |
| --- | --- |
| u | Undo the last change made. |
| W | Move forward one space-delimited word. |
| w | Move forward one word. |
| x | Delete a single character. |
| : file | Edit a specified file without leaving vi. |
| n | Move to the next file in the list. |
| q | Quit and return to the system prompt. |
| q! | Quit and return to the system prompt, throwing away any changes to the file. |
| r file | Include the contents of the specified file at this position in the file that is currently being edited. |
| w file | Save the file to disk with this name. |
| w | Save the file to disk. |

# Workshop

The Workshop summarizes the key terms you learned and poses some questions about the topics presented in this chapter. It also provides you with a preview of what you will learn in the next hour.

# Key Terms

**addressing commands** The set of vi commands that enable you to specify what type of object you want to work with. The `d` commands serve as an example: `dw` delete word, and `db` delete the previous word.

**colon commands** The vi commands that begin with a colon, usually used for manipulation.

**command mode** The mode in which you can manage your document; this includes the capability to change text, rearrange it, and delete it.

**insert mode** The vi mode lets you enter text directly into a file. The `i` command starts the insert mode, and Escape exits it.

**modal** A modal program has multiple environments, or modes, that offer different capabilities. In a modal program, the Return key, for example, might do different things, depending on which mode you are in.
