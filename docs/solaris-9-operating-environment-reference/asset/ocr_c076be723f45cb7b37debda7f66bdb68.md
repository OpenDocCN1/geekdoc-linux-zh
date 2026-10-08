# See Also

csh(1), ksh(1), line(1), set(1), sh(1), attributes(5), environ(5)

# readonly — Shell Built-In Function to Protect the Value of the Given Variable from Reassignment

# Synopsis

```
sh
readonly [name...]
ksh
**
readonly [name=value]..
```

# Description

Bourne Shell
The names you specify are marked readonly, and the values of the names cannot be changed by subsequent assignment. If you specify no arguments, a list of all readonly names is printed.

Korn Shell
The given names are marked readonly and cannot be changed by subsequent assignment.
 the readonly command, ksh(1) commands that are preceded by one or two asterisks (*) are treated specially in the following ways.

+   - Variable assignment lists preceding the command remain in effect until the command completes.
- I/O redirections are processed after variable assignment.
- Errors abort a script that contains them.
- Words following a command preceded by ** that are in the format of a variable assignment are expanded with the same rules as a variable assignment. This means that tilde substitution is performed after the equal sign and word splitting and file-name generation are not performed.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNWcsu |

# See Also

ksh(1), sh(1), typeset(1), attributes(5)