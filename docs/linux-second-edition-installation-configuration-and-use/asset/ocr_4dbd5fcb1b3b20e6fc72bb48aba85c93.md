# COMMAND EXECUTION 395

The above command searches the whole file system for files that end in the ter 'sh'. The list of files is written to the file result. Since the command is executed in the background, work can continue immediately. Output [1] 334 means that the background process has the PID number 334. PID stands for identification. The PID number is of interest if the process is to be prematurely terminated with kill. The number in square brackets indicates the number of background processes started by the bash and is generally of no interest.

If you forget the & when starting a command, you do not need to wait until it terminates or stop brutally with Ctrl+C. Instead, you should interrupt the program with Ctrl+Z and continue it with bg as a background process.

# Execution of several commands

After the & character you can also specify an additional command. In this case, the first command is executed in the background, while the second one is executed in the foreground. In the following example, find is started again in the background, and at the same time ls displays the current directory list:

```
user$ find -name *sh > result & ls
```

If a semicolon is entered instead of the & character, the bash executes the commands one after the other and in the foreground:

```
user$ ls; date
```

The above command first displays the current directory list and then the current date. If these two pieces of information are to be redirected to a single file with >, both commands must be enclosed in parentheses. This causes the two programs to be executed by the same shell (normally, a new shell is started for each command).

```
user$ (ls; date) > contents
```

Now the file contents contains the file list produced by ls and the current date determined by date. The parentheses cause the two programs to be executed by the same shell and therefore yield a common result. (Normally, a new shell is started for the execution of each command.)

The pair && and || can be used to execute commands conditionally, that is, depending on the result of another command:

```
user$ command1 && command2
```

execute-command1. Only if this executes successfully (no error, return value=0) is command2 executed.

```
user$ command1 || command2
```

executes-command1. Only if an error occurred during execution of this command (return value !=0) is command2 executed.

Additional possibilities for the construction of conditions and branches are referred by the shell command if; however, this is of interest only for shell programming (see page 415).