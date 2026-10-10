The computer will list all of the files in the current directory, including the new file:

1999 SUMM99 august99 july99 june99 summer99

There is just one small problem with this example: the convention in this book is to use lowercase letters for file names, and to capitalize directory names. (You don't have to do this, but it helps distinguish files from directories.) SUMM99 is an ordinary file, not a directory, so in the next section you will give it a different name.

# ## 6.9 Renaming a File with mv

The mv (“move”) command is used for renaming files. (It is also used for moving files to other directories, as you will see in the next chapter.)

+   1. **Choose a new name for the file.** As usual, you should choose names that are short and descriptive. An appropriate name for a file containing a calendar for the summer of 1999 might be `vacation99`.

+   2. **Enter the mv command, followed by the old name and the new name.** To rename SUMM99 as vacation99, type the command line
+   
+      $ mv SUMM99 vacation99 <RETURN>

+   3. **Verify that the new file name appears in the directory.** Because UNIX does not tell you that the file has been renamed, you will have to check this yourself using the `ls` command:
+   
+      $ ls <RETURN>
+   
+      The computer will list all of the files in the current directory:
+   
+      1999 aug99 july99 june99 sum99 vacation99

The difference between cp (copy) and mv (move) is that cp creates a new file, leaving the old file intact, while mv simply renames the old file.

# ## 6.10 Printing on the Default Printer

Frequently, you are likely to require hardcopy output from your files. How you produce this depends on the number and type of printers available to you, as well as the type of UNIX you are using.

+   - **Enter the simple line printer command, followed by the file name.** If you are using Berkeley UNIX, enter the `lpr` (“line printer”) command:
+   
+     $ lpr 1999 <RETURN>
+   
+     On AT&T UNIX, enter the `lp` command: