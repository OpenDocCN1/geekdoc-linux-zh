-S.  If both -k and -S are specified, the last one specified is used.

+   -n  No execute mode. Print commands, but do not execute them. Even lines beginning with an @ are printed. However, lines that contain the string $(MAKE) or $(MAKE) or that have + as a prefix to the command are executed.

+   -q  Question. The make command returns a zero or non-zero status code, depending on whether the target file is or is not up-to-date. Targets are not updated with this option.

+   -r  Clear suffix list and do not use the built-in rules.

+   -S  Silent mode. Command lines are not printed to standard output before their execution. This mode is also entered if the special target name .SILENT appears in the makefile.

+   -S  Terminate if an error occurs while executing the commands to bring a target up-to-date. This is the default and the opposite of -k. If both -k and -S are specified, the last one given is used. This enables overriding the presence of the k flag in the MAKEFLAGS environment variable.

+   -t  Touch the target files (causing them to be up-to-date) rather than issue the usual commands.

+   [macro_name=value]  Zero or more command line macro definitions can be specified. See the Macros section.

+   [names]  Zero or more target names that appear in the makefile. Each target so specified is updated by make. If no names are specified, make updates the first target in the makefile that is not an inference rule.

# Environment

All variables defined in the environment (see environ(5)) are read by make and are treated and processed as macro definitions, with the exception of the SHELL environment variable which is always ignored. make automatically sets SHELL to /usr/bin/sh. Variables with no definition or empty string definitions are included by make.

There are four possible sources of macro definitions which are read in the following order: internal (default), current environment, the makefile(s), and command line. Because of this order of processing, macro assignments in a makefile override environment variables. The -e option allows the environment to override the macro assignments in a makefile. Command-line macro definitions always override any other definitions.

The MAKEFLAGS environment variable is processed by make on the assumption that it contains any legal input option (except -f, -p, and -d) defined for the command line. The MAKEFLAGS variable can also be specified in the makefile.

(XPG4 only. MAKEFLAGS in the makefile replaces the MAKEFLAGS environment variable. Command line options have precedence over MAKEFLAGS environment variable.)

If MAKEFLAGS is not defined in either of these places, make constructs the variable for itself, puts the options specified on the command