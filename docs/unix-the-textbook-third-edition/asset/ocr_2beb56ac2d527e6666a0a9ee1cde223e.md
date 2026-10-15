# EXERCISE 9.9

Create three FIFOs, called fifo1, fifo2, and fifo3, with a single command. Write down the command that you used to perform the given task.

# EXERCISE 9.10

Create a FIFO, called fifo4, with its access privileges set to read and write for owner and group, and no privileges for others. Show the command that you used to accomplish the given task.

# EXERCISE 9.11

Try the shell session given in this section on your system. Does your system produce output in the same order as shown in our session? If not, show the output produced on your system.

# SUMMARY

UNIX automatically opens three files for every command for it to read input from and send its output and error messages to. These files are called standard input (stdin), standard output (stdout), and standard error (stderr). By default, these files are attached to the terminal on which the command is executed. Thus, the shell makes the command input come from the keyboard and its output and error messages to go to the monitor screen.

These default files can be changed to other files by using redirection operators: < for input redirection and > for output and error redirection.

The three standard files can be referred to by using the digits 0 (stdin), 1 (stdout), and 2 (stderr), called the file descriptors for the three standard files. All open files in UNIX are referred to by similar integers that are used by the kernel to perform operations on these files.

In the Bourne, Korn, Bash, and POSIX shells, the greater-than symbol (>) is used in conjunction with descriptors 1 and 2 to redirect standard output and standard error, respectively.

The standard output of a command can be connected to the standard input of another command via a UNIX pipe (|). Pipes are created in the main memory and are used to take the output of a command and give it to another command without creating a disk file, effectively making the two commands talk to each other. For this reason, a pipe is called an interprocess communication (IPC) channel, which allows related commands on the same machine to communicate with each other at the shell and application levels. The processes communicating through pipes must be related through a common ancestor; the relationship is usually parent–child or sibling.

The I/O and error redirection features and pipes can be used together to implement powerful command lines. However, redirection operators and pipes alone cannot be used to redirect the standard output of a command to a file as well as connecting it to standard input of another command. The tee utility can be used to accomplish this task, sending standard output of a command to one or more files as well as to another command. The commands and tee are connected through pipes.