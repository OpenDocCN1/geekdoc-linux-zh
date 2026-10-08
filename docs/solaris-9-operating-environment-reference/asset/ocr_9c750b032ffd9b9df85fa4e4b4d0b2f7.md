# 1360 sysV-make

executed to update the target. The first nonempty line that does not begin with a Tab or
# begins a new dependency or macro definition. You can continue shell commands across
lines with a backslash-newline (\-) sequence. Everything printed by make
(except the initial Tab) is passed directly to the shell as is. Thus, the following sequence

```
echo a\nb
```

produces

```
ab
```

exactly as the shell would. Number sign (#) and newline surround comments including
contained \-newline sequences.
The following Makefile says pgm depends on two files, a.o and b.o, and that
they, in turn, depend on their corresponding source files (a.c and b.c) and a common file
incl.h.

```
pgm: a.o b.o
cc a.o b.o -o pgm
a.o: incl.h a.c
cc -c a
b.o: incl.h b.c
cc -c b
```

Command lines are executed one at a time, each by its own shell. You can use the
SHELL environment variable to specify which make should use to execute
commands. The default is /usr/bin/sh. The first or two characters in a command
can be @, -, or -. If @ is present, printing of the command is suppressed. If a
- makes a line is printed if it is executed unless you
spec the -s option, entry .SILENT is included in Makefile, or the initial
character sequence contains a dash. The -n option specifies printing without execution;
however, if the command has the string $(MAKE) in it, the line is always executed
(see the discussion of the MADEOPTIONS macro in "make Environment" (page 1360).
-t (touch) option updates the modified date of a file without executing any
commands.

Commands returning non-zero status normally terminate make. If you specify the -i
option, the IGNORE_ variable is included in Makefile, or if the initial character
of the command contains a dash (-), the error is ignored. If you specify the -k option,
work is abandoned on the current entry but continues on other branches that do
depend on that.

Interrupt and quit delete the target unless the target is a dependent of the directive
PRECIOUS.

# make Environment

The environment is read by make. All variables are assumed to be macro definitions and
processed as before any Makefile
after the internal rules; thus, make assignments in a Makefile override
environment variables. The -e option overrides the assignments in a Makefile.
Suffixes and their associated rules in the Makefile override any identical suffixes in the
built-in rules.
The Environment variable is processed by make as containing any legal
input option (except -f and -p) defined for the command line. Further, on invocation,
make "vars" works if it is not in the environment, which puts the options into
it passes it on to invocations of commands. Thus, MAKEFLAGS always contains the