permissions set for each file. (Permissions and configuring shell property files are described later in this chapter.) Other information in the listing includes the number of hard links to the file (column 2), size of each file in bytes (column 4) and the date and time each file was most recently modified (column 5).

> **NOTE:** A symbolic link is a file that points to another file, effectively allowing you to have multiple filenames representing a single physical file. Permissions for a symbolic link appears as lrwxrwxrwx, but are not interpreted as full read/write/execute permissions. If you try to open a symbolic link, the permissions on the file that link points to (the original file) determine whether or not you can access the file.

# Checking system activity

In addition to being a multituser operating system, Linux is also a multitasking system. *Multitasking* means that many programs can be running at the same time. An instance of a running program is referred to as a *process*. Linux provides tools for listing running processes, monitoring system usage, and stopping (or killing) processes when necessary.

The most common utility for checking running processes is the **ps** command. With **ps**, you can see which programs are running, the resources they are using, and who is running them. The following is an example of the **ps** command:

```
```
$ ps au
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
root 2146 0.0 0.8 1908 1100 tty0 Ss+ 14:50 0:00 login -- jake
jake 2147 0.0 0.7 1836 1020 tty0 Ss+ 14:50 0:00 -bash
jake 2310 0.0 0.7 2592 912 tty0 R+ 18:22 0:00 ps au
```
```

In this example, the **a** option asks to show processes of all users who are associated with your current terminal, and the **u** option asks that user names be shown, as well as other information such as the time the process started and memory and CPU usage. The concept of terminal comes from the old days, when people worked exclusively from character terminals, so a terminal typically represented a single person at a single screen. Now you can have many “terminals” on one screen by opening multiple Terminal windows.

On this shell session, there isn’t much happening. The first process shows that the user named **jake** logged in to the login process (which is controlled by the root user). The next process shows that **jake** is using a bash shell and has just run the **ps** command. The terminal device **tty0** is being used for the login session. The **STAT** column represents the state of the process, with **R** indicating a currently running process and **S** representing a sleeping process. (A *sleeping* process is one that is still active, but is waiting for some event to complete before continuing. It may be waiting for someone to type something at a shell or for a process to send information it requested.) A small **s** indicates a session leader and **+** indicates the foreground process group.

The **USER** column shows the name of the user who started the process. Each process is represented by a unique ID number, referred to as a process ID (PID). (You can use the PID if you ever need to kill a runaway process.) The **%CPU** and **%MEM** columns show the percentage