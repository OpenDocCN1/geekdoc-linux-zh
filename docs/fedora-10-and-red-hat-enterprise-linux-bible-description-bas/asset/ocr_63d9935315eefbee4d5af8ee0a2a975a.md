# Part I: Getting Started in Fedora and RHEL

The path directory order is important. Directories are checked from left to right. So, in example, if there is a command foo located in both the /bin and /usr/bin directories, the one in /bin is executed. To have the other foo command run, you type either the full path to command or change your PATH variable. (Changing the PATH and adding directories to it is described later in this chapter).

Not all the commands that you run are located in directories in your PATH. Some commands are built into the shell. Other commands can be overwritten by aliases that define any commands and options that you want to run. There are also ways of defining a function that consists of a series of commands. Here is the order in which the shell checks for the commands you use:

+   1. Aliases — Names set by the alias command that represents a particular command and a set of options. (Type alias to see what aliases are. Often, aliases allow you to define a short name for a long, complicated command. Some users use aliases to map a command name from another operating system to the similar utility in Linux.

+   2. Reserved word — Words that are reserved by the shell for special use. Many of these are words that you would use in programming-type functions, such as do, while,

+   3. Function — A set of commands that are executed within the current shell.

+   4. Built-in command — A command that is built into the shell.

+   5. File system command — This is a command that is stored in and executed from the computer's file system. These are the commands that are indicated by the value of the PATH variable.

To find out where a particular command is taken from, you can use the type command. (If you are using a shell other than bash, use the which command instead.) For example, if to find out where the bash shell is located, type the following:

```
$ type bash
bash /bin/bash
```

Try these few words with the type command to see other locations of commands: which, case, and return. If a command resides in several locations, you can add the -a option to have all the known locations of the command printed.

> TIP: When you run a command and receive an error message that the command was not found or permission to run the command was denied. In the first case, check that you spelled the command correctly and that it is located in your PATH. In the second case, the command may be in the PATH, but not executable. Adding execute permissions to a command is described later in this chapter.