
# DELETING TEXT

- x (Delete character) You can delete a single character by moving the cursor until it is the character you want to delete and giving the command x.
- dw (Delete word) You can delete a word by positioning the cursor on the first letter of the word and giving the command dw.
- dd (Delete line) You can delete a line of text by moving the cursor until it is anywhere on the line and giving the command dd.

# UNDOING MISTAKES

- u (Undo) If you delete a character, line, or word by mistake or give any command you want to reverse, give the command u (Undo) immediately after the command you undo. The vim editor will restore the text to the way it was before you gave the last command. If you give the u command again, vim will undo the command you gave before the one you just und. You can use this technique to back up over many of your actions. With the compatible parameter (page 193), however, vim can undo the most recent change.
- r (Redo) If you undo a command you did not mean to, give a Redo command: CTRL-R or r (followed by a RETURN). The vim editor will redo the undo. With the Undo command, you can get the Redo command many times in a row.

# ENTERING ADDITIONAL TEXT

- i (Insert) When you want to insert new text within existing text, move the cursor so it is the character that follows the new text you want to enter. Give it the i (Insert) command to put vim in Input mode, enter the new text, and press ESC to return to Command mode. Alternatively, you can position the cursor on the character that precedes the new text and use a a (Append) command.
- o (Open) To enter one or more lines, position the cursor on the line where you want the new text to go. Give the command o (Open). The vim editor opens a blank line below the line the cursor was, puts the cursor on the new, empty line, and goes into Input mode. Enter the new text, ending each line with a RETURN. When you are finished entering text, press ESC to return to Command mode. The command works in the same way o works, except it opens a blank line before the cursor is.

# CORRECTING TEXT

To correct text, use dd, dw, or x to remove the incorrect text. Then use i, a, o, or O to insert the correct text.

For example, change the word "pressing" by hitting "hitting" in Figure 5-19 on page 190, you might use the ARROW keys to move the cursor until it is on top of the p in pressing-ing. Give the command dw to delete the word pressing. Put vim in Input mode by giving an i, enter the word hitting followed by a SPACE, and press ESC. The word is changed and vim is in Command mode, waiting for another command. A shorthand for the two commands dw followed by a i if the i is (Change word). The command cw puts vim into Input mode.

# Page breaks for the printer

tip CONTROL-L tells the printer to skip to the top of the next page. You can enter this character anywhere in a document by pressing CONTROL-L while you are in input mode. ^L does not appear, press CONTROL-v before CONTROL-L.

# ENDING THE EDITING SESSION

While you are editing, vim keeps the edited text in an area named the Work buffer. When you finish editing, you must write the contents of the Work buffer to a disk file so that the edited text is saved and available when you want it.

Make sure vim is in Command mode, and use the ZZ command (you must uppercase Zs) to write your newly entered text to the disk and end the editing session. After you give the ZZ command, vim returns control to the shell. You can exit with :q! if you do not want to save your work.

Do not confuse ZZ with CONTROL-Z

caution When you exit vim with ZZ, make sure that you type ZZ and not CONTROL-Z (typically the pending key). When you press CONTROL-Z, vim disappears from your screen, almost as you had exited from it. In fact, vim will continue running in the background with your work unsaved. Refer to "Job Control" on page 303. If you want to start editing the same file with a vim command, vim displays a message about a swap file.

# THE compatible Parameter

The compatible parameter makes vim more compatible with vi. By default this parameter is not set. From the command line use the -C option to set the compatible parameter and use the -N option to unset it. To get started with vim you can ignore this parameter.

Setting the compatible parameter changes many aspects of vim works. For example, when the compatible parameter is set, the Undo command (page 192) can undo only your most recent change; in contrast, with the compatible parameter unset, you can Undo repeatedly to undo many changes. On the compatible parameter, give the command :help compatible RETURN. To display a complete list of vim's differences from the original vi, use :help vi-diff RETURN. See page 190 for a discussion of the help command.

# CHAPTER SUMMARY

The utilities introduced in this chapter are a small but powerful subset of the many utilities available on an Ubuntu Linux system. Because you will use them frequently and because they are integral to the following chapters, it is important that you become comfortable using them.

# 194 CHAPTER 5 THE LINUX UTILITIES

The utilities listed in Table 5-2 manipulate, display, compare, and print files.

# Table 5-2 File utilities

| Utility | Function |
| --- | --- |
| cp | Copies one or more files (page 163) |
| diff | Displays the differences between two files (page 168) |
| file | Displays information about the contents of a file (page 170) |
| grep | Searches file(s) for a string (page 166) |
| head | Displays the lines at the beginning of a file (page 166) |
| lpq | Displays a list of jobs in the print queue (page 165) |
| lpr | Places file(s) in the print queue (page 165) |
| lprm | Removes a job from the print queue (page 165) |
| mv | Renames a file or moves file(s) to another directory (page 164) |
| sort | Puts a file in order by lines (page 168) |
| tail | Displays the lines at the end of a file (page 167) |
| uniq | Displays the contents of a file, skipping adjacent duplicate lines (page 168) |

To reduce the amount of disk space a file occupies, you can compress it with the bzip2 utility. Compression works well on files that contain patterns, as most text files reduce the size of almost all files. The inverse of bzip2—bunzip2— restores a file to its original, compressed form. Table 5-3 lists utilities that compress and decompress files. The bzip2 utility is the most efficient of these.

# Table 5-3 (De)compression utilities

An archive is a file, frequently compressed, that contains a group of files. The tar utility (Table 5-4) packs and unpacks archives. The file extensions .tar.bz2, .tar.gz, and .tgz identify compressed tar archive files and are often seen on software packages obtained over the Internet.

# Table 5-4 Archive utility

| Utility | Function |
| --- | --- |
| tar | Creates or extracts files from an archive file (page 176) |

The utilities listed in Table 5-5 determine the location of a utility on the local system. For example, they can display the pathname of a utility or a list of C++ compilers available on the local system.

# Table 5-5 Location utilities

| Utility | Function |
| --- | --- |
| mlocate | Searches for files on the local system (page 180) |
| whereis | Displays the full pathnames of a utility, source code, or man page (page 178) |
| which | Displays the full pathname of a command you can run (page 178) |

Table 5-6 lists utilities that display information about other users. You can easily learn a user's full name, the user's status, the login shell of the user, and other items of information maintained by the system.

# Table 5-6 User and system information utilities

| Utility | Function |
| --- | --- |
| finger | Displays detailed information about users, including their full names (page 181) |
| hostname | Displays the name of the local system (page 163) |
| w | Displays detailed information about users who are logged in on the local system (page 183) |
| who | Displays information about users who are logged in on the local system (page 180) |

The utilities shown in Table 5-7 can help you stay in touch with other users on the local network.

# Table 5-7 User communication utilities

| Utility | Function |
| --- | --- |
| mesg | Permits or denies messages sent by write (page 185) |
| write | Sends a message to another user who is logged in (page 184) |
