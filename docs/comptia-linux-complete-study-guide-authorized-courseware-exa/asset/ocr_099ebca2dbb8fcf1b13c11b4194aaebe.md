change the case. Position the cursor on the first character you want to change, and press `~` repeatedly until the task is done.

**Undo**  To undo any change, type **u** in command mode.

**Open text**  In command mode, typing **o** opens text—that is, it inserts a new line immediately below the current one and enters insert mode on that line.

**Search**  To search forward for text in a file, type **/** in command mode, followed immediately by the text you want to locate. Typing **?** searches backward rather than forward.

**Change text**  The **c** command changes text from within command mode. You invoke it much like the **d** or **y** command, as in **cw** to change the next word or **cc** to change an entire line.

**Go to a line**  The **G** key brings you to a line that you specify. The **H** key "homes" the cursor—that is, it moves the cursor to the top line of the screen. The **L** key brings the key to the bottom line of the screen.

**Replace globally**  To replace all occurrences of one string with another, type **:s/original/replacement**, where *original* is the original string and *replacement* is its replacement. Change **%** to a starting line number, comma, and ending line number to perform this change on a small range of lines.

Vi offers a great deal more depth than is presented here; the editor is quite capable, and some Linux users are very attached to it. Entire books have been written about Vi. Consult one of these, or a Vi Web page like http://www.vim.org, for more information.

# ## Saving Changes

To save changes to a file, type **:w** from command mode. This enters ex mode and runs the **w** ex-mode command, which writes the file using whatever filename you specified when you launched Vi. Related commands enable other functions:

**Edit a new file**  The **:e** command edits a new file. For instance, **:e /etc/inittab** loads /etc/inittab for editing. Vi won't load a new file unless the existing one has been saved since its last change or unless you follow **:e** with an exclamation mark (**!**).

**Include an existing file**  The **:r** command includes the contents of an old file in an existing one.

**Execute an external command**  The ex-mode command **:!** executes the external command that you specify. For instance, typing **:!ls** runs **ls**, enabling you to see what files are present in the current directory.

**Quit**  Use the **:q** command to quit the program. As with **:e**, this command won't work unless changes have been saved or you append an exclamation mark to the command (as in **:q!**).

You can combine ex commands such as these to perform multiple actions in sequence. For instance, typing **:wq** writes changes and then quits from Vi. (**ZZ** is the equivalent of **:wq**.)