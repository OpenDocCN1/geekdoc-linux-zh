# SuSE System Administration
Part III

+   - Backspace/Delete—Only one of these two keys can be selected as the erase key, which erases the previous character typed. For more information, read the Linux Keyboard Setup mini-HOWTO.

+   - End-of-File, Usually Ctrl+D—When a program is reading its standard input from the keyboard and you want to let it know that you've typed everything, you press Ctrl+D. ("Usually" indicates that this option is shell dependent and may differ depending upon shell you are using.)

+   - Word-Eraser, Usually Ctrl+W—This combination deletes the last word you typed.

+   - Kill-Line, Usually Ctrl+U—This kills the entire line of input so that you can start again.

+   - Interrupt, Usually Ctrl+C—This kills the current program. Some blocks hit at this time when the program might leave the terminal in a strange state if it were unexpectedly killed.

+   - Suspend, Usually Ctrl+Z—This key sends a suspend signal to the program you're using. The result is that the program is stopped temporarily, and you can get the shell prompt again. You can then put program (job) in the background and do something else.

+   - Quit, Usually Ctrl+\ (Ctrl+Backslash)—Sends a Quit signal to the current program, programs that ignore Ctrl+C can be stopped with Ctrl+\, but programs ignoring Ctrl+C are often doing so for a reason.

+   - Stop, Usually Ctrl+S, and Start, Usually Ctrl+Q—These keys stop and restart terminal output temporarily, which can be useful if a command produces a lot of output, although it can be more useful to repeat the command and pipe it less.

You can examine many other terminal modes and settings with the stty command. This command has a built-in set of sensible settings for terminals, and typing stty to find the current settings usually shows you the differences from its "sane" settings:

```
$ stty
speed 9600 baud; line = 0;
```

> Tip
If ever find that your terminal state is messed up, you can usually fix it with the command $ stty sane and Ctrl+j. Note that you finish the command Ctrl+j, rather than Enter (which is the same as Ctrl+m). The inert option might have