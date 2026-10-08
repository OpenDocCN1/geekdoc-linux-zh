# help, sccs-help — Ask for Help Regarding SCCS Error or Warning Messages

# Synopsis

```
/usr/ccs/bin/help [argument]...
```

# Description

See sccs-help(1).

# history, fc — Process Command History List

# Synopsis

```
sh
/usr/bin/fc [first][last]
/usr/bin/fc -1 [-nr] [first][last]
/usr/bin/fc -s [old=new] [first]
```

```
csh
history [-hr] [n]
```

# ksh

```
fc -e [old=new] [command]
fc -e editor [-nlr] [first][last]
```

# Description

Command history creates a numbered list of the most recent commands that you have used. You can display these commands and reuse them as originally issued. You can also change a command by editing it. The syntax and arguments for history commands differ for each shell.

# /usr/bin/fc

The fc command lists or edits and reexec commands previously entered to an interactive shell.
The command history list references commands by number. The first number in the list is chosen arbitrarily. The relationship of a number to its command does not change except when you log in and no other process is accessing the list, at which time the system may reset the numbering to start the oldest retained command at number (usually 1). When the number reaches the value in HISTORYSIZE or 128 (whichever is greater), she may wrap the numbers, starting the next command with a lower number (usually 1). Despite this optional wrapping, fc maintains the time-ordering sequence of commands. For example, if four commands in sequence are the numbers 32766, 32767, 1 (wrapped), and 2 as they are executed, command 32767 is considered the command previous to 1, even though its number