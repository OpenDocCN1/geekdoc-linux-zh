When it cannot find the executable file, the Bourne Again Shell (bash) displays a message such as the following:

```
$ abc
bash: abc: command not found
```

One reason the shell may not be able to find the executable file is that it is not in a directory in your PATH. Under bash the following command temporarily adds the working directory (.) to your PATH:

```
$ PATH=$PATH:.
```

For security reasons, you may not want to add the working directory to PATH permanently; see the adjacent tip and the one on page 307.

# Try giving a command as ./*command*

**tip** You can always execute an executable file in the working directory by prepending ./*to the name of the file. For example, if **myprog** is an executable file in the working directory, you can execute it with the following command, regardless of how **PATH** is set:

```
$ ./myprog
```

When the shell finds the program but cannot execute it (you do not have execute permission for the file that contains the program), it displays a message similar to

```
$ def
bash: ./def: Permission denied
```

See “ls -l: Displays Permissions” on page 203 for information on displaying access permissions for a file and “chmod: Changes Access Permissions” on page 204 for instructions on how to change file access permissions.

# EXECUTING THE COMMAND LINE

**Process** If it finds an executable file with the same name as the command, the shell starts a new process. A process is the execution of a command by Linux (page 314). The shell makes each command-line argument, including options and the name of the command, available to the called program. While the command is executing, the shell waits for the process to finish. At this point the shell is in an inactive state called *sleep*. When the program finishes execution, it passes its exit status (page 930) to the shell. The shell then returns to an active state (wakes up), issues a prompt, and waits for another command.

The shell does not process arguments Because the shell does not process command-line arguments but only hands them to the called program, the shell has no way of knowing whether a particular option or other argument is valid for a given program. Any error or usage messages about options or arguments come from the program itself. Some utilities ignore bad options.

# EDITING THE COMMAND LINE

You can repeat and edit previous commands and edit the current command line. See pages 140 and 318 for more information.