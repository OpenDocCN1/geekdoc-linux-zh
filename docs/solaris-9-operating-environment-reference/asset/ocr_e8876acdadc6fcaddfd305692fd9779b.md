# type 1457

# Exit Status

| | |
| 0 | Standard input is a terminal. |
| 1 | Standard input is not a terminal. |
| >1 | An error occurred. |

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUMvcsu |
| CSI | Enabled |

# See Also

isatty(3C), tname(3C), attributes(5), environ(5)

# Diagnostics

not on an active synchronous line
The standard input is not a synchronous terminal, and you specified -l.
not a tty The standard input is not a terminal, and you did not specify -s.

# type — Write a Description of Command Type

# Synopsis

/usr/bin/type name,...

# Description

The type command indicates how name operand would be interpreted if used as a command, type displays information about each operand, identifying the operand as a shell built-in, function, alias, hashed command, or keyword, and can display the path name of the operand where applicable.
The shell built-in version of type is similar to the type command.

# Operands

name A to be interpreted.

# Examples

```
The following example shows the output for the tty, who, and whence commands.
castle% type tty
ty is /bin/tty
castle% type who
who is a tracked alias for /bin/who
castle% type whence
```