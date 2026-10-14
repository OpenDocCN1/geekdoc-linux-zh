Table A–3 summarizes the commands used to insert and append text to a file. These commands are executed from the command mode and automatically put vi into the input mode.

**Table A–3: Text Insertion Command Summary**

| Command | Result |
|---|---|
| `i` | Inserts text immediately before the current cursor position. |
| `a` | Appends text immediately after the current cursor position. |
| `I` | Inserts text at the beginning of the current line. |
| `A` | Appends text to the end of the current line. |
| `o` | Opens a new line directly below the current line. |
| `O` | Opens a new line directly above the current line. |

# A.1.6 Editing Text

Up to this point you only have learned how to add new text to the file, but what if you need to change some text? The vi text editor provides commands for deleting and changing text. For example, to remove the word easily, from the sixth line in my.file, move the cursor to the first character of the word and enter:

```
dw
```

This command is a combination of the delete command d, and the motion command w. In fact, many vi commands can be combined with motion commands to specify the duration of the action. The general form of a vi command follows:

```
[number] [command] motion
```

The command entry represents an action command, motion represents a motion command, and number represents the number of times to perform the command. You also can use this general form to move the cursor in larger steps.

To illustrate this concept, move the cursor to the beginning of my.file by typing H. Now, to move the cursor forward four words, enter:

```
4w
```

The cursor has moved four entire words and is positioned at the first letter of the fifth word, easy.