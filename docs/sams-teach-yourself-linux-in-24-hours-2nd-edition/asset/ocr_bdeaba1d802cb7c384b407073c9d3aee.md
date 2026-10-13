```
trashcan delete aborted.
# rmv -e
emptying the trash...
empty the trash? y
# rmv -1
your .trash directory contains:
total 0
```

The rmv script asks if you're sure you want to empty the trash. If you type an n, the delete is aborted. If you type a y, the trash is deleted. Because the letter e is found on the command line, the empty variable is set to true and the statements following the if ... then test line are run. The script prints a message to your display, and then, using the read command, waits for you to enter an answer. The answer is then tested, and if it is yes, the files in the .trash directory are deleted.

Using the shell, you can quickly build simple programs to accomplish major tasks. Feel free to improve this program by adding features or improving on how file names are handled at the command line. One such improvement might be to add the capability to handle wildcards or whole directories. Another improvement might be an interactive deletion of files. See the bash manual page for more information about other shell commands and operators you can use in your own shell scripts.

# Summary

This hour introduced just the basics of using a shell with OpenLinux. Don't be intimidated by the command line! Mastery of the intricacies and idiosyncrasies of using any shell can take lots of practice. Make sure you practice safe computing: define aliases to force potentially harmful commands to act interactively; think twice before using wildcards when deleting files; and never use OpenLinux as the root operator all the time. The more you learn about OpenLinux, the more confidence you'll have in tackling problems and building custom solutions when using the shell.

# Q&A

Q Help! I was using the shell, a program ran awry, and all of a sudden the screen is full of garbage characters?

A Try using the reset command. Chances are that your shell still understands your keyboard input. Type reset and press Enter to reset your terminal or console.