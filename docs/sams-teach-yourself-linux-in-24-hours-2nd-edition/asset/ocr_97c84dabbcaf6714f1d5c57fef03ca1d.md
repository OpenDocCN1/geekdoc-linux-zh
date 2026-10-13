Although you might find the more command to be more than adequate in reading files, you might really like the less pager.

# Browsing Files with the less Command

less is more or less like more, but less is also much more than more. Confused? Don't be, because less, like more, is also a pager command. Its author, Mark Nudelman, improved on a number of features in the more command and added many others.

The less command offers a number of advantages over more:

+   - You can scroll backwards and forwards through text files using your cursor keys.
+   - You can navigate through files with bookmarks by line numbers or by percentages of file.
+   - You have sophisticated searches, pattern options, and highlighting through multiple files.
+   - Keystrokes are compatible with word processing programs, such as emacs.
+   - The less command doesn't quit on you when you reach the end of a file or the end of the standard input.
+   - The information prompt at the bottom of the screen is more customizable and offers more information.
+   - There are loads of options, including a separate key setup program, lesskey, so you can customize which keys control less.

When you install Linux, the less pager is the default pager used by a number of programs, such as the man command. If you need to read compressed files (those with a .gz extension, and about which you'll learn in Hour 5), you can use the zless command found under the /usr/bin directory.

As an example, I first create a text file containing a list of all the OpenLinux commands in the /usr/bin directory with the ls command, as follows:

```
# ls /usr/bin >programs.txt
```

This command line creates a text file called programs.txt. To read this file, use the less command as in the following:

```
# less programs.txt
```

![](bbox=[0.88, 0.5, 0.99, 0.68])