# User Process

A user process, also known as an interactive process, is a process runs via a Linux shell. All Linux shells provide a command line where a user can enter the names of commands and programs he wishes to run. When a user enters a command, such as `ls -al`, or a program, such as `/install-sh`, the shell creates a copy of itself as a new process and replaces the new process with the command or program mentioned in the command line. In simple terms, the shell runs the named command which assigns the name to an object so that it may referenced by an action or program as another process.

# Parent and Child Processes

A parent process is any process that starts or spawns and control another processes. A child process is a process that is initiated by another process. It can also be spawned by its parent process. For example, if you are working in X Windows System and you open an xterm (terminal emulator). From the xterm, you run the command `find -- -name *.jpg` to find all .jpg files in your home directory. In this example, the terminal window is the parent process of the find command. If the terminal window is closed, the find command ceases to run because the find command was run as a child process of the term process. Stopping a parent process automatically halts the child process, so when the terminal window is closed, the find command process stops running.

Let's learn about some commands that we use in Linux processes.

Commands in Linux Processes

+   - The ps command
+   - The kill command
+   - The killall command

Now, you learn about these in detail one by one.

The kill command works together with the ps command

+   - With the `ps` command (ps stands for process status) you find out the identity of the program you want to get rid of.
+   - Then kill will finish it off.

Let's discuss about `ps` command in detail:

# The ps Command

The `ps` command is used to display the currently running processes on Unix/Linux systems. If you know the function of Task Manager, which pops up under Windows NT/2000/XP when you press Ctrl+Alt+Del, then you can easily understand what `ps` does on Linux. It can show you the processes on your system in various formats. Let's take the following example: To display all processes owned by the current user, type `ps ux` and hit return:

```
$ ps ux
```

This shows a listing of processes similar to:

```
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
deven 3064 0.1 3.6 18324 9088 ? S 17:55 0:00 /usr/bin/gnome-
```