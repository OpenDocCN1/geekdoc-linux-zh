have execute permission. The shell does not look through all directories but only the ones specified by the variable PATH. Refer to page 359 for more information on PATH. Also refer to the discussion of the which and whereis utilities on page 255. When it cannot find the file, bash displays the following message:

```
$ abc
bash: abc: command not found...
```

Some systems are set up to suggest where you might be able to find the program you tried to run. One reason the shell might not be able to find the executable file is that it is not in a directory listed in the PATH variable. Under bash the following command temporarily adds the working directory (.) to PATH:

```
$ PATH=$PATH:.
```

For security reasons, it is poor practice to add the working directory to PATH permanently; see the following tip and the one on page 360.

When the shell finds the file but cannot execute it (i.e., because you do not have execute permission for the file), it displays a message similar to

```
$ def
bash: ./def: Permission denied
```

See “ls -l: Displays Permissions” on page 191 for information on displaying access permissions for a file and “chmod: Changes Access Permissions” on page 193 for instructions on how to change file access permissions.

# Try giving a command as ./command

> tip
> You can always execute an executable file in the working directory by prepending ./ to the name of the file. Because ./filename is a relative pathname, the shell does not consult PATH when looking for filename. For example, if myprog is an executable file in the working directory, you can execute it using the following command (regardless of how PATH is set):

```
$ ./myprog
```

# EXECUTING A COMMAND

+   Process If it finds an executable file with the name specified on the command line, the shell starts a new process. A process is the execution of a command by Linux (page 373). The shell makes each command-line argument, including options and the name of the command, available to the called program. While the command is executing, the shell waits for the process to finish. At this point the shell is in an inactive state named sleep. When the program finishes execution, it passes its exit status (page 1029) to the shell. The shell then returns to an active state (wakes up), issues a prompt, and waits for another command.

+   The shell does not process arguments Because the shell does not process command-line arguments but merely passes them to the called program, the shell has no way of knowing whether a particular option or other argument is valid for a given program. Any error or usage messages about options or arguments come from the program itself. Some utilities ignore bad options.