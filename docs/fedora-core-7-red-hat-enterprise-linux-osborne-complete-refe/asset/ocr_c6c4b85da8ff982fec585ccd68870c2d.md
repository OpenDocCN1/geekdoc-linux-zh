The editor used is the one specified by the shell in the **EDITOR** variable. This serves as the default editor for the `fc` command. You can assign to the **EDITOR** variable a different editor if you wish, such as Emacs instead of Vi. The next example will edit the fourth event, `cd reports`, with the standard editor and then execute the edited event:

```
```
$ fc 4
```
```

You can select more than one command at a time to be edited and executed by referencing a range of commands. You select a range of commands by indicating an identifier for the first command followed by an identifier for the last command in the range. An identifier can be the command number or the beginning characters in the command. In the next example, the range of commands 2–4 is edited and executed, first using event numbers and then using beginning characters in those events:

```
```
$ fc 2 4
$ fc vi c
```
```

The `fc` command uses the default editor specified in the **FCEDIT** special variable. Usually, this is the Vi editor. If you want to use the Emacs editor instead, you use the `-e` option and the term **emacs** when you invoke `fc`. The next example will edit the fourth event, `cd reports`, with the Emacs editor and then execute the edited event:

```
```
$ fc -e emacs 4
```
```

# ### Configuring History: HISTFILE and HISTSAVE

The number of events saved by your system is kept in a special system variable called **HISTSIZE**. By default, this is usually set to 500. You can change this to another number by simply assigning a new value to **HISTSIZE**. In the next example, the user changes the number of history events saved to 10 by resetting the **HISTSIZE** variable:

```
```
$ HISTSIZE=10
```
```

The actual history events are saved in a file whose name is held in a special variable called **HISTFILE**. By default, this file is the **bash_history** file. You can change the file in which history events are saved, however, by assigning its name to the **HISTFILE** variable. In the next example, the value of **HISTFILE** is displayed. Then a new filename is assigned to it, **newhist**. History events are then saved in the **newhist** file.

```
```
$ echo $HISTFILE
.bash_history
$ HISTFILE="newhist"
$ echo $HISTFILE
newhist
```
```

# ### Filename Expansion: \*, ?, [ ]

Filenames are the most common arguments used in a command. Often you may know only part of the filename, or you may want to reference several filenames that have the same extension or begin with the same characters. The shell provides a set of special characters that