# PREDEFINED VARIABLES
IN THE KORN SHELL

# How can I redefine a predefined variable?

Actually, we showed you how to do this in Chapter 5 when we redefined the PS1 variable to change our prompt. Table 13-4 shows the parameters and variables that are set by the Korn shell, and Table 13-5 shows the parameters and variables that are used by various aspects of the Korn shell.

| Parameter | Meaning or Use |
|---|---|
| # | The number of positional parameters currently set |
| - | Flags passed to the shell on startup, or by the set command |
| ? | The value returned, in decimal, of the last command |
| $ | The process number of the current shell |
| _ | Initially the fully qualified path name of the shell or script. Reassigned automatically to the last argument of the previous command |
| ! | The process number of the last background command |
| ERRNO | The value of errno as set by the last failed system call |
| LINENO | The current line number of the script being executed |
| OLDPWD | The last working directory set by cd |
| OPTARG | The last option returned by the getopts command |
| OPTIND | The index (position) of the last option returned by the getopts command |
| PPID | The process ID of the parent of the shell |
| PWD | The current working directory |
| RANDOM | A pseudo-random integer between 0 and 32767 that changes each time the parameter is referenced, using the previous value as a seed |
| REPLY | Set by the select statement, or by read with no arguments |
| SECONDS | The number of seconds since the shell was started |

Table 13-4 Parameters Set by the Korn Shell