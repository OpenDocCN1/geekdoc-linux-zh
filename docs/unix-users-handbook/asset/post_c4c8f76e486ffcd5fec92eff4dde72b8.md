
evaluates to

```
file1.c file2.c file3.c
```

Macro values can contain references to other macros (see WARNINGS):

```
ONE = 1
TWELVE = $(ONE)2
```

The value of `$(TWELVE)` is set to `$(ONE)2` but when it is used in a target, command, or include line, it is expanded to `12`. If the value of `ONE` is subsequently changed by another definition further down in the makefile or on the command line, any references to `$(TWELVE)` reflect this change.

Macro definitions can also be specified on the command line and override any definitions in the makefile.

(XPG4 only. Macros on the command line are added to the MAKEFLAGS environment variable. Macros defined in the MAKEFLAGS environment variable, but without any command line macro, adds the macro to the environment overwriting any existing environment variable of the same name.)

Certain macros are automatically defined for make (see Built-in Macros). See the Environment section for a discussion of the order in which macro definitions are treated.

The value assigned to a macro can be overridden by a conditional macro definition. A conditional macro definition takes on the form `target := string1 = string2`. When the target line associated with target is being processed, the macro value specified in the conditional macro definition is in effect. If `string1` is previously defined, the new value of `string1` will override the previous definition. The new value of `string1` takes effect when target or any dependents of target are being processed.

## INCLUDE LINES

If the string `include` appears as the first seven letters of a line in a makefile, and is followed by one or more space or tab characters, the rest of the line is assumed to be a file name and is read and processed by the current invocation of make as another makefile after any macros in the filename have been expanded.

## General Description

make executes commands previously placed in a makefile to update one or more target names. Target names are typically names of programs. If no `-f` option is specified, the filenames `makefile`, `Makefile`, `s.makefile`, `SCCS/s.makefile`, `s.Makfile` and `SCCS/s.Makefile` are tried in that order. If `-f -` is specified, the standard input is used. More than one `-f` option can be specified. The makefile arguments are processed in the order specified. A space between the `-f` and the filename must be present, and multiple makefile names must each have their own `-f` option preceding them. The contents of a makefile override the built-in rules and macros if they are present.

If no target names are specified on the command line, make updates the first target in the (first) makefile that is not an inference rule. A target is updated only if it depends on files that are newer than the target. Missing files are deemed to be out-of-date. All dependents of a target are recursively updated, if necessary, before the target is updated. This effects a depth-first update of the dependency tree for the target.

If a target does not have any dependents specified after the separator on the target line (explicit dependents), any shell commands associated with that target are executed if the target is out-of-date.

A target line can have either a single or double colon between the target name or names and any explicit dependent names. A target name can appear on more than one target line, but all of those lines must be of the same (single- or double-colon) type. For the usual single-colon case, at most one of these target lines can have explicit commands associated with it. If the target is out-of-date with any of its dependents on any of the lines, the explicit commands are executed, if they are specified, or else a default rule can be executed. For the double-colon case, explicit commands can be associated with more than one of the target lines containing the target name; if the target is out-of-date with any of the dependents on a particular line, the commands for that line are executed. A built-in rule may also be executed.

Target lines and their associated shell command lines are also referred to as rules. Hash marks (`#`) and new-line characters surround comments anywhere in the Makefile except in rules. Comments in the rules depend on the setting of the SHELL macro.

The following makefile says that `pgm` depends on two files: `a.o` and `b.o`, and that they in turn depend on their corresponding source files (`a.c` and `b.c`) and a common file `incl.h`:

```makefile
OBSJS = a.o b.o

pgm: $(OBSJS)
cc $(OBSJS) -o pgm

a.o: incl.h a.c
cc -c a.c

b.o: incl.h b.c
cc -c b.c
```

Command lines are executed one at a time, each by its own shell. Each command line can have one or more of the following prefixes: `-`, `@`, or `+`. These prefixes are explained below.

Commands returning non-zero status normally terminate make. The `-i` option or the presence of the special target `.IGNORE` in the makefile cause make to continue executing the makefile regardless of how many command lines cause errors, although the error messages are still printed on standard output. If `-i` is present at the beginning of a command line, any error returned by that line is printed to standard output but make does not terminate. The prefix `-` can be used to selectively ignore errors in a makefile. If the `-k` option is specified and a command line returns an error status, work is abandoned on the current target, but continues on other branches that do not depend on that target. If the `-k` option is present in the MAKEFLAGS environment variable, processing can be returned to the default by specifying the `-S` option.

The `-n` option specifies printing of a command line without execution. However, if the command line has the string `$(MAKE)` or `$<MAKE>` in it or `+` as a prefix, the line is always executed (see discussion of the MAKEFLAGS macro under Environment). The `-t` (touch) option updates the modified date of a file without executing any commands.

A command line is normally printed before it is executed, but if the line has a `@` at the beginning, printing is suppressed. The `-s` option or the presence of the special target `.SILENT` in the makefile suppresses printing of all command lines. The `@` can be used to selectively turn off printing. Everything printed by make (except the initial tab) is passed directly to the shell without alteration. Thus,

```bash
echo a\
b
```

produces `ab` just as the shell would.

The `-b` option allows old makefiles (those written for the old version of make) to run without errors. The old version of make assumed that if a target did not have any explicit commands associated with it, the user intended the command to be null, and would not execute any `.DEFAULT` rule that might have been defined. The current version of make operates in this mode by default. However, the current version of make provides a `-B` option which turns this mode off so that if a target does not have explicit commands associated with it and a `.DEFAULT` rule is defined, the `.DEFAULT` rule is executed. Note that the `-b` and `-B` options have no effect on the search and possible location and execution of an appropriate inference rule for the target. The search for a built-in inference rule other than `.DEFAULT` is always performed.

The signals SIGINT, SIGQUIT, SIGHUP, and SIGTERM (see signal(5)) cause the target to be deleted unless the target depends on the special name `.PRECIOUS`.

## Options

The following is a brief description of all options and some special names. Options can occur in any order. They can be specified separately, or together with one `-`, except for the `-f` option.

- **-b** Compatibility mode for old (Version 7) makefiles. This option is turned on by default.
- **-B** Turn off compatibility mode for old (Version 7) makefiles.
- **-d** Debug mode. Print out detailed information on files and times examined. (This is very verbose and is intended for debugging the make command itself.)
- **-e** Environment variables override assignments within makefiles.
- **-f makefile** Description file name, referred to as the makefile. A file name of `-` denotes the standard input. The contents of the makefile override the built-in rules and macros if they are present. Note that the space between `-f` and makefile must be present. Multiple instances of this option are allowable (except for `- -`), and are processed in the order specified.
- **-p** Write to standard output the complete set of macro definitions and target descriptions.
- **-i** Ignore error codes returned by invoked commands. This mode is also entered if the special target name `.IGNORE` appears in the makefile.
- **-k** When a command returns nonzero status, abandon work on the current entry, but continue on other branches that do not depend on that target. This is the opposite of
