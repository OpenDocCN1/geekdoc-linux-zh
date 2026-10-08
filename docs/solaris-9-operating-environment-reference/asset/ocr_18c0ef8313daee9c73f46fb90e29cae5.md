```
if expression ; \\
then command ; \\
  ... ; \\
else command ; \\
  ... ; \\
fi
```

Although composed of several input lines, the escaped newline characters ensure that make treats them as all one (shell) command line.
To use the Bourne shell for control loops, use a command line of the following form.

```
for var in list ; \\
do command ; \\
  ... ; \\
ndone
```

To refer to a shell variable, use a double dollar sign ($$). This syntax expansion of the dollar sign by make.

# Command Substitutions

To incorporate the standard output of a shell command in a macro, use a definition of the following form.
MACRO:sh =command

The command is executed only once, standard error output is discarded, and newline characters are replaced with spaces. If the command has a non-zero exit status, make halts with an error.

To capture the output of a shell command in a macro, use a reference of the following form:
$(MACRO:sh)

where MACRO is the name of a macro containing a valid Bourne shell command line. In this case, the command is executed whenever the reference is evaluated. As with command substitutions, the reference is replaced with the standard output of the command. If the command has a non-zero exit status, make halts with an error.

In contrast to commands in rules, the command is not subject to command substitution; therefore, you do not need to replace a dollar sign ($) with a double dollar sign ($$).

# Signals

INT, SIGTERM, and QUIT signals received from the keyboard halt make and remove the target file being processed unless target is in the dependency list for :PRECIOUS::.

# Examples

The following Makefile says that pgm depends on two files, a.o and b.o, and that in turn depend on their corresponding source files (a.c and b.c) along with a common file incl.h

```
pgm: a.o b.o
  $(LINK.c) -o $@ a.o b.o
a.o: incl.h a.c
  cc -c a.c
```