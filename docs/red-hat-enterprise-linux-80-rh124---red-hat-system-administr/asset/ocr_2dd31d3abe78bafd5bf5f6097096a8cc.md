# CHANGING THE SHELL ENVIRONMENT

# OBJECTIVES

After completing this section, you should be able to set shell variables to help run commands, and edit Bash startup scripts to set environment variables to modify the behavior of the shell and programs run from the shell.

# USING SHELL VARIABLES

The Bash shell allows you to set shell variables that can help run commands or to modify the behavior of the shell. You can also export shell environment variables, which are automatically copied to programs run from shell when they start. You can use variables to make it easier to run a command with a long argument, or to apply a common setting to commands run from that shell.

Shell variables are unique to a particular shell session. If you have two terminal windows, or two independent terminal login sessions to the remote server, you are running two shells. Each shell has its own set of values for its shell variables.

# Assigning Values to Variables

Assign a value to a shell variable using the following syntax:

```
VARIABLE NAME=value
```

Variable names can contain uppercase or lowercase letters, digits, and the underscore character (_). For example, the following commands set shell variables:

```
[user@host ~]$ COUNT=40
[user@host ~]$ first_name=John
[user@host ~]$ file1=tmp/abc
[user@host ~]$ _ID=RH123
```

Remember, this change only affects the shell in you run the command, not any other shells you may be running on that server.

You can use the set command to list all shell variables that are currently set. (It also lists all functions, which you can ignore.) This list is long enough that you may want to pipe the output into the less command so that you can view one page at a time.

```
[user@host ~]$ set | less
BASH:/usr/bin/bash
BASHOPTS=checkwinsize:cdhist:complete_fullquote:expand_aliases:extglob:quote:
force_ignore:histappend:interactive_comments:progcomp:promptvars:sourcepath
BASHSOURCED=Y
...output omitted...
```