# Getting the Most Out of the C Shell

```
% alias netcom
echo Netcom login: taylor;rlogin netcom.com
% alias sunworld
echo SunWorld login: taylor;rlogin sunworld.com
```

![](bbox=[0.125, 0.215, 0.191, 0.273])

You can't enter alias sunworld to list the list and sunworld aliases because alias command means to replace the alias for netcom and the the command sunworld.

# CAUTION

Separating commands with a semicolon is the UNIX way of having multiple commands on a single line, so when I enter the alias netcom, for example, it's as if I'd entered all these commands one after another:

```
echo Netcom login: taylor
login netcom.com
```

+   4. Two aliases worth examining closely are those for the cd and setprompt commands. As you learn in a few moments, you can set your prompt to be just about any characters you'd like.(Hang on for just a paragraph or two, and you will learn all of what's occurring in the next example!) I like to have my prompt indicate where the file system I'm currently working. To ensure the prompt is always up to date, I simply alias the command so that each time I change directories, the prompt is recalculated.

```
% alias cd
chdir ! : setprompt
% alias setprompt
set prompt="$System($cdw):! : "
```

> The cd command does the same thing as cd and is intended for use within aliases as shown. If you find chdir easier to remember than cd, you can use it.

# JUST A MINUTE

Aliases are what makes the C shell and Korn shell such great interfaces. I can, and do, easily customize the set of commands and the default flags (look at all the options I set as default values for the rm command). I turn off some commands that I don't want to run accidentally. Let your imagination run with aliases. If you decide you like one and if you're using csh, add the alias to your cshrc so it's permanent (.profile if you're using ksh). If you want to turn off an alias, you can use the unalias command, and it's gone until you log in again. For example, unalias netcom would temporarily remove from the shell the netcom alias shown earlier.

# SUMMARY