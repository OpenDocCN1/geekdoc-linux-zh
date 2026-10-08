# glob

# glob — Shell Built-In Function to Expand a Word List

# Synopsis

glob wordlist

# Description

For csh, glob performs file-name expansion and history substitutions on wordlist. This command is much the same as the echo(1) command, but glob does not recognize \escapes. Words are delimited by null characters in the output.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUN|csu |

# See Also

csh(1), echo(1), attributes(5)

# goto — Shell Built-in Functions

# Synopsis

```
csh
goto label
```

# Description

See exit(1).

# gprof — Display Call-Graph Profile Data

# Synopsis

```
/usr/ccs/bin/gprof [-abcd1sz] [-e function-name] [-E function-name]
[-f function-name] [-F function-name] [image-file [profile-file...]]
[-n number-of-functions]
```

# Description

gprof produces an execution profile of a program. The effect of called routines is incorporated in the profile of each caller. The profile data is taken from the call-graph