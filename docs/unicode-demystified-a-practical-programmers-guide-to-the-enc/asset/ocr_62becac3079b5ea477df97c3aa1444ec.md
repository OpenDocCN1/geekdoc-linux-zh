The test builtin can evaluate an expression in a shell script. The expression is often a comparison of two quantities or files or an inquiry about the status of a file. As all decisions GNU/Linux shell scripts, a true status is represented by the value zero; false, by any nonzero value.

The looping structures available in the Bourne Again Shell and Z Shell are for...in, for, until, and while. These structures perform one or more tasks repetitively.

The break and continue control structures alter control within loops; break transfers out of a loop, and continue transfers immediately to the top of a loop.

The trap builtin catches a signal by GNU/Linux to the process running the script and you specify what actions to be taken upon receipt of one or more signals. The trap builtin might be used, for instance, to ignore the signal when the user presses the interrupt key.

The exec builtin executes a command without creating a new process. The new command replaces the current process, assuming the same environment and PID number of that process. This builtin executes user programs and other GNU/Linux commands, when it is not necessary to return control to the calling process.

The Here document allows input to a command in a shell script to come from within the shell itself.

A function is a series of commands that, unlike a shell script, are parsed prior to being stored in main memory. Shell scripts are parsed at run time and are stored on disk. A function can be defined on the command line or within a shell script; if you want the function definition to remain in effect across login sessions, you can define it in your .bash_profile file. Like the functions of a programming language, a shell function is called by giving its name along with any arguments.

In addition to the use of control structures, builtins, functions, and the like, useful shell scripts generally use GNU/Linux utilities. The find utility, for instance, is commonplace in shell scripts that search for files in the system hierarchy and can perform a vast range of tasks, from simple to complex.

A well-written shell script adheres to the use of standard techniques, such as specifying the shell to execute the script on the first line of the script, verifying the number and type of arguments that the script is called with, displaying a standard usage message to report command line errors, and redirecting all informational messages to standard error.