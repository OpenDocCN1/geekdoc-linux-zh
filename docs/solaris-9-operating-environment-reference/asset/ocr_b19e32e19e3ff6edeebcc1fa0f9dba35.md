# which

# 1547

```
atoplot: /usr/ucb/atoplot
basename: /usr/bin/basename /usr/ucb/basename
bgplot: /usr/ucb/bgplot
biff: /usr/ucb/biff
cc: /usr/ucb/cc
chown: /usr/bin/chown /usr/ucb/chown
clear: /usr/bin/clear /usr/ucb/clear
... (More lines not listed)
castle%
```

# Files

+   /usr/src/*
/usr/(doc,man)/*
/etc, /usr/(lib,bin,ucb,old,new,local)

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNwcpu |

# See Also

chdir(2), attributes (5)

# Bugs

Because딨 uses chdir(2) to run faster, you must specify full path names with the -M, -S, or -B options; that is, path names must begin with a slash (/).

# which — Locate a Command; Display Its Path Name or Alias

# Synopsis

```
/usr/bin/which [filename]...
```

# Description

which takes a list of names and looks for the files that would be executed these names given as commands. Each argument is expanded if it is aliased and searched for along the user's path. Both aliases and path are taken from the user's .cshrc file.

> Note — which is not a shell built-in command; it is the UNIX command, /usr/bin/which.