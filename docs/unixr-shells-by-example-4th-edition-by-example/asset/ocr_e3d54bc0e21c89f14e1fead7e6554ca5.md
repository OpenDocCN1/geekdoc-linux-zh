finishes execution and then, if necessary, will report the status of the exiting program. A prompt will appear and the whole process will start again. The order of processing the command line is as follows:

+   1. History substitution is performed (if applicable).
+   2. Command line is broken up into tokens, or words.
+   3. History is updated (if applicable).
+   4. Quotes are processed.
+   5. Alias substitution and functions are defined (if applicable).
+   6. Redirection, background, and pipes are set up.
+   7. Variable substitution ($user, $name, etc.) is performed.
+   8. Command substitution (echo "Today is `date`") is performed.
+   9. Filename substitution, called globbing (cat abc.??, rm * .c, etc.) is performed.
+   10. Command is executed.

# 1.4.2 Types of Commands

When a command is executed, it is an alias, a function, a built-in command, or an executable program residing on disk. Aliases are abbreviations (nicknames) for existing commands and apply to the C, TC, Bash, and Korn shells. Functions apply to the Bourne (introduced with AT&T System V, Release 2.0), Bash, and Korn shells. They are groups of commands organized as separate routines. Aliases and functions are defined within the shell's memory. Built-in commands are internal routines in the shell, and executable programs reside on disk. The shell uses the path variable to locate the executable programs on disk and forks a child process before the command can be executed. This takes time. When the shell is ready to execute the command, it evaluates command types in the following order:

+   1. Aliases
+   2. Keywords
+   3. Functions
+   4. Built-in commands
+   5. Executable programs

If, for example, the command is xyz the shell will check to see if xyz is an alias. If not, is it a built-in command or a function? If neither of those, it must be an executable program residing on the disk. In order to execute the command, the shell must then search the path to find out where the command is located in the directory structure in order to execute it. This process is illustrated in Figure 1.2.