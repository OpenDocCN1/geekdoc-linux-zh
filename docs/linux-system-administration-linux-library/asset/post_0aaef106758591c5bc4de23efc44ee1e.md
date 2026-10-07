
The ls command may be used to verify that the FIFO was created:

```
$ ls -l test_fifo
prw-rw-r-- 1 user user 0 Jan 29 14:50 test_fifo
```

# Sockets

Sockets are virtual connections between two processes. Unlike named pipes, sockets may be unidirectional or bidirectional. The standard input-output library contains a socket library function, called socket(), which creates a communication endpoint and returns a file descriptor containing its local host's network address and the port number to which the second process may attach in order to communicate with the first. If you have ever used an Internet address in the format http://12.34.56.78:10, you were connecting to a specific socket.

# Devices

Linux recognizes two kinds of devices, differing in the way they exchange data with the CPU. The first type is the random-access block device, which serves as SCSI, floppy, or IDE disk drives. A block device file is a buffered file. Data is added to the buffer until some predetermined event occurs, typically a full buffer. At this point the buffer is flushed to the device, and the data-collection process begins again. Your hard drives are prime examples of block devices. If data were saved to a hard drive character by character, it would be exceedingly slow.

The second type of device is the character device, such as a tape drive, modem, or serial mouse. Character device files are used for unbuffered reads and writes. This means that the data is sent out as soon as it is received. The character device /console is a great example. Of course, you don't want your system buffering the keystrokes before sending them to the console. You want to see them as they are being typed.

Devices of either type are represented in the filesystem as device files and are stored in the /dev directory, which also includes sockets and pipes. The /dev/printer device is one such socket. When you read or write a device file, the data comes from or goes to the device represented by that file. For instance, if you used the command and directed the output to /dev/printer, the output that would have been written to the screen will be piped to the printer represented by /dev/printer.

# Processes

The filesystem that we have examined is only one of the internals of Linux. This filesystem by itself is static. The activity on a Linux system is represented as processes, which open and manipulate files within the filesystem.

Each program that is run by a computer's Central Processing Unit (CPU) is called a process. A command may include many processes. There are several processes running at any one time on a Linux system. As a system administrator, you will be directly responsible for ensuring that the necessary processes are run and the schedule by which they are run. You are further responsible for managing the system so that the higher-priority processes get the CPU's attention. Last, you must ensure that the memory space is adequate to house all processes that must be run. To do these things, you need to know the fundamental details about what a process is and how it works.

# The Concept of Multitasking

The most precious resource in the system is the CPU. There is usually only one CPU, so its usage must be optimized. Linux is a multiprocessing operating system, which means that one of its goals is to share our CPU time among various processes. If there are more processes than CPUs, the rest of the processes must wait for the CPU to become available. Multiprocessing is conceptually simple; processes execute until some situation forces them to stop. Typically this is because a system resource is needed unavailable. In a multiprocessing system, several processes are kept in memory at the same time so when one process is forced to stop, the CPU can be used by another process instead of sitting idle. The CPU is shared among multiple processes (tasks); hence the name multitasking.

# Types of Processes

There are three basic types of processes: interactive processes, batch processes, and daemon processes. The kernel manages these processes and assigns each a unique process ID (PID) in an ascending order until the defined process name is reached; at this point it starts at the first unused number again. The only process ever assigned a PID of 1 is init process, which has a parent PID of 0 distinguish it from the other processes. We'll talk more about this important process in a moment.

Processes are owned in the same way that files are owned; the ID of the user who starts the process is assigned as the real user ID of the process. Likewise, the group ID of the user is assigned as the real group ID of the process. But it is not the real user ID and group ID that determine the process's access rights and who can start and stop it. Instead, the effective UID and GID are used. If the executable has permission setuid, then the process will be run as the owner of that file executed it and will allow access for anyone in the group it was assigned. The assumed UID and GID are referred to as the effective UID and GID. If the executable has not been set suid, the real UID and GID are also the effective UID and GID.

WARNING It's somewhat common to use a setuid binary to allow ordinary users to perform tasks that would otherwise require superuser privileges. The mount command, for example, has its suid bit set and is owned by root, so ordinary users can mount partitions under certain circumstances. This practice is potentially dangerous, however, a bug in a suid root program can give local users superuser access to the system. Programs that are routinely installed in this way are therefore subjected to extraordinary security scrutiny. You should not use this feature willy-nilly, because it can easily produce a security breach.

# Interactive Processes

Some processes are run interactively by users in a terminal session. If you log into a Linux system and run a process, it is an interactive process. If you want to run a process in the background, you can use the fg and bg commands. However, if you launch an X program from an xterm or other terminal window, however, the becomes unresponsive unless you include the ampersand in the command. If you use Ctrl+Z to regain control of the xterm, the X program you launched from the term becomes unresponsive unless you type bg to allow both processes to run.

Technically, interactive processes in X work the same as they do in text mode; however, GUI environments include default methods of launching programs that are effectively the same as appending ampersand on a command line. Running an X program in the background doesn't make the X program inaccessible, though; it opens a window and displays its output. Your experience is therefore one in which programs appear to run side-by-side, and you use mouse clicks, or perhaps merely movements, bring one process or another to the foreground. All the visible programs are active and running, even if you are not doing much when you're not interacting with them.

To see what processes are running, you can use the jobs utility. To bring a process to the foreground, use the fg command. To move a process to the background, use the bg command.

```
$ jobs
[1] + Stopped  tar -zcf /dev/st0 /
```

```
[1] - Stopped  tar -zcf /dev/st0 /
```

```
[1] + Running   tar -zcf /dev/st0 /
```

```
$ tar -zcf /dev/st0 &
[2] 4036
```

Batch processes are submitted from a queue and have no association with a terminal. Batch processes are great for performing recurring processes at some time when the system usage is low. To accomplish this on a Linux system, use the batch and commands. The command is really pretty simple to use. Let's assume that you want to run the tar command that we just used in the interactive process example at 2:00 in the morning tomorrow. You would use the at command as shown below:

```
# at 2:00
at> tar -zcf /dev/st0 /
```
