![](bbox=[0.3, 0.08, 0.75, 0.38])

If you get this message, give the following command to exit from vim and get the shell prompt back:

```
:q!
```

Normally, when you enter the colon (:), vim moves the cursor to the bottom line of the screen (it does nothing in this case). The characters q! tell vim to quit without saving your work. (You will not ordinarily exit from vim this way because you typically want to save your work.) You must press RETURN after you give this command. Once you get the shell prompt back, refer to “Specifying a Terminal” on page 1040, and then start vim again.

If you start this editor without a filename, vim assumes that you are a novice and tells you how to get started (Figure 5-17).

The practice file is new so it does not contain any text. The vim editor displays a message similar to the one shown in Figure 5-16 on the status (bottom) line of the terminal to indicate that you are creating and editing a new file. When you edit an existing file, vim displays the first few lines of the file and gives status information about the file on the status line.

# COMMAND AND INPUT MODES

Two of vim's modes of operation are Command mode (also called Normal mode) and Input mode (Figure 5-18). While vim is in Command mode, you can give vim commands. For example, you can delete text or exit from vim. You can also command vim to enter Input mode. In Input mode, vim accepts anything you enter as text and displays it on the screen. Press ESCAPE to return vim to Command mode. By default the vim editor keeps you informed about which mode it is in: It displays INSERT at the lower-left corner of the screen while it is in Insert mode.

The following command causes vim to display line numbers next to the text you are editing: