2> should be replaced with >&. This command may take several minutes, perhaps hours, depending on the size of the file structure, system load (in terms of the number of users logged on), and the number of processes running on the system. So if you want to do some other work on the system while the command executes, you cannot do so because the command executes in the foreground.

```
$ find / -name foo -print > foo.paths 2> /dev/null
...
$
```

The find command is a perfect candidate for background execution because, while it runs, you have access to the shell and can do other work. Thus, the preceding command should be executed as follows:

```
$ find / -name foo -print > foo.paths 2> /dev/null &
[1] 23467
$
```

The number shown in brackets is returned by the shell and is the job number (also called job ID) for the process; the other number is the PID of the process. Here, the job number for the find command is 1 and the PID is 23467. A job is a process that is not running in the foreground and is accessible only at the terminal with which it is associated. Such processes typically run in the back or are suspended processes.

The commands that perform tasks that do not involve user intervention and take a long time to finish are good candidates for background execution. Some examples are sorting large files (sort command), compiling large programs (cc, gcc, CC, make, etc.), computationally intensive programs such as one that determines if a large integer number is prime, and searching a large file structure for one or more files (find command). Commands that do terminal I/O, such as the vim editor, are, of course, not good candidates for background execution. The reason is that, when such a command executes in the background, it stops accepting input from the keyboard. The command needs to be brought back to the foreground before it can start running again. The fg command allows you to bring a background process to the foreground.

While running a command in the foreground, you might need to suspend it in order to go back to the shell, do something under the shell, and then return to the suspended process. For example, say that you are in the middle of editing a C program file with vim and need to compile the program to determine whether some errors have been corrected. You can save changes to the file, suspend vim, compile the program to view the results of the compilation, and return to vim. You can suspend a foreground process by pressing <Ctrl+Z>, move a suspended process to the foreground by using the fg command, and move a suspended process to the background by using the bg command. So you can suspend vim by pressing <Ctrl+Z>, compile the program to identify any other errors, and resume the suspended vim session by using the fg command.