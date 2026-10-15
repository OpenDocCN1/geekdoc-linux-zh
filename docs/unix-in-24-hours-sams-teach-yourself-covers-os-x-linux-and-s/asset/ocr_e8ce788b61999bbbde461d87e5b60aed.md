usermod commands for just this purpose. If yours has one of these commands, check the man page to learn more about how to use it. Now you can go back to step 2 and set up a Bash shell alias. This will help you avoid mischief with the rm command.

The best way to avoid trouble with any of these commands is to learn to be just a bit paranoid about them. Before you remove a file, make sure it’s the one you want to remove. Before you remove a directory, make doubly sure that it doesn’t contain any files you might want. Before you rename a file or directory, double-check to see whether renaming it is going to cause any trouble. Before you press Enter, make sure the command is exactly what you want to invoke.

Take your time with the commands you learned in this hour, and you should be fine. Even in the worst case, you will hopefully have the safety net of a backup performed by a system administrator—though you shouldn’t rely on it.

# Summary

You now have completed six hours of Unix instruction, and you are armed with enough commands to make Unix do what you want it to do—as well as cause some trouble. In this hour, you learned the differences between cp and mv for moving files and how to use mv to rename both files and directories. You also learned how to create directories with the mkdir command and how to remove them with the rmdir command. And you learned about the rm command for removing files and directories, as well as how to avoid getting into too much trouble with it.

Finally, if you were really paying attention, you learned how to identify which login shell you’re using (csh, ksh, bash, or sh).

# Workshop

The Workshop summarizes the key terms you’ve learned and poses some questions about the topics presented in this lesson. It also provides you with a preview of what you will learn in the next hour.

# Key Terms

recursive command This type of command repeatedly invokes itself while operating on a hierarchy of files.

shell alias Most Unix shells have a convenient way for you to create abbreviations for commonly used commands or series of commands, known as shell aliases. For example, if I always found myself typing ls -F, an alias can let me type just ls and have the shell automatically add the -F flag each time.

# Exercises

+   1. What are the differences between cp and mv?
+   2. If you were installing a program from a USB stick onto a hard disk, would you use