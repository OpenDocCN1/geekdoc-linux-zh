![](bbox=[0.13, 0.09, 0.73, 0.37])

# Figure 8-3 	 *The vi editor editing /etc/fstab*

Later, the bottom line functions as a command entry and status line. The rest of the lines display the file. If the file contains fewer lines than the window, *vi* displays the empty lines with a tilde (^) in the first column.

The current line is marked by the cursor, which appears as a small black rectangle. The cursor appears on top of a character.

# vi modes

In *vi*, you work in one of three modes:

+   *   *Visual command mode* is the default. In this mode, anything that you type is interpreted as a command that applies to the line containing the cursor. The *vi* commands are similar to *ed* commands.
+   
+   *   *Colon command mode* enables you to read or write files, set *vi* options, and quit the *vi* editing session. All colon commands start with a colon (:). When you enter the colon, *vi* positions the cursor at the last line and enables you to type a command. The command takes effect when you press Enter.
+   
+   *   *Text input mode* enables you to enter text into the buffer. You can enter input mode with the commands *a* (*append after* cursor), *A* (*append at end of* line), or *i* (*insert after* cursor). After entering lines of text, you have to press *Esc* to leave input mode and reenter *visual command* mode.

One problem with all these modes is that you cannot easily tell *vi*’s current mode. It is frustrating to begin typing, only to realize that *vi* is not in input mode. The converse situation also occurs commonly—you may be typing text when you want to enter a command. You want to make sure that *vi* is in *command* mode, just press *Esc* a few times. (Pressing *Esc* more than one does no harm.)

> To view online help in *vi*, type **:help** while in *command* mode. Type **:q** to exit the help screen and return to the file you are editing.