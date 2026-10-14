# 11.2.2 Basic Emacs Editing Keys

The following table lists basic editing keys and describes their function. Where two common keystrokes are available for a function, both are given.

| KEYS | DESCRIPTION |
|---|---|
| @uparrow or C-p | Move point up to the previous line. [GNU INFO BUG: any <> in the preceding line should be the one of the cursor arrow keys.] |
| @downarrow or C-n | Move point down to the next line. [GNU INFO BUG: any <> in the preceding line should be the one of the cursor arrow keys.] |
| @leftarrow or C-b | Move point back through the buffer one character to the left. [GNU INFO BUG: any <> in the preceding line should be the one of the cursor arrow keys.] |
| @rightarrow or C-f | Move point forward through the buffer one character to the right. [GNU INFO BUG: any <> in the preceding line should be the one of the cursor arrow keys.] |
| PgUp or C-v | Move point forward through the buffer one screenful. |
| PgDn or M-v | Move point backward through the buffer one screenful. |
| BKSP or C-h | Delete character to the left of point. |
| DEL or C-d | Delete character to the right of point. |
| INS | Toggles between Insert mode and Overwrite mode. |
| Shift-INS or C-y | Yank text in the kill ring at point (see section Pasting Text). |
| C-SPC | Set mark (see section Cutting Text). |
| C-_ | Undo the last action (control-underscore). |
| C-a | Move point to the beginning of the current line. |
| C-e | Move point to the end of the current line. |
| C-g | Cancel the current command. |
| C-h F | Open a copy of the Emacs FAQ in a new buffer. |
| C-h a function RET | List all Emacs commands related to function. |
| C-h i | Start Info. |
| C-h k key | Describe key. |
| C-h t | Start the Emacs tutorial. |
| C-k | Kill text from point to end of line. |
| C-l | Re-center the text in the Emacs window, placing the line where point is in the middle of the screen. |
| C-t | Transpose the character at point with the character to the left of point. |
| C-u number | Repeat the next command or keystroke you type number times. |
| C-w | Kill text from mark to point. |
| C-x C-c | Save all buffers open in Emacs, and then exit the program. |
| C-x C-f file RET | Open file in a new buffer for editing. To create a new file that does not yet exist, just specify the file name you want to give it. To browse through your files, type TAB instead of a file name. |
| C-left-click | Display a menu of all open buffers, sorted by major mode (works in X only). |