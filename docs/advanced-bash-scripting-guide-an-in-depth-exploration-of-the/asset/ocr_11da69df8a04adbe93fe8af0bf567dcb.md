# Advanced Bash-Scripting Guide

This is one of three shell directives that effect command processing. The others are builtin and enable.

Invoking builtin BUILTIN_COMMAND runs the command BUILTIN_COMMAND as a shell builtin, temporarily disabling functions and external system commands with the name.

This either enables or disables a shell builtin command. As an example, enable -n kill disables the shell builtin kill so that Bash subsequently encounters kill, it invokes the external command /bin/kill.

The -a option to enable lists all the shell builtins, indicating whether or not they are enabled. The -f filename option enables load a builtin as a shared library (DLL) module from a properly compiled object file. [68]

This is a port of the ksh autoloader. With autoload in place, a function with an autoload declaration will load from an external file at its first invocation. [69] This saves system resources.

Note that autoload is not a part of the core Bash installation. It needs to be loaded in with enable -f (see above).

# Table 15-1. Job identifiers

| Notation | Meaning |
|---|---|
| %N | Job number [N] |
| %S | Invocation (command-line) of job begins with string S |
| %S | Invocation (command-line) of job contains within string S |
| %% | "current" job (last job stopped in foreground or started in background) |
| %+ | "current" job (last job stopped in foreground or started in background) |
| %- | Last job |
| $% | Last background process |