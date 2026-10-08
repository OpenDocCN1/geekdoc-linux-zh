# 810

# make

When you do not specify the -q option, the make command exits with one of the following values.

+   0 Successful completion.
>0 An error occurred.

# Files

+   makefile
Makefile Current version(s) of the make description file.
s.makefile SCCS history files for the above makefile(s) in the current directory.
s.makefile

+   SCCS/s.makefile SCCS history files for the above makefile(s).

+   make.rules Default file for user-defined targets, macros, and implicit rules.
/usr/share/lib/make/make.rules

+   Makefile for standard implicit rules and macros (not read if makefile.rules
is read).

+   .make.state State file in the local directory.

# Attributes

See attributes(5) for descriptions of the following attributes:

/usr/ccs/bin/make

| Attribute Type | Attribute Value |
| Availability | SUNWsprot |

/usr/xpg4/bin/make

| Attribute Type | Attribute Value |
| Availability | SUNWxu4t |

# See Also

ar(1), cd(1), lex(1), sccs-get(1), sh(1), sysV-make(1) yacc(1),
passwd(4), attributes(5), POSIX.2(5)
Solaris Advanced User's Guide and Programming Utilities

# Diagnostics

Don't know how to make target target

There is no makefile entry for target