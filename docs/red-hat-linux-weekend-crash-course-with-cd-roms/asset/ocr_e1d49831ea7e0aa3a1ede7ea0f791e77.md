Sometimes, you may want to repeat the previous command but add extra arguments to it. Suppose that ls -l shows too many files. Simply repeat that command, but pipe the output through the more command as follows:

```
!! | more
```

Bash replaces the two exclamation points with the previous command and then appends | more to that command.

![](bbox=[0.13, 0.31, 0.26, 0.38])

An easy way to recall previous commands is to press the up arrow key, which causes Bash to go backward in the list of commands. To move forward in the command history, press the down arrow key.

# Using aliases for commands

To see the benefit of aliases, type the following command:

```
alias goboot='cd /usr/src/linux/arch/i386/boot'
```

This defines goboot as an alias — another name — for the text that appears within the single quotes. That text is a command to change the current directory to /usr/src/linux/arch/i386/boot.

Now that you’ve defined the alias, type the following at the Bash prompt:

```
goboot
```

Now type pwd to confirm that the current directory is indeed /usr/src/linux/arch/i386/boot.

As you can see, an alias simply is an alternative (and usually shorter) name for a lengthy command. Bash replaces the alias with its definition and performs the equivalent command.

If you no longer need an alias, use the unalias command to remove the alias. For example, if you no longer want to use the goboot alias, type:

```
unalias goboot
```

After this step, typing goboot causes you to get an error message like this:

```
goboot
bash: goboot: command not found
```