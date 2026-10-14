For the Bourne, Korn, and POSIX shells, the general format for redirecting both standard output and standard error to the same file is the following:

```
command1 > outfile 2>&1 errorfile
```

The command entry is an operating system command. The 1> symbol redirects the standard output. The outfile entry is the file to which the process writes the standard output. The 2>&1 symbol tells the shell to write the standard error (file descriptor 2) in the file associated with the standard output (&1), outfile.

For the C shell, the general format for redirecting both standard output and standard error to the same file is the following:

```
command >& outfile
```

The command entry is an operating system command. The outfile entry is the file to which the process writes the standard output. The right-angle bracket and ampersand (>&) symbol tells the shell to write the standard output and standard error to the same file specified by outfile.

# 6.3 Running Several Processes Simultaneously

The operating system can run a number of different processes at the same time. This capability makes it a multitasking operating system, which means that the processes of several users can run at the same time.

These different processes can be from one or multiple users. As a result, you do not have to enter commands one at a time at the shell prompt. Instead, you can run both foreground and background processes simultaneously. The following sections describe both foreground and background processes.

# 6.3.1 Running Foreground Processes

Usually, when you enter a command on the command line, you wait for the results to display on your screen. Commands entered singly at the shell prompt are called foreground processes.

Most commands take a short time to execute – perhaps a second or two. However, some commands require longer execution times. If a long-duration command runs as a foreground process, you cannot execute other commands until the current one finishes. As a result, you may want to run a long-duration command as a background process. The following section describes background processes.

# 6.3.2 Running Background Processes

Generally, background processes are most useful with commands that take a long time to run. Instead of tying up your screen by entering a