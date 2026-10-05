# 188 CHAPTER 5 THE LINUX UTILITIES

![](bbox=[0.292, 0.085, 0.712, 0.303])

Figure 5-17 Starting vim without a filename

RETURN after you give this command. Once you get the shell prompt back, refer to “Specifying a Terminal” on page 1106, and then start vim again.

If you start editor without a filename, vim assumes that you are a novice and tells you how to get started (Figure 5-17).

The practice file is new so that it does not contain any text. The vim editor displays a message similar to the one shown in Figure 5-16 on the status (bottom) line of the terminal to indicate that you are creating and editing a new file. When you edit an existing file, vim displays the first few lines of the file and gives status information about the file on the status line.

# COMMAND AND INPUT MODES

Two of vim's modes of operation are Command mode (also called Normal mode) and Input mode (Figure 5-18). While vim is in Command mode, you can give vim commands. For example, you can delete text or exit from vim. You can also command vim to enter Input mode. In Input mode, vim accepts anything you enter and displays it on the screen. Press ESCAPE to return vim to Command mode, By default the vim editor keeps you informed about which mode it is in: It displays INSERT at the lower-left corner of the screen while it is in Insert mode.

The following command causes vim to display line numbers to the text you are

```
:set number RETURN
```

Last Line mode The colon (:) in the preceding command puts vim into another mode, Last Line mode. While in this mode, vim keeps the cursor on the bottom line of the screen. When finishing the command by pressing RETURN, vim restores the cursor to its place in the text. Give the command :set nonumber RETURN to turn off line numbers.