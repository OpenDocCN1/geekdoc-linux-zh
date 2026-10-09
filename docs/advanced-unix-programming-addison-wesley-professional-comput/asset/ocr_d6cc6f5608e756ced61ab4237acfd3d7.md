# Exercises

6.1. Using as many shells as you have access to (e.g., sh, ksh, bash, csh), try typing bad command lines to see what error message you get, if any, and what happens. Try these examples for starters:

```
echo abc > f1 > f2
echo def | cat < f1
echo ghi < f1 | cat
cat < f1 < f2
echo jkl | | cat
echo jki > f1
```

6.2. In the function gettoken in Section 6.4, in state INQUOTE, when getchar is called, not much attention is paid to an end-of-file. Is this a problem? Why or why not?

6.3. Add parameter replacement (e.g., echo $PATH) to the shell in Section 6.4.

6.4. Add wild-cards (file-name generation) to the shell in Section 6.4. Use the standard function glob if you have it (most systems do). If you don't have it, you can restrict matching to the last component of path names (i.e., ls */*.c is illegal).

6.5. Add a goto built-in statement to the shell of Section 6.4. Can you implement it as an external command to be run as a child process? (Hint: Review open file descriptions in Section 2.2.3.)

6.6. Add an if statement to the shell of Section 6.4.

6.7. Design and implement a menu shell. Instead of prompting for commands, it displays a menu of choices and the user simply picks one. You'll need menus for command arguments, too. Rather than building in the details of various commands, the shell should take its information about commands and their arguments from a database.

6.8. Design and implement a windowing shell. Use Curses if you have access to it.

Divide the terminal screen into halves (which is easier—a horizontal or vertical split?). Run a shell child process in each half. The user presses a function key or a control key (Ctrl-w, say) to select the active window. A command running in the inactive window continues to output to the screen, but when input is requested it blocks until the user activates the window and types a response. A window scrolls when it gets full, and the scrolled-off lines are gone forever. Only line-oriented input and output are supported. Design questions: Should the standard output of a com-