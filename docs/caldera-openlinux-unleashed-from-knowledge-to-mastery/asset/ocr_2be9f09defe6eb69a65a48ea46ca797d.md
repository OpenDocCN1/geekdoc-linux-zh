can also delete text from the command line by using the **Backspace** or **Delete** keys. Most users should find these simple editing commands sufficient, but, for those who do not, `tesh` also supports a wide range of equivalent `emacs` and `vi` editing commands.

Another method of using the history file is to display and edit the history list using a number of other editing commands that `tesh` provides. The **history** command can be invoked by any one of three different methods.

First, the history list may be displayed to the screen as follows:

```
history [-nr] [n]
```

+   *   The **n** option is used to specify the number of commands to display. If the **n** option is not used, the **history** command will display the entire history list.
+   *   The **-h** option causes **history** to remove the command numbers and timestamps that are usually present in the output of the **history** command.
+   *   The **-r** option tells **history** to display the commands in reverse order, starting with the most recent command.

Second, the contents of the history file or the history list may be modified as follows:

```
history -S |-L |-M [filename]
```

+   *   The **-S** option writes the history list to a file.
+   *   The **-L** option appends a history file to the current history list.
+   *   The **-M** option merges the contents of the history file with the current history list and sorts the resulting list by the timestamp contained with each command.

![](bbox=[0.13, 0.65, 0.9, 0.67])

> All the options for the second form of the **history** command use the `filename` option as the name of the history file. If no `filename` is specified, the **history** command will use the `value` of the `histfile` variable. If the `histfile` variable isn't set, it will use the `~/.history` (home directory) file.

Third, the current history list may be cleared with this command:

```
history -c
```

In addition to the **history** command and its options, `tesh` also contains many history navigation and editing commands. The following commands are used to navigate through the history list: