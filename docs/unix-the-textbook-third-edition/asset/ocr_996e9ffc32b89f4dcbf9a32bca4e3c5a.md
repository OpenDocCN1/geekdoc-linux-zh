# TABLE 3.17 vi, vim, gvim Summary

| Vi Syntax | | |
|---|---|---|
| Command | Action | |
| cw | Change word. | |
| cc | Change line. | |
| c$ | Change text from current position to end of line. | |
| C | Same as c$. | |
| dd | Delete current line. | |
| 7 dd | Delete seven lines. | |
| d$ | Delete text from current position to end of line. | |
| D | Same as d$. | |
| 5dw | Deletes five words. | |
| d7,14 | Deletes lines seven through fourteen in the buffer. | |
| s | Substitute character. <Esc> ends substitute mode. | |
| 4s | Substitute four characters. <Esc> ends substitute mode. | |
| S | Substitute entire line. <Esc> ends substitute mode. | |
| u | Undo last change. | |
| <Ctrl+R> | Redo last change (vim and gvim). | |
| U | Restores the current line, if you have not moved off of it. | |
| x | Delete current cursor position. | |
| X | Delete back one character. | |
| 5X | Delete previous five characters | |
| . | Repeat last change. | |
| ~ | Change case and move cursor right. | |
| <Ctrl+A> | Increment number at the cursor (vim and gvim). | |
| <Ctrl+X> | Decrement number at the cursor (vim and gvim). | |
| Vi Mode Keys | | |
| Key | Action | |
| a | Appends text after the character the cursor is on. | |
| A | Appends text after the last character of the current line. | |
| c | Begins a change operation, allowing you to modify text. | |
| C | Changes from the cursor position to the end of the current line. | |
| i | Inserts text before the character the cursor is on. | |
| I | Inserts text at the beginning of the current line. | |
| o | Opens a blank line below the current line and puts the cursor on that line. | |
| O | Opens a blank line above the current line and puts the cursor on that line. | |
| Vi Command Mode | | |
| Command | Action | |
| :wq | Saves the buffer and quits. | |
| :w | Saves the current buffer and remains in the editor. | |
| :w filename | Saves the current buffer to filename | |
| :q | Quit vi (fails if changes were made). | |
| :q! | Quit vi without saving the buffer. | |
| :Q | Quit vi and invoke ex. | |
| :vi | Return to vi after Q command. | |
| ZZ | Quits vi, saving the file only if changes were made since the last save. | |