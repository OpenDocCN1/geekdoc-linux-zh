command to be substituted in place of the command name itself". There are two ways this can be done. The first is to enclose the command like this:

```
$ (command)
```

The second is to enclose the command in back quotes like this:

```
`` `command` ``
```

The command will be executed in a sub-shell environment and the standard output of the shell will replace the command substitution when the command finishes.

# **Arithmetic Expansion**

Arithmetic expansion is also allowed and comes in the form:

```
$ (expression)
```

The value of the expression will replace the substitution. Eg:

```
```
#!/bin/sh
echo $(1 + 3 + 4)
```
```

Will echo “8” to stdout

# **Control Constructs**

The flow of control within SH scripts is done via four main constructs; if... then... elif..., else..., do..., while..., for... and case....

***If.. Then.. Elif.. Else***

This construct takes the following generic form; the parts enclosed within ([]) and () are optional:

```
```
if list
then list
[elif list
then list] ...
[else list]
fi
```
```