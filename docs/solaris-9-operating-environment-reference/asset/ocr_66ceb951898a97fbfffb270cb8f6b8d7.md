# 1254

set, unset, setenv, unsetenv, export — Shell Environment Variable Built-in Functions

# Synopsis

sh

```
set [--aehkntuvx [argument...]]
unset [name...]
export [name]
```

csh

```
set [var = value]
set var[n] = word
unset pattern
setenv [VAR word]
unset variable
```

ksh

```
set [+aehkmnoptuvx] [+o option]... [+A name] [arg...]
unset [-f name...]
.
export [name= value]...
```

# Description

Bourne Shell

The Bourne shell set command has the following options.

+   -a Mark variables that are modified or created for export.
-e Exit immediately if a command exits with a non-zero exit status.
-f Disable file-name generation.
-h Locate and remember function commands as you define functions (function commands are normally located when the function is executed).
-k Put all keyword arguments in the environment for a command, not just those that precede the command name.
-n Read commands, but do not execute them.
-t Exit after reading and executing one command.
-u Treat unset: variables as an error when substituting.
-v Print shell input lines as they are read.
-x Print commands and their arguments as they are executed; useful in $1 to -.

Using + instead of - turns these options off. You can also use these options when invoking the shell. The current state of set is found in $-$. The remaining arguments are positional parameters and are assigned, in order, to $1, $2, ... If you specify no arguments, the values of all names are printed.