# 208 Text Editing with ed and vi

| Table 5-3 (continued)
| Command | Does the Following |
|---|---|
| Change Text | |
| C | Changes up to the end of the current line. |
| cc | Changes the current line. |
| J | Joins the current line with the next one. |
| rx | Replaces the character under the cursor with x(where x is any character). |
| Move Cursor | |
| h ← | Moves one character to the left. |
| j ↓ | Moves one line down. |
| k ↑ | Moves one line up. |
| L | Moves cursor to the end of the screen. |
| l → | Moves one character to the right. |
| w | Moves to the beginning of the following word. |
| Scroll Text | |
| Ctrl+D | Scrolls forward by half a screen. |
| Ctrl+U | Scrolls backward by half a screen. |
| Refresh Screen | |
| Ctrl+L | Redraws screen. |
| Cut and Paste Text | |
| p | Puts the yanked line above the current line. |
| P | Puts the yanked line below the current line. |
| yy | Yanks (copies) current line into an unnamed buffer. |
| Colon Commands | |
| !command | Executes a shell command. |
| :q | Quits the editor. |
| :q! | Quits without saving changes. |
| :r filename | Reads the file and inserts it after the current line. |
| :w filename | Writes a buffer to the file. |
| :wq | Saves changes and exits. |
| Search Text | |
| /string | Searches forward for a string. |
| ?string | Searches backward for a string. |