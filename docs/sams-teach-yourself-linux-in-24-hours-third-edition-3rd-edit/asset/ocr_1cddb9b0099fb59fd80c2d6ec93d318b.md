The `linenumber` parameter (see Table 8.5) is the line where the cursor should be placed when the file opens in the buffer. In `vi`, you can display the line numbers along the left margin. Line numbers are useful if you are writing programming code or a legal document. For example, to start working at line 31 in the file named `practice.txt`, use the command `vi +31 practice.txt`.

The `pattern` parameter is used when you want `vi` to search for a string of text. When `vi` finds this text string, the cursor is placed at the first instance where the text string is found. For example, if a section of the text file where you want to start working contains the text string "introduction," use the command `vi +/introduction practice.txt`.

# Task: Creating a Text File

Before you can practice with the `vi` text editor, you'll need a file in which you can practice cursor movement and text editing commands. One way to follow along during the rest of the hour, and to have a second source of help, is to copy the tutorial that was installed with `vim`. The following steps guide you through the process of creating a new file and adding some text to the file:

+   1. Look for the `vim` tutorial file. Look in the `/usr/doc/` directory for a `vim-common-??` subdirectory. On a Linux-Mandrake system, this file is located at `/usr/doc/vim-common-5.6/tutor/tutor`.
+   2. Change to the directory that you want to use as your working directory (use the `cd` command). You might want to use your home directory or a subdirectory within your home directory.
+   3. Open `vi` and create a practice file at the same time. Type `vi practice.txt` and press Enter. This file will be stored in the working directory.
+   4. Add the contents of the tutorial file (which you located in step 1) to the practice file. Type `:r /usr/doc/vim-common-5.6/tutor/tutor` and press Enter. If the tutorial is located in another directory, make sure to use the correct directory path. Your file should look like the one shown in Figure 8.2.

![](bbox=[0.22, 0.88, 0.3, 0.94])

> > In Hour 7, "Moving Around the Filesystem," you learned how to use the `cat` command to append (or insert) the contents of one file to the end of another file. In `vi`, the `:r filename` command performs the same job.