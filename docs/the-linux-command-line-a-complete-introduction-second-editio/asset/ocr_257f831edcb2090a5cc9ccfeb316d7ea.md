| Sequence | Action |
|---|---|
| !! | Repeat the last command. It is probably easier to press the up arrow and ENTER. |
| !number | Repeat history list item number. |
| !string | Repeat last history list item starting with string. |
| !?string | Repeat last history list item containing string. |

I caution against using the !string and !?string forms unless you are absolutely sure of the contents of the history list items.

Many more elements are available in the history expansion mechanism, but this subject is already too arcane, and our heads may explode if we continue. The “HISTORY EXPANSION” section of the bash man page goes into all the gory details. Feel free to explore!

# SCRIPT

In addition to the command history feature in bash, most Linux distributions include a program called script that can be used to record an entire shell session and store it in a file. The basic syntax of the command is as follows:

```
script file
```

where file is the name of the file used for storing the recording. If no file is specified, the file typescript is used. See the script man page for a complete list of the program’s options and features.

# Summing Up

In this chapter, we covered some of the keyboard tricks that the shell provides to help hardcore typists reduce their workloads. As time goes by and we become more involved with the command line, we can refer