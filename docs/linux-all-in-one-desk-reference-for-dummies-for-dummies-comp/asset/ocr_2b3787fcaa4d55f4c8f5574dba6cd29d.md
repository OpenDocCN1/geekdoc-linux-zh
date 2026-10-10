# Repeating previously typed commands

To make repeating long commands easy for you, *bash* stores up to 500 old commands as part of a *command history* (basically just a list of old commands). To see the command history, type **history**. *bash* displays a numbered list of the old commands, including those that you entered during previous logins.

If the command list is too long, you can limit the number of old commands that you want to see. For example, to see only the ten most recent commands, type this command:

```
history 10
```

To repeat a command from the list that the **history** command shows, simply type an exclamation point (!), followed by that command’s number. To repeat command number 3, type **!3**.

You can repeat a command without knowing its command number. Suppose you typed **more /usr/lib/X11/xdm/xdm-config** a few minutes ago and now you want to look at that file again. To repeat the previous **more** command, type the following:

```
!more
```

Often, you may want to repeat the last command that you just typed, perhaps with a slight change. For example, you may have displayed the contents of the directory by using the **ls -l** command. To repeat that command, type two exclamation points as follows:

```
!!
```

Sometimes, you may want to repeat the previous command but add extra arguments to it. Suppose that **ls -l** shows too many files. Simply repeat that command but pipe the output through the **more** command as follows:

```
!! | more
```

*bash* replaces the two exclamation points with the previous command and then appends | **more** to that command.

![](bbox=[0.13, 0.8, 0.21, 0.93])

> Here’s the easiest way to recall previous commands: Just press the up-arrow key, and *bash* keeps going backward through the history of commands you previously typed. To move forward in the command history, press the down-arrow key.