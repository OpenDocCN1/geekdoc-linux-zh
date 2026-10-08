
-   **-S**: If both `-k` and `-S` are specified, the last one specified is used.
-   **-n**: No execute mode. Print commands, but do not execute them. Even lines beginning with an @ are printed. However, lines that contain the string `$(MAKE)` or `$(MAKE)` or that have + as a prefix to the command are executed.
-   **-q**: Question. The make command returns a zero or non-zero status code, depending on whether the target file is or is not up-to-date. Targets are not updated with this option.
-   **-r**: Clear suffix list and do not use the built-in rules.
-   **-S**: Silent mode. Command lines are not printed to standard output before their execution. This mode is also entered if the special target name `.SILENT` appears in the makefile.
-   **-S**: Terminate if an error occurs while executing the commands to bring a target up-to-date. This is the default and the opposite of `-k`. If both `-k` and `-S` are specified, the last one given is used. This enables overriding the presence of the k flag in the MAKEFLAGS environment variable.
-   **-t**: Touch the target files (causing them to be up-to-date) rather than issue the usual commands.
-   **[macro_name=value]**: Zero or more command line macro definitions can be specified. See the Macros section.
-   **[names]**: Zero or more target names that appear in the makefile. Each target so specified is updated by make. If no names are specified, make updates the first target in the makefile that is not an inference rule.

# Environment

All variables defined in the environment (see environ(5)) are read by make and are treated and processed as macro definitions, with the exception of the SHELL environment variable which is always ignored. make automatically sets SHELL to /usr/bin/sh. Variables with no definition or empty string definitions are included by make.

There are four possible sources of macro definitions which are read in the following order: internal (default), current environment, the makefile(s), and command line. Because of this order of processing, macro assignments in a makefile override environment variables. The -e option allows the environment to override the macro assignments in a makefile. Command-line macro definitions always override any other definitions.

The MAKEFLAGS environment variable is processed by make on the assumption that it contains any legal input option (except -f, -p, and -d) defined for the command line. The MAKEFLAGS variable can also be specified in the makefile.

(XPG4 only. MAKEFLAGS in the makefile replaces the MAKEFLAGS environment variable. Command line options have precedence over MAKEFLAGS environment variable.)

If MAKEFLAGS is not defined in either of these places, make constructs the variable for itself, puts the options specified on the command line and any default options into it, and passes it on to invocations of commands. Thus, MAKEFLAGS always contains the current input options. This proves very useful for recursive makes. Even when the -n option is specified, command lines containing the string `$(MAKE)` or `$(MAKE)` are executed; hence, one can perform a `make -n` recursively on an entire software system to see what would have been executed. This is possible because the -n is put into MAKEFLAGS and passed to the recursive invocations of `$(MAKE)` or `$(MAKE)`. This is one way of debugging all of the makefiles for a software project without actually executing any of the commands.

Each of the commands in the rules is given to a shell to be executed. The shell used is the shell command interpreter (see sh(1)), or the one specified in the makefile by the SHELL macro. To ensure the same shell is used each time a makefile is executed, the line:

```
SHELL=/usr/bin/sh
```

or a suitable equivalent should be put in the macro definition section of the makefile.

# Suffixes

Target and/or dependent names often have suffixes. Knowledge about certain suffixes is built into make and used to identify appropriate inference rules to be applied to update a target (see the section on Inference Rules). The current default list of suffixes is:

```
.o .C .c .C .Cx .Cx~ .cpp .Cpp~ .cc .cc~
.y .l .i .s .s~ .sh .sh~
.h .h .H .p .P .f .f~ .r .r~
```

These suffixes are defined as the dependents of the special built-in target `.SUFFIXES`. This is done automatically by make.

Additional suffixes can be specified in a makefile as the dependents list for `.SUFFIXES`. These additional values are added to the default values. Multiple suffix lists accumulate. The order of the suffix list is significant (see the Inference Rules section). If the user wishes to change the order of the suffixes, he must first define `.SUFFIXES` with a null dependent list, which clears the current value for `.SUFFIXES`, and then define `.SUFFIXES` with the suffixes in the desired order. The list of suffixes built into make on any machine can be displayed by:

```
make -fp - 2>/dev/null </dev/null
```

The list of built-in suffixes incorporated with the definitions in a given makefile called mymakefile can be displayed by:

```
make -fp mymakefile 2>/dev/null </dev/null
```

# Inference Rules

Certain target or dependent names (such as those ending with `.o`) have inferable dependents such as `.c` and `.s`, etc. If no update commands for such a name appear in the makefile, and if an inferable dependent file exists, that dependent file is compiled to update the target. In this case, make has inference rules that allow building files from other files by examining the suffixes and determining an appropriate inference rule to use. There are currently default inference rules defined for:

### Single Suffix Rules

```
.C .c
.C .Cx~ .cXx .cpp .Cpp~ .cc .cc~
.sh .sh~
.p .p~
.f .f~
.r .r~
```

### Double Suffix Rules

+   .C.O  .C~.O  .C~.C  .C.a  .C~.a
+   .C.o  .C~.o  .C~.C  .C.a  .C~.a
+   .CXX.o  .CXX~.o  .CXX~.cXX  .CXX.a  .CXX~.a
+   .cpp.o  .cpp~.o  .cpp~.cpp  .cpp.a  .cpp~.a
+   .cc.o  .cc~.o  .cc~.CC  .cc.a  .cc~.a
+   .s.o  .S~.o  .S~.a
+   .P.o  .P~.o  .P~.p  .P.a  .P~.a
+   .f.o  .f~.o  .f~.f  .f.a  .f~.a
+   .r.o  .R~.o  .R~.r  .r.a  .r~.a
+   .y.o  .Y~.o  .Y~.y  .y.c
+   .l.o  .l~.o  .l.c
+   .h~.h  .H~.h  .hxx~.hxx  .hpp~.hpp
+   .C.o  .C~.o  .C.a  .C~.a

Double suffix inference rules (`.c.o`) define how to build `x.o` from `x.c`.

Single suffix inference rules (`.c`) define how to build `x` from `x.c`. In effect, the first suffix is null. Single suffix rules are useful for building targets from only one source file; e.g., shell procedures and simple C programs.

A tilde in the above rules refers to an SCCS file (see sccsfile(4)). Thus, the rule `.C~.o` would transform an SCCS C source file into an object file (`.o`). Since the `s.` of the SCCS files is a prefix, it is incompatible with make's suffix point-of-view. Hence, the tilde is a way of changing any file reference into an SCCS file reference.

A rule to create a file with suffix `.o` from a file with suffix `.c` is specified as an entry with `.c.o` as the target and no dependents. Shell commands associated with the target define the rule for making a `.o` file from a `.c` file. Any target name that has no slashes in it and starts with a dot is identified as an inference (implicit) rule instead of a target (explicit) rule. Targets with one dot are single suffix inference rules; targets with two dots are double suffix inference rules. Users can, in a Makefile, define additional inference rules and either redefine or cancel default inference rules.

The default inference rule for changing a `.c` file into a `.o` file might look like this:

```
.c.o:
	$(CC) $(CFLAGS) -c $<
```

and the default inference rule for changing a yacc file to a C object file might look like this:

```
.y.o:
	$(YACC) $(YFLAGS) $<
	$(CC) $(CFLAGS) -c y.tab.c
	rm y.tab.c
	mv y.tab.o $@
```

Certain macros are used in the default inference rules to permit the inclusion of optional matter in any resulting commands. For example, CFLAGS, LDFLAGS, and YFLAGS are used for compiler options to cc(1), lex(1), and yacc(1), respectively. LDFLAGS is commonly used to designate linker/loader options. These macros are automatically defined by make but can be redefined by the user in the Makefile.

The macro LIBS is, by convention, used to specify the order of inclusion of any special libraries during the linking phase of compilation. To specify a particular order of inclusion for a
