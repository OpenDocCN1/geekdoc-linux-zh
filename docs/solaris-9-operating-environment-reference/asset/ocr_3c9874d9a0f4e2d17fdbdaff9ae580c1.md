# 318

# eqn, neqn, checkeq

# Exit Status

If command is invoked, the exit status of env is the exit status of command, otherwise, the env command exits with one of the following values:

+   - 0 Successful completion.
- 1-125 An error occurred.
- 126 command was found but could not be invoked.
- 127 command could not be found.

# Attributes

See attributes(5) for descriptions of the following attributes:

# /usr/bin/env

| Attribute Type | Attribute Value |
| Availability | SUN/wcu |
| CSI | Enabled |

# /usr/xpg4/bin/env

| Attribute Type | Attribute Value |
| Availability | SUN/wxcu4 |
| CSI | Enabled |

# See Also

ksh(1), sh(1), exec(2), profile(4), attributes(5), environ(5), XPG4(5)

# eqn, neqn, checkeq — Typeset Mathematics Test

# Synopsis

```
/usr/bin/eqn [-dxy] [-fn] [-pn] [-sn] [file]...
/usr/bin/neqn [file]...
/usr/bin/checkeq [file]...
```

# Description

eqn and neqn are language processors to assist in describing equations. eqn is a preprocessor for troff(1) and is intended for devices that can print troff output neqn is a preprocessor for noroff(1) and is intended for use with terminals. Usage is almost always:

```
castle$ file... | troff
castle$ file... | noroff
```

If you specify no files, eqn and neqn read from the standard input. A line beginning with * marks the start of an equation; the end of an equation is marked by a line