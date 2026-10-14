# Table 8-6: History Expansion Commands

| Sequence | Action |
|---|---|
| !! | Repeat the last command. It is probably easier to press the up arrow and ENTER. |
| !number | Repeat history list item number. |
| !string | Repeat last history list item starting with string. |
| !?string | Repeat last history list item containing string. |

# SCRIPT

In addition to the command history feature in bash, most Linux distributions include a program called script, which can be used to record an entire shell session and store it in a file. The basic syntax of the command is

```
script [file]
```

where file is the name of the file used for storing the recording. If no file is specified, the file typescript is used. See the script man page for a complete list of the program's options and features.

# Final Note

In this chapter we have covered some of the keyboard tricks that the shell provides to help hardcore typists reduce their workloads. I suspect that as time goes by and you become more involved with the command line, you will refer to this chapter to pick up more of these tricks. For now, consider them optional and potentially helpful.