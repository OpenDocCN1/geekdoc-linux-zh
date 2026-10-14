# Table 12-3 (continued)

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

# Cutting, Copying, and Pasting Text

The d command not only deletes text, it also “cuts” text. Each time we use the d command, the deletion is copied into a paste buffer (think clipboard) that we can later recall with the p command to paste the contents of the buffer after the cursor or with the P command to paste the contents before the cursor.