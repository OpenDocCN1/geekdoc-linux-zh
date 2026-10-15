# EXPLANATION (CONTINUED)

+   3 ls !:3 reads: go to the last command on the history list and get the fourth word (words start at 0) and pass it to the ls command as an argument. (!file3 is the fourth word.)

+   4 The bang (!) with the dollar sign ($) refers to the last argument of the last command on the history list. The last argument is c.

+   5 The caret (^) represents the first argument after the command. The bang (!) with the ^ refers to the first argument of the last command on the history list. The first argument of the last command is a.

+   6 The asterisk (*) represents all arguments after the command. The ! with the * refers to all of the arguments of the last command on the history list.

+   7 The last command from the history list is printed but not executed. The history list is updated. You could now perform caret substitutions on that line.

# 13.5.4 Command-Line Editing

The bash shell provides two built-in editors, emacs and vi, that allow you to interactively edit your history list. When you use the editing features at the command line, whether in vi or emacs mode, the readline functions determine which keys will perform certain functions. For example, if using emacs, Ctrl-P allows you to scroll upward in the command-line history, whereas if using vi, the k key moves upward through the history list. Readline also controls the arrow keys, cursor movement, changing, deleting, inserting text, and redoing or undoing corrections. Another feature of readline is the completion feature previously discussed in "Command and Filename Completion" on page 783.

This allows you to type part of a command, filename, or variable, and then, by pressing the Tab key, the rest of the word is completed. There are many more features provided by the Readline library designed to help manipulate text at the command line.

The emacs built-in editor is the default built-in editor and is modeless, whereas the vi built-in editor works in two modes, one to execute commands on lines and the other to enter text. If you use UNIX, you are probably familiar with at least one of these editors. To enable the vi editor, add the set command listed below and put this line in your ~/.bashrc file. To set vi, type what's shown in the following example, at either the prompt or in the ~/.bashrc file.

# EXAMPLE 13.34

```
set -o vi
```

# EXPLANATION

Sets the built-in vi editor for command-line editing of the history list.

4. If the set -o (editor) has not been set, but the EDITOR variable has been set to either emacs or vi, then bash will use that definition.