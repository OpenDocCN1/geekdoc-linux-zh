Many Linux systems automatically create a core dump when a program fails. The Linux operating system usually puts a file named *core* in the directory the program was run from.

# ### Understanding a Core Dump

A core dump is a recording of what was in memory at the time of program failure. The reasoning here is that a programmer can take the core dump and determine what went wrong during program execution. But with the number and types of tools available today, the chance of a programmer using a core dump file is very small.

When a program crash causes a core dump, the file that is written to disk varies in size. The contents of the file will be everything that pertains to the file that was in memory at that particular time. Larger files will have larger core dumps.

# ### Managing Core Files

Core files can be restricted in size or even eliminated with the **ulimit** command. The ulimit command will, among other things, limit the *size* of core dumps. To limit the size of a core dump to 100K, use the command *ulimit -c 100*.

The *-c* option sets the maximum core dump value. In many systems, you should use a value of 0 to prevent any core dumps. The default value for core dumps on Red Hat Linux is 0. Use a value of *unlimited* if you want the maximum core dump saved to disk.

To find any core dump files on the system, use the **find** command. To find all core dumps starting in the root (/) directory, use the command *find / -name core*. **find** is the command, */* is the starting directory, the *-name* option says to use a pattern, and *core* is the pattern to look for. You can get the owner and creation date of the core file from a directory listing of the file. To see which program caused the dump, try using the **gdb**, GNU Debugger, program. *gdb* performs a lot of different functions, but the *-c* option will examine a core dump and return the program name that generated it as well as other information. To see the information about a core dump, use the *gdb -c core* command.

The directory listing can also be produced with the *find* command. For example, *find / -name core -type f -ls* will find all core files and produce a directory listing. The *-type f* command will suppress listing directories named *core*.

You can easily delete unneeded core files. You could even write a cron job that searches for core files and then deletes them. But keep in mind that a core dump indicates a problem with a program. If you are getting several core dumps, you need to have someone available to check the files.

# ## ■ MANAGING PROCESSES

A process is a program that is currently running on Linux. Any program running on the system is termed a process. The shell in which you type in commands is a process. The **ls** command is a process. The Web browser is a process. Each of these programs can run other processes, and at any given time hundreds of processes can be running.

Because the Linux operating system is a multiserver, multitasking operating system, each user on the system can run multiple processes. If user *jnjsmith* is connected and using *vi*, and *root* is also connected and running *vi*, *vi* will be associated with two processes. Even a single user can have multiple copies of a program running at the same time. Tracking processes becomes extremely important when you have multiple users running processes.

Managing processes is one of the major duties of a Linux administrator. An admin has the power to kill a process, restart a process, or give it a different priority. When a process is started, it is assigned a process ID (PID). The PID is used to manage and monitor the process.