so a terminal typically represented a single person at a single screen. Now you can have many "terminals" on one screen by opening multiple Terminal windows.

On this shell session, there isn't much happening. The first process shows that the user named jake logged in to the login process (which is controlled by the root user). The next process shows that jake is using a bash shell and has just run the `ps au` command. The terminal device `tty0` is being used for the login session. The STAT column represents the state of the process, with R indicating a currently running process and S representing a sleeping process.

The USER column shows the name of the user who started the process. Each process is represented by a unique ID number referred to as a process ID (PID). (You can use the PID if you ever need to kill a runaway process.) The %CPU and %MEM columns show the percentage of the processor and random access memory, respectively, that the process is consuming. VSV (virtual set size) shows size of the image process (in kilobytes), and RSS (resident set size) shows the size of the program in memory. START shows the time the process began running, and TIME shows the cumulative system time used.

Many processes running on a computer are not associated with a terminal. A normal Red Hat Linux system has many processes running in the background. Background system processes perform such tasks as logging system activity or listening for data coming in from the network. They are often started when Red Hat Linux boots up and run continuously until it shuts down. To see and thereby monitor all the processes running on your Red Hat Linux system, type:

```
$ ps aux | less
```

I added the pipe (|) and the less command to `ps aux` to allow you to page through the many processes that will appear on your screen. Use the spacebar to page through and type q to end the list. A pipe lets you direct the output of one command to be the input of the next command.

# ## Exitting the shell

To exit the shell when you are done, either type `exit` or Press Ctrl+D. If you are exiting from your login shell (the shell that started when you first logged in), type `logout` to exit the shell.

I just showed a few commands designed to familiarize you quickly with your Linux system. There are hundreds of other commands that you can try that are contained in directories such as `/bin` and `/usr/bin`. There are also administrative commands in `/sbin` or `/usr/sbin` directories. Many of these commands are described in the remainder of this chapter.

# # Understanding the Red Hat Linux Shell

Before icons and windows took over computer screens, you typed commands to run most computers. On UNIX systems, from which Red Hat Linux was derived, the program used to interpret and manage commands was referred to as the shell.