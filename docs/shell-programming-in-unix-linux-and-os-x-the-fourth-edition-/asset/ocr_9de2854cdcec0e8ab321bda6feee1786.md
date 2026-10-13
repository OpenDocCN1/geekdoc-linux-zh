Now go into command mode (Esc) and use k to access previous commands from the command history:

```
```text
$ _                         Esc k       $ echo this is a test
```
```

Every time k is used, the line is replaced by the previous line from the command history, as far back as you want to go, within the constraints set with `HISTSIZE`, as discussed earlier.

```
```text
$ echo this is a test       k          $ cd /tmp
$ cd /tmp                   k          $ pwd
```
```

To execute the command being displayed, just press the Enter key.

```
```text
$ pwd                       Hit Enter
/tmp
$ _
```
```

The j command is the reverse of the k command and is used to display the next most recent command in the history. In other words, k moves you “back” in time, and j moves you “forward” in time. Try them a few times and you'll immediately see what we mean.

The / command searches through the command history for a command containing the specified string. If the / is entered followed by a string, the shell searches backward through its history to find the most recently executed command that contains that string. The command will then be displayed.

If no line in the history contains the specified string, the shell “beeps” to indicate the error. When the / is entered, the current line is replaced by a /.

```
```text
/tmp
$ _                         Esc /test    /test_
```
```

The search is begun when the Enter key is pressed.

```
```text
/test_                    Enter        $ echo this is a test
```
```

To execute the command that results from the search, Enter must be pressed again.

```
```text
$ echo this is a test                         Hit Enter again
this is a test
$ _
```
```

If the command that’s displayed isn’t the one you seek, continue the search by typing in / without a pattern and pressing Enter. The shell is smart enough to use the string that you entered the last time you executed the search command and continue from the last match shown further back in your command list.

When you’ve found the command in the history (either by k, j, or /), you can edit the command using the other vi commands we’ve already discussed. Worth noting is that by making these changes, you don’t actually change the command in the history. You’re editing a copy of the command, which will then be entered in the history as the most recent command when you press Enter.

Table 14.1 summarizes the basic vi line edit commands.