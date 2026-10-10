# ## tcs h Configuration Files

tcsh has a more complicate startup sequence. A login tcsh sources the following files if they exist:

+   - /etc/csh.cshrc
+   - /etc/csh.login
+   - ~/.tcshrc or, if not found, ~/.cshrc
+   - ~/.history
+   - ~/.login
+   - ~/.cshdirs

Non-login shells only read /etc/csh.cshrc and ~/.tcshrc or ~/.cshrc.

Chapter 3 describes the contents of these text files in detail. You can use any text editor (such as the simple KDE text editor) to edit the files.

You might want to look at some of these files with more to get a feeling for the types of things that can be configured. Don't expect to understand too much at this point, however.

# ## Processes

Every running program on a UNIX system is called a process. Each process is identified by a small integer called the process ID or pid for short. You should understand how UNIX processes work. Often, you need to find out the process ID of a runaway program to terminate it. If the system is busy, you need to find out which processes are running and hogging the computer.

# ### Listing Processes

To see the processes on your Linux system, type this:

```
$ ps
```

The output will probably look something (but not exactly) like this:

PID TTY TIME CMD  
889 tty0 00:00:00 bash  
903 tty0 00:01:48 emacs  
1088 tty0 00:00:00 ps

The PID column lists the process IDs. The TTY column specifies the terminal associated with the command. The TIME column specifies how much CPU time the command has consumed. Finally, the CMD column is the name of the command that is running.