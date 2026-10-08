# break, continue

is y
castle% biff n
castle% biff
is n
castle%

# Files

~/.login User's login file.
~/.profile User's profile file.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNmscpu |

# See Also

csh(1), mail(1), sh(1), attributes(5)

# break, continue — Shell Built-in Functions to Break Out of Loops

# Synopsis

```
sh
break [n]
continue [n]

csh
break
continue

ksh
*
break [n]
continue [n]
```

# Description

Bourne Shell
break exits from the enclosing for or while loop if any. If you specify n, break n levels.
 resumes the next iteration of the enclosing for or while loop. If you specify n, resume at the n-th enclosing loop.