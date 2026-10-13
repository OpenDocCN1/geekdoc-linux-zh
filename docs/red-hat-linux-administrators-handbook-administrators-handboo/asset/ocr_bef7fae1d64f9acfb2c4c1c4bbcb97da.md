This is a built-in shell command that is available in most popular shells. history displays a list of commands you have recently entered at the command line. The number of commands that history displays is limited by an environment variable called "history." For example, if you add set history = 100 to your login file, then whenever you log in, the history command remembers up to 100 command lines. The commands you see in the history can be easily rerun by entering their index number with a ! sign. For example, suppose the you see the following listings after you enter the history command:

```
1 10:25 vi irc-bot.h
2 10:25 vi irc-bot.c
3 10:26 which make
```

To run the vi irc-bot.c command again, simply enter !2 in the command line.

# set

Syntax:

```
set var = value
```

This is a built-in shell command that is available in most popular shells. set allows you to set environment variables with specific values. For example,

```
set foo = bar
```

sets a new environment variable foo to have bar as the value. To see the list of all environment variables, run set by itself. To view the value of a specific environment variable, such as path, run the following:

```
echo $path
```

This shows you the value of the named environment variable. If you use this command quite often to set a few special environment variables, add it to .login or .profile or your shell's dot file so that the special environment variables are automatically set when you log in.