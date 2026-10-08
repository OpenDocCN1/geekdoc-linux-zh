In addition to these commands, you can use other commands to move the cursor. Table 3-1 summarizes the vi editor's cursor movement keys.

| Key | Movement |
| :--- | :--- |
| h or left arrow | Left one character position |
| l or right arrow | Right one character position |
| k or up arrow | Up one line |
| j or down arrow | Down one line |
| H | Upper-left corner of the screen |
| L | Last line on the screen |
| nG | Go to the line specified by a number, n |
| w | Forward one word |
| b | Back one word |
| 0 (zero) | To the beginning of the current line |
| $ | To the end of the current line |
| Ctrl+U | Up one-half screen |
| Ctrl+D | Down one-half screen |
| Ctrl+F or Pg down | Forward one screen |
| Ctrl+B or Pg up | Back one screen |

Table 3-1: vi editor's cursor movement keys

Remember that cursor movement keys only work in command mode.

Note: Using the letter keys to move the cursor dates back to the days when UNIX used teletype terminals that had no arrow keys. Designers of vi chose the letter keys because of their relative position on the keyboard.

# Deleting Text

Now that you know how to insert text and move around a file, you are ready to delete text. To do so, move to a character and then type x to delete that character. You can also combine many delete commands with cursor movement commands to delete more than one character. Table 3-2 summarizes the most common delete commands.