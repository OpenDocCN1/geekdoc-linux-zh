Any command that is executed is a *process*. Processes can be initiated by the user, or by the operating system itself. Further, processes can create other processes as they execute. If process A is executed and creates process B as part of its execution, B is called a *child process* of A, and A is the *parent process* of B. A process can have many child processes, but only one parent process.

Each process has an associated *environment*, a series of variables that define certain parameters for the process. The environment is expressed as a list of variables and their values. Both the variable's name and value are represented as strings that can be made up of most standard characters. When a child process is created, it inherits the environment of its parent process. A child process can then modify its environment before passing it to its own child processes.

For example, the `PATH` variable indicates which directories the system should look in to execute a command, if no directory path is specified in the command. In Linux, even the processes run by the operating system search through directories in the `PATH` variable: you can use the path mechanism anywhere you try to execute a command. Even if there is no variable `PATH` in the environment, the system always checks the directories `/bin` and `/usr/bin` for suitable commands.

The variables can be configured and made available to the system using the `export` command. This is done as shown in the following example:

```
`# PATH=/bin
# export PATH`
```

To view the setting for an environment variable, the `echo` command is used. When specifying a variable to display the variable name is preceded by the `$` symbol. An example of this is shown here:

```
`# echo $PATH
/bin:/usr/bin:/usr/local/bin`
```

![](bbox=[0.1, 0.71, 0.16, 0.76])

Pay close attention to the files listed in the following sections. It is very important to understand that the shell configuration files are used to configure the shell environment for users.

![](bbox=[0.1, 0.78, 0.16, 0.83])

These configuration files are covered in more detail in Chapter 10.

# ## Editing the PATH variable

![](bbox=[0.1, 0.85, 0.18, 0.87])

+   1.3 GNU and UNIX Commands
+   * Work effectively on the UNIX Command Line. Includes invoking commands in the path and outside the path.