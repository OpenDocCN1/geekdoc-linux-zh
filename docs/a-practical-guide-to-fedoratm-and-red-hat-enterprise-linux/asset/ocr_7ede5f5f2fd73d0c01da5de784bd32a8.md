![](bbox=[0.323, 0.101, 0.815, 0.339])

**Figure 7-2 Starting vim without a filename**

displays the first few lines of the file and gives status information about the file on the status line.

**Problem** If you start vim with a terminal type that is not in the terminfo database, vim displays an error message and waits for you to press RETURN or sets the terminal type to ansi, which works on many terminals.

**Emergency exit** To reset the terminal type, press ESCAPE and then give the following command to exit from vim and display the shell prompt:

```
:q!
```

When you enter the colon (:), vim moves the cursor to the bottom line of the screen. The characters q! tell vim to quit without saving your work. (You will not ordinarily exit from vim this way because you typically want to save your work.) You must press RETURN after you give this command. When the shell displays its prompt, refer to “Specifying a Terminal” on page 1024 and start vim again.

If you start vim without a filename, it displays information about itself (Figure 7-2).

# **LPI** COMMAND AND INPUT MODES

Two of vim’s modes of operation are *Command mode* (also called Normal mode) and *Input mode* (Figure 7-3). While vim is in Command mode, you can give vim commands. For example, you can delete text or exit from vim. You can also command vim to enter Input mode. In Input mode, vim accepts anything you enter as text and displays it on the screen. Press ESCAPE to return vim to Command mode. By default the vim editor keeps you informed about which mode it is in: It displays INSERT at the lower-left corner of the screen while it is in Insert mode.