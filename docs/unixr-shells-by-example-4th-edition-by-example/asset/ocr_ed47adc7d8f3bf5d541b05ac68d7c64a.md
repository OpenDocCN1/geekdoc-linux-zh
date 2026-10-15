# The fc Command.

The fc command, also called the fix command, can be used in two ways: (1) to select commands from the history list, and (2) to edit the commands in either the vi or emacs editor, or for that matter, any editor on your system.

In the first form, fc with the -l option can select specific lines or ranges of lines from the history list. When the -l switch is on, the output goes to the screen. For example, fc -l, the default, prints the last 16 lines from the history list, fc -l 10 selects lines numbered 10 through the end of the list, and fc -l -3 selects the last three lines.

The -n switch turns off the numbering of commands in the history list. With this option on, you could select a range of commands and redirect them to a file, which in turn could be executed as a shell script. The -r switch reverses the order of the commands.

The second form of fc is described in "Command-Line Editing" on page 793.

# Table 13.6 The fc Command

| Argument | Meaning |
|---|---|
| -e editor | Puts history list into editor |
| -l n-n | Lists commands in range from n to m |
| -n | Turns off numbering of history list |
| -r | Reverses the order of the history list |
| -s string | Accesses command starting with string |

# EXAMPLE 13.30

```
1 $ fc -l
4   ls
5   history
6   exit
7   history
8   ls
9   pwd
10  clear
11  cal 2000
12  history
13  vi file
14  history
15  ls -l
16  date
17  more file
18  echo a b c d
19  cd
20  history
```