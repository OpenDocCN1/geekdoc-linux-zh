# TABLE 8.4 Deleting Text from the Buffer Area

| To Delete | Use This Command |
|---|---|
| From the cursor to the end of a word | dw |
| The three words following the cursor | 3dw |
| From the cursor to the end of a line | d$ |
| From the cursor to the beginning of a line | d0 |
| From the cursor to the end of a paragraph | d} |
| The line on which the cursor rests | dd |
| Current line and 3 following lines | 4dd |
| The character under the cursor | x |
| The character to the left of the cursor | X |
| Undo unwanted changes | u |

# Copying Text

Organizing a document involves quite a bit of moving text around. To move text around in vi, you must first yank the text, move the cursor to the new location for the text, and then paste the text in the new location.

New Term

When you yank text, you are selecting it (although you might not see the text highlighted on the screen) and making a copy of the selected text. The yanked text is stored in an unnamed buffer. This unnamed buffer is a temporary holding pen where only the last piece of yanked text is kept.

To yank text, move the cursor to the beginning of the text that you want to copy, press the y key followed by the cursor movement command (found in Table 8.1) that will move the cursor to the end of the text. For example, to copy the text from the cursor position to the end of the line, press y$. To position the cursor in the place where you want to copy the text, use the cursor movement commands. After the cursor is in place, paste the text by pressing p. The text will be copied on the line below the cursor.

![](bbox=[0.2, 0.82, 0.28, 0.92])

> If you want to move text, first delete the text to be moved (use one of the commands found in Table 8.3). Then move the cursor to the place where you want to paste the text and press the p key.