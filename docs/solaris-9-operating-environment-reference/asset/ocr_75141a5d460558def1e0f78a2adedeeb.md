# The Suffixes List

The suffixes list is given as the list of dependencies for the .SUFFIXES: special-function target. The default list is contained in the SUFFIXES macro (see "Table of Predefined Macros" on page 797 for the standard list of suffixes). You can define additional .SUFFIXES: targets; a .SUFFIXES: target with no dependencies clears the list of suffixes. Order is significant within the list; make selects a route that corresponds to the target's suffix and the first dependency-file suffix found in the list. To put suffixes at the head of the list, clear the list and replace it with the new suffixes followed by the default list, as shown below.

```
.SUFFIXES:
.SUFFIXES: suffixes ($SUFFIXES)
```

A tilde (-) indicates that if a dependency with the indicated suffix (minus the ~) is out of SCCS, its most recent version should be retrieved, if necessary, before the target is processed.

# Library Maintenance

A target name of the following form refers to a member or a space-separated list of members in an ar(1) library.

```
lib(member...)
```

You must give the dependency of the library member on the corresponding file as an explicit entry in the makefile. This entry can be handled with a pattern-matching rule of the following form:

```
lib(.s) : %s
```

where .s is the suffix of the member; this suffix is typically ,o for object libraries.
A target name of the following form refers to the member of a randomized object library that defines the entry point named symbol.

```
lib(symbol)
```

# Command Execution

Command lines are executed one at a time, by each own process or shell. Shell commands, not notably cd, are ineffective across an unescaped newline in the makefile. A line is printed (after macro expansion) just before being executed. This printing is suppressed if the line starts with a $, if there is a .SILENT: entry in the makefile, or if you run make with the -s option. Although the -n specifies printing without execution, lines containing the macro $ are ignored regardless, and lines containing the @ special character are printed. The -t (touch) option updates the modification date of a file without executing any rules. This behavior can be dangerous when sources are maintained by more than one person.

make invokes the shell with the -e (exit-on-errors) argument. Thus, with semicolon-separated command sequences, execution of the latter depends on the success of the former. This can be overridden by starting the command line with a - or by writing a script that returns a non-zero status only as appropriate.

# Bourne Shell Constructs

To use the Bourne shell if control structure for branching, use a command line of the following form.