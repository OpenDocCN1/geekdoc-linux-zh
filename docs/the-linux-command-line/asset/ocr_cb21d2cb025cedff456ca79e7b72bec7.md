# Table 9-1: Cursor Movement Commands

| Key | Action |
|---|---|
| Ctrl-a | Move cursor to the beginning of the line. |
| Ctrl-e | Move cursor to the end of the line. |
| Ctrl-f | Move cursor forward one character; same as the right arrow key. |
| Ctrl-b | Move cursor backward one character; same as the left arrow key. |
| Alt-f | Move cursor forward one word. |
| Alt-b | Move cursor backward one word. |
| Ctrl-l | Clear the screen and move the cursor to the top left corner. The clear command does the same thing. |

# Modifying Text

Table 9-2 lists keyboard commands that are used to edit characters on the command line.

# Table 9-2: Text Editing Commands

| Key | Action |
|---|---|
| Ctrl-d | Delete the character at the cursor location |
| Ctrl-t | Transpose (exchange) the character at the cursor location with the one preceding it. |
| Alt-t | Transpose the word at the cursor location with the one preceding it. |
| Alt-l | Convert the characters from the cursor location to the end of the word to lowercase. |
| Alt-u | Convert the characters from the cursor location to the end of the word to uppercase. |

# Cutting And Pasting (Killing And Yankin g) Text

The Readline documentation uses the terms killing and yanking to refer to what we would commonly call cutting and pasting. Items that are cut are stored in a buffer called the kill-ring.