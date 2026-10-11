# Search paths

The `PATH` variable is a colon-separated list of directories to be searched when an executable is run. For example:

```
PATH=/sbin:/bin:/usr/sbin:/usr/bin:/usr/bin/X11:/usr/local/sbin :/usr/local/bin
```

Each of the directories in the list is checked in order when a command is entered at the command prompt.

The `CDPATH` variable is a colon-separated list of directories that are checked when the `cd` command is used. By default this variable is not set. Consider the following setting:

```
CDPATH=~/Documents:~/Graphics
```

If the user types `cd Project`, the shell will first check for a Project directory in the current directory, then in `~/Documents`, and then `~/Graphics`.

# Exporting variables

Before a subprocess, such as an application or another shell, can use a variable, the variable must be exported. By default, a variable can only be used only in the shell where it was created; this is called the variable’s *scope*. Exporting the variable increases its scope. This is done with the following syntax:

```
export variable_name
```

You can also combine commands and export a variable while naming it, such as the following:

```
export variable_name=value
```

An environment variable can also be set up only for a given process, without changing the variable in the current shell. This is done with the following syntax:

```
variable_name=value command
```

To list all current environment variables and their values, use the `export` command with no options or with the `-p` option. To list all shell variables, even those not exported as environment variables, use the `set` command.

![](bbox=[0.12, 0.86, 0.2, 0.9])

> When a variable is declared, it is a shell variable. When it is exported, it becomes an environment variable.