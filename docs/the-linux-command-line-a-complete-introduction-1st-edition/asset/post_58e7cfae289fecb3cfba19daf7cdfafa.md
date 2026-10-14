
## Command Line Editing

bash uses a library (a shared collection of routines that different programs can use) called Readline to implement command line editing. We have already seen some of this. We know, for example, that the arrow keys move the cursor, but there are many more features. Think of these as additional tools that we can employ in our work. It’s not important to learn all of them, but many of them are very useful. Pick and choose as desired.

> Note: Some of the key sequences below (particularly those that use the ALT key) may be intercepted by the GUI for other functions. All of the key sequences should work properly when using a virtual console.

## Cursor Movement

Table 8-1 lists the keys used to move the cursor.

### Table 8-1: Cursor Movement Commands

| Key | Action |
| --- | --- |
| CTRL-A | Move cursor to the beginning of the line. |
| CTRL-E | Move cursor to the end of the line. |
| CTRL-F | Move cursor forward one character; same as the right arrow key. |
| CTRL-B | Move cursor backward one character; same as the left arrow key. |
| ALT-F | Move cursor forward one word. |
| ALT-B | Move cursor backward one word. |
| CTRL-L | Clear the screen and move the cursor to the top left corner. The clear command does the same thing. |

## Modifying Text

Table 8-2 lists keyboard commands that are used to edit characters on the command line.

## Cutting and Pasting (Killing and Yanking) Text

The Readline documentation uses the terms killing and yanking to refer to what we would commonly call cutting and pasting. Table 8-3 lists the commands for cutting and pasting. Items that are cut are stored in a buffer called the kill ring.

**Table 8-2: Text Editing Commands**

| Key | Action |
|---|---|
| CTRL-D | Delete the character at the cursor location. |
| CTRL-T | Transpose (exchange) the character at the cursor location with the one preceding it. |
| ALT-T | Transpose the word at the cursor location with the one preceding it. |
| ALT-L | Convert the characters from the cursor location to the end of the word to lowercase. |
| ALT-U | Convert the characters from the cursor location to the end of the word to uppercase. |

**Table 8-3: Cut and Paste Commands**

| Key | Action |
|---|---|
| CTRL-K | Kill text from the cursor location to the end of line. |
| CTRL-U | Kill text from the cursor location to the beginning of the line. |
| ALT-D | Kill text from the cursor location to the end of the current word. |
| ALT-BACKSPACE | Kill text from the cursor location to the beginning of the current word. If the cursor is at the beginning of a word, kill the previous word. |
| CTRL-Y | Yank text from the kill-ring and insert it at the cursor location. |

> **THE META KEY**
> 
> If you venture into the Readline documentation, which can be found in the “READLINE” section of the bash man page, you will encounter the term *meta key*. On modern keyboards this maps to the ALT key, but it wasn’t always so. Back in the dim times (before PCs but after Unix) not everybody had their own computer. What they might have had was a device called a terminal. A terminal was a communication device that featured a text-display screen and a keyboard and had just enough electronics inside to display text characters and move the cursor around. It was attached (usually by serial cable) to a larger computer or the communication network of a larger computer. There were many different brands of terminals, and they all had different keyboards and display feature sets. Since they all tended to at least understand ASCII, software
> 
> developers wanting portable applications wrote to the lowest common denominator. Unix systems have a very elaborate way of dealing with terminals and their different display features. Since the developers of Readline could not be sure of the presence of a dedicated extra control key, they invented one and called it meta. While the ALT key serves as the meta key on modern keyboards, you can also press and release the ESC key to get the same effect as holding down the ALT key if you’re still using a terminal (which you can still do in Linux!).

## Completion

Another way that the shell can help you is through a mechanism called completion. Completion occurs when you press the TAB key while typing a command. Let’s see how this works. Say your home directory looks like this:

```
[me@linuxbox ~]$ ls
Desktop  ls-output.txt  Pictures  Templates  Videos
Documents  Music  Public
```

Try typing the following but don’t press the ENTER key:

```
[me@linuxbox ~]$ ls l
```

Now press the TAB key:

```
[me@linuxbox ~]$ ls ls-output.txt
```

See how the shell completed the line for you? Let’s try another one. Again, don’t press ENTER:

```
[me@linuxbox ~]$ ls D
```

Press TAB:

```
[me@linuxbox ~]$ ls D
```

No completion—just a beep. This happened because D matches more than one entry in the directory. For completion to be successful, the “clue” you give it has to be unambiguous. We can go further:

```
[me@linuxbox ~]$ ls Do
```

Then press TAB:

```
[me@linuxbox ~]$ ls Documents
```

The completion is successful.
