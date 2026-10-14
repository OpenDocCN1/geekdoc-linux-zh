
We can demonstrate this as follows: Place the cursor on Line 3 and then type o.

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3

Line 4
Line 5
```

A new line was opened below the third line, and we entered insert mode. Exit insert mode by pressing the ESC key. Type u to undo our change.

Type O to open the line above the cursor:

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3
Line 4
Line 5
```

Exit insert mode by pressing the ESC key and undo our change by typing u.

## Deleting Text

As we might expect, vi offers a variety of ways to delete text, all of which contain one of two keystrokes. First, the X key will delete a character at the cursor location. x may be preceded by a number specifying how many characters are to be deleted. The D key is more general purpose. Like x, it may be preceded by a number specifying the number of times the deletion is to be performed. In addition, d is always followed by a movement command that controls the size of the deletion. Table 12-3 lists some examples.

Place the cursor on the word It on the first line of our text. Type x repeatedly until the rest of the sentence is deleted. Next, type u repeatedly until the deletion is undone.

> Note: Real vi supports only a single level of undo. vim supports multiple levels.

## Table 12-3: Text Deletion Commands

| Command | Deletes |
|---|---|
| x | The current character |
| 3x | The current character and the next two characters |
| dd | The current line |
| 5dd | The current line and the next four lines |

## Table 12-3 (continued)

| Command | Deletes |
|---|---|
| dW | From the current cursor location to the beginning of the next word |
| d$ | From the current cursor location to the end of the current line |
| d0 | From the current cursor location to the beginning of the line |
| d^ | From the current cursor location to the first non-whitespace character in the line |
| dG | From the current line to the end of the file |
| d20G | From the current line to the 20th line of the file |

Let’s try the deletion again, this time using the d command. Again, move the cursor to the word It and type dW to delete the word:

```
The quick brown fox jumped over the lazy dog. was cool.
Line 2
Line 3
Line 4
Line 5
```

Type d$ to delete from the cursor position to the end of the line:

```
The quick brown fox jumped over the lazy dog.
Line 2
Line 3
Line 4
Line 5
```

Type dG to delete from the current line to the end of the file:

```
~
~
~
~
```

Type u three times to undo the deletions.

## Cutting, Copying, and Pasting Text

The d command not only deletes text, it also “cuts” text. Each time we use the d command, the deletion is copied into a paste buffer (think clipboard) that we can later recall with the p command to paste the contents of the buffer after the cursor or with the P command to paste the contents before the cursor.

The y command is used to “yank” (copy) text in much the same way the d command is used to cut text. Table 12-4 lists some examples combining the y command with various movement commands.

## Table 12-4: Yanking Commands

| Command | Copies |
|---|---|
| yy | The current line |
| 5yy | The current line and the next four lines |
| yw | From the current cursor location to the beginning of the next word |
| y$ | From the current cursor location to the end of the current line |
| y0 | From the current cursor location to the beginning of the line |
| y^ | From the current cursor location to the first non-whitespace character in the line |
| yG | From the current line to the end of the file |
| y20G | From the current line to the 20th line of the file |

Let’s try some copy and paste. Place the cursor on the first line of the text and type yy to copy the current line. Next, move the cursor to the last line (G) and type p to paste the copied line below the current line:

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3
Line 4
The quick brown fox jumped over the lazy dog. It was cool.
```

Just as before, the u command will undo our change. With the cursor still positioned on the last line of the file, type P to paste the text above the current line:

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3
Line 4
The quick brown fox jumped over the lazy dog. It was cool.
Line 5
```

Try out some of the other y commands in Table 12-4 and get to know the behavior of both the p and P commands. When you are done, return the file to its original state.
