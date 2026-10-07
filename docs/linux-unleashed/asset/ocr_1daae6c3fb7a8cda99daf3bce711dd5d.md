The following are examples of setting key bindings:

```
bindkey ^W kill-whole-line
bindkey ^S beginning-of-line
```

# ## Other Neat Stuff

tcsh supports several neat features that none of the other shells discussed in this book supports. This section lists a few of the most useful of these extended features.

# ### Correcting Spelling Errors

This feature, which is not available with any of the other shells discussed in this book, is a dream come true for many people (including me). If you're plagued by recurring typos, this feature alone might cause you to use tcsh over any of the other shells. You can tell tcsh to correct spelling errors in a command that you entered, and you can also tell it to automatically try to correct commands that it can't figure out.

The first function isn't quite as useful because you must know that you have made a typing mistake before you actually execute the command. This feature is invoked by pressing Esc+8 on the command line before you press Enter.

For example, suppose you want to change to the /usr/X386/X11/bin directory, so you type the following command on the command line:

```
cd /usr/X387/X11/bun
```

If you caught the typing errors before you executed the command (by pressing the Enter key), you can correct the errors by pressing Esc+8. tcsh then tries to correct the spelling of the command and changes the command to read

```
cd /usr/X386/X11/bin
```

You can now press the Enter key, and the command executes just as you wanted. Obviously this command has some limitations because the shell can't (yet) read your mind, but for simple character transpositions or capitalization errors, it works very nicely.

The second method of instructing tcsh to perform spelling corrections on your commands is to set the correct tcsh variable. This variable, depending on what options you use, tells tcsh to try to correct spelling errors in command names or anywhere in the command. The syntax for setting the correct variable is one of the following:

```
set correct=cmd or
set correct=all
```