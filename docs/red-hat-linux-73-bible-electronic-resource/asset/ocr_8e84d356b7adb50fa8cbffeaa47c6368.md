Shell scripts are equivalent to batch files in DOS/Windows but offer greater flexibility and control through advanced looping constructs, logical operators, functions, and a larger base of commands to use. Shell scripts have much the same syntax as programming languages and are capable of handling many of the same tasks.

Nearly a dozen different shells are available in Red Hat Linux, some of which function virtually identically in an interactive environment. From a programming standpoint, there are basically two varieties, those based on the Bourne shell (sh), and those derived from the C shell (csh). All code and examples on this chapter are based on the bash (Bourne-again shell) environment, which implements a superset of the original Bourne shell. In fact, /bin/sh is a symbolic link to /bin/bash.

The syntax (that is, the way commands and options are constructed) of the C shell is similar to that of the C programming language. It has interactive capabilities that are not included in most Bourne shells. Each shell also uses different configuration files and different methods of setting shell environment variables.

# ## Executing shell scripts

Shell scripts are files of text commands, functions, environment variables, and/or comments that you can run as commands. In theory, a shell script is a way of grouping a sequence of commands instead of typing them at a shell prompt. In reality, shell scripts can be as complex as any executable program.

An advantage of shell scripts is that they can be opened in any text editor to see what it does. A disadvantage is that shell scripts often execute more slowly than compiled programs. There are two ways to execute a shell script:

+   -   The filename is used as an argument to the shell (e.g., `bash script_file`). In this method, the file does not need to be executable; it just contains a list of shell commands. The shell specified on the command line is used to interpret the commands in the script file. This is most common for quick, simple tasks.
+   -   The shell script is executed by specifying the name of the file on the command line. This requires that the first line of the shell script contain the name of the shell interpreter that is to be used (e.g., `#!/bin/bash` as the first line of the file) and that the execute bit is set. This method is most common for complex scripts that may be used frequently. The first line of a shell script is the only line where the pound sign (#) isn’t interpreted as a comment.

> **CROSS-REFERENCE:** See Chapter 3 for information on `chmod` and `read`/`write`/`execute` file permissions.

The examples in this chapter are of the second variety. When scripts are executed in either manner, options to the program may be specified on the command line. Anything following the name of the script is referred to as a *command-line argument*. These are referenced within the