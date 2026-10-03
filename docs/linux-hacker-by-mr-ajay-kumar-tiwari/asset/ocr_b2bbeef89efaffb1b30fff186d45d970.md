# Linux Hack

Ajay Kumar Tiwari

```
# cp ~/longname.txt /really/a/very/long/path/long-filename.txt
```

```
# ls -l !cp:2
```

```
ls -l /really/a/very/long/path/long-filename.txt
```

In the example below, !cp:$ searches for the previous command in history that starts with cp and takes the last argument (in this case, which is also the second argument as shown above) of cp and substitutes it for the ls -l command as shown below.

```
# ls -l !cp:$
```

```
ls -l /really/a/very/long/path/long-filename.txt
```

# Hack 63. Disable the usage of history using HISTSIZE

If you want to disable history all together and don’t want bash shell to remember the commands you’ve typed, set the HISTSIZE to 0 as shown below.

```
# export HISTSIZE=0
```

```
# history
```

# [Note:

History did not display anything]

# Hack 64. Ignore specific commands from the history using HISTIGNORE

Sometimes you may not want to clutter your history with basic commands such as pwd and ls. Use HISTIGNORE to specify all the commands that you want to ignore from the history.