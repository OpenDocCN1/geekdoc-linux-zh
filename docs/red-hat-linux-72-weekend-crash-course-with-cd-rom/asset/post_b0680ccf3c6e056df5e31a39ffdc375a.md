
![](img/5fe8f856723cde0b366f73584b9e64b8_109_0.png)

### Figure 8-3 The vi editor editing /etc/fstab

Later, the bottom line functions as a command entry and status line. The rest of the lines display the file. If the file contains fewer lines than the window, *vi* displays the empty lines with a tilde (^) in the first column.

The current line is marked by the cursor, which appears as a small black rectangle. The cursor appears on top of a character.

### vi modes

In *vi*, you work in one of three modes:

- *Visual command mode* is the default. In this mode, anything that you type is interpreted as a command that applies to the line containing the cursor. The *vi* commands are similar to *ed* commands.
- *Colon command mode* enables you to read or write files, set *vi* options, and quit the *vi* editing session. All colon commands start with a colon (:). When you enter the colon, *vi* positions the cursor at the last line and enables you to type a command. The command takes effect when you press Enter.
- *Text input mode* enables you to enter text into the buffer. You can enter input mode with the commands *a* (*append after* cursor), *A* (*append at end of* line), or *i* (*insert after* cursor). After entering lines of text, you have to press *Esc* to leave input mode and reenter *visual command* mode.

One problem with all these modes is that you cannot easily tell *vi*’s current mode. It is frustrating to begin typing, only to realize that *vi* is not in input mode. The converse situation also occurs commonly—you may be typing text when you want to enter a command. You want to make sure that *vi* is in *command* mode, just press *Esc* a few times. (Pressing *Esc* more than one does no harm.)

> To view online help in *vi*, type **:help** while in *command* mode. Type **:q** to exit the help screen and return to the file you are editing.

### Moving the cursor

The vi editor initially positions the cursor on the first character. One of the first things that you need to learn is how to move the cursor around. Try the following commands. Just type the letter (in visual command mode) and vi responds.

- b moves the cursor one word backward.
- h moves the cursor one character to the left.
- j moves the cursor one line down.
- k moves the cursor one line up.
- l moves the cursor one character to the right.
- w moves the cursor one word forward.
- Ctrl+D moves down half a screen.
- Ctrl+U scrolls up half a screen.

![](img/5fe8f856723cde0b366f73584b9e64b8_110_0.png)

Luckily, you can also move the cursor using the arrow keys. If you cannot remember the meaning of the hjkl characters, just use the arrow keys to move around the file.

You can go to a specific line number at any time. This is when a colon command comes in. To go to line 1, for example, type the following and then press Enter:

```
:1
```

When you type the colon, vi displays the colon on the last line of the screen. From then on, vi uses the text that you type as a command. You have to press Enter to submit the command to vi. In colon command mode, vi accepts all the commands that the ed editor accepts—and then some.

### Searching for strings

To search for a string, first type a slash (/). The vi editor displays the slash on the last line of the screen. Type the search string and then press Enter. The vi editor locates the string and positions the cursor at the beginning of that string. Thus, to locate the string cdrom in the file /etc/fstab, type:

```
/cdrom
```

### Deleting lines

To delete the line that contains the cursor, type dd (two lowercase ds). The vi editor deletes that line of text and makes the next line the current one.

### Entering text before cursor

To begin entering text in front of the cursor, type i (a lowercase i all by itself). The vi editor switches to text input mode. Now you can enter text. When you finish entering text, press Esc to return to visual command mode.

### Saving changes

After you finish editing the file, you can save the changes in the file with the :w command. To quit the editor without saving any changes, use the :q! command. If you want to save the changes and exit, you can type :wq to perform both steps at the same time. The vi editor saves the changes in the file and exits. You can also save the changes and exit the editor by pressing Shift-zz (hold down the Shift key and press z twice).

### Commands

In addition to the few commands you have just learned, vi accepts a large number of commands. Table 8-2 lists some commonly used vi commands, organized by task.

**Table 8-2 Commonly Used vi Commands**

| Task and Command | Meaning |
| :--- | :--- |
| **Insert text** | |
| a | Inserts text after the cursor. |
| A | Inserts text at the end of the current line. |
| I | Inserts text at the beginning of the current line. |
| i | Inserts text before the cursor. |
| o | Inserts a new line below the current line. |
| O | Inserts a new line above the current line. |
| **Delete text** | |
| D | Deletes up to the end of the current line. |
| dd | Deletes the current line. |
| dl | Deletes the character on which the cursor rests. |
| dh | Deletes the character preceding the cursor. |
| dw | Deletes from the cursor to the end of the following word. |
| x | Deletes the character on which the cursor rests. |
| **Change text** | |
| C | Changes up to the end of the current line. |
| cc | Changes the current line. |
| s | Deletes the character under the cursor and enters insert mode. |
| J | Joins the current line with the next one. |
| rx | Replaces the character under the cursor with *x* (*x* is any character). |
| **Move cursor** | |
| h | Moves one character to the left. |
| j | Moves one line down. |
| k | Moves one line up. |
| L | Moves cursor to the end of the screen. |
| l | Moves one character to the right. |
| w | Moves to the beginning of the following word. |
| **Scroll text** | |
| Ctrl-b | Scrolls backward by one full screen. |
| Ctrl-d | Scrolls forward by half a screen. |
| Ctrl-f | Scrolls forward by one full screen. |
| Ctrl-u | Scrolls backward by half a screen. |
| **Cut and paste text** | |
| P | Puts a yanked (copied) line above the current line. |
| p | Puts a yanked line below the current line. |
| yy | Yanks the current line into an unnamed buffer. |
| **Colon commands** | |
| :command | Executes the shell *command*. |
| :q | Quits the editor. |
| :q! | Quits the editor without saving changes. |
| :r *filename* | Reads a file and inserts text after the current line. |
| :w *filename* | Writes a buffer to a file. |
| :wq | Saves changes and exits the editor. |
| **Search text** | |
| /string | Searches forward for *string*, a series of one or more characters. |
| ?string | Searches backward for *string*, a series of one or more characters. |
| **Miscellaneous** | |
| u | Undoes the last command. |
| Esc | Ends input mode and enters visual command mode. |
| U | Undoes recent changes to the current line. |

To try these commands, copy a file such as /etc/X11/XF86Config to your home directory and use vi to edit that file with the following commands:

```bash
cd
cp /etc/X11/XF86Config .
vi XF86Config
```

As you edit the file, try the commands shown in Table 8-2. Because good vi skills are useful in all UNIX systems, including Red Hat Linux, you should spend a few minutes familiarizing yourself with some of the commands from Table 8-2.

### Troubleshooting

If you get an error message resembling TERM variable not set when starting vi, use the export command to set the TERM environment variable. For example,

```bash
export TERM=linux
```

Similarly, if your vi sessions scroll strangely or the bottom lines of the screen seem jumbled and the TERM environment variable is set, try setting TERM to vt100 (export TERM=vt100), which is a very generic, basic terminal type setting.

If you have trouble remembering what mode you are in (visual command mode, colon command mode, or insert mode) while using vi, execute the colon command :set showmode. This will cause the bottom line of the vi window to display the current mode constantly, unless you are executing a colon command or a search.

If you have totally fouled up a file and want to abandon all your changes, use the colon command, :q!, to exit without saving any changes.

![](img/5fe8f856723cde0b366f73584b9e64b8_113_0.png)

### REVIEW

This session showed you how to use the graphical text editors in GNOME and KDE to edit files. The graphical text editors are intuitive to use, but sometimes you may have to edit text files without the benefit of a graphical login. For those situations, you practiced editing text files with the text-mode editors: ed and vi.

### QUIZ YOURSELF

1. How do you start the GNOME text editor? (See “Text Editing with GUI Text Editors.”)
2. When editing with the ed editor, how do you view all lines of a file? (See “Using ed.”)
3. When editing a file with the ed editor, what command do you use to locate a line containing a string monitor? (See “Using ed.”)
4. What are the three modes of the vi editor? (See “Using vi.”)
5. How do you exit the vi editor without saving any changes? (See “Using vi.”)
