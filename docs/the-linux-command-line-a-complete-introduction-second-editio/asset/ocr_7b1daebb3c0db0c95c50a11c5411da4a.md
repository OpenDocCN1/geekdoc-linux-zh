clipboard) that we can later recall with the p command to paste the contents of the buffer either before or after the cursor.

The y command is used to “yank” (copy) text in much the same way the d command is used to cut text. Table 12-4 provides some examples of combining the y command with various movement commands.

# Table 12-4: Yanking Commands

| Command | Copies |
|---|---|
| yy | The current line |
| 5yy | The current line and the next four lines |
| yw | From the current cursor position to the beginning of the next word |
| y$ | From the current cursor location to the end of the current line |
| y0 | From the current cursor location to the beginning of the line |
| y^ | From the current cursor location to the first non-whitespace character in the line |
| yG | From the current line to the end of the file |
| y20G | From the current line to the twentieth line of the file |

Let’s try some copy-and-paste. Place the cursor on the first line of the text and type yy to copy the current line. Next, move the cursor to the last line (G) and type p to paste the line below the current line.

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3
Line 4
Line 5
The quick brown fox jumped over the lazy dog. It was cool.
```

Just as before, the u command will undo our change. With the cursor still positioned on the last line of the file, type P to paste the text above