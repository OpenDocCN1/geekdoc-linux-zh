
## The Process File System

  In Chapter 5, “The File System,” you were introduced to the virtual file system mounted in the /proc directory. The proc file system (PROCFS) stores pointers to objects (or logical addresses) being processed in memory, with one file for each active process running on your system; the name of each file (represented as a folder or container in the CDE File Manager) is the PID number of the process it represents. To see how this might work, use the ps command as follows to view a user’s running process: `ps -eaf | grep <username>`. In Figure 15.8, you can see that this returns two lines, the (Bourne) shell that was spawned when barries logged in, and the grep command that was just issued. Having established that the shell is PID 11978, I was able to use the cd command to switch to the 11978 directory in the proc file system and `ls -1` to list the contents of the directory so that I could view an image of the process with all of its child processes in view. Figure 15.8 shows you this listing.

![](img/256e02a6afce528d264a8d911fa0ff20_638_0.png)

![](img/256e02a6afce528d264a8d911fa0ff20_638_1.png)

**NOTE** Sometimes the grep command does not show itself in the process command’s listing. That is done to keep people from wondering why grep shows up when it is initiated from another system.

Notice that, as all other processes do, the shell process has a number of subdirectories (indicated by the first letter d in the attributes listing) that store state information and control functions related to the state of the shell process. Each directory and subdirectory also has a watch-point access that is used to control memory access of the process.

Although the proc file system is represented as if it were a real file system, it cannot be viewed or modified with standard commands such as cat, file, rm, pg, commands that you would use to manipulate standard files. Solaris provides some commands that you can use to display information about the proc file system, the so-called proc tools. One command that accesses the proc file system you are already familiar with, the ps (process) command. The ps command returns system information to you quickly because it only has to read the information and attributes of the objects in the proc file system to respond. Other programs can read the proc file system, but only one program, referred to as the controlling process, can write to it. Figure 15.9 shows the output of several of the proc commands for the shell process shown previously in Figure 15.8.

Here is a list of some of the commands that display information from the process file system:

- **pfiles**: When you give the `pfiles <PIDnumber>` command, Solaris returns the status and control information for any open files relating to the process you specify. The pfiles command is one of the more commonly used proc tools because it exposes all of the operational dependencies between applications and their data files.
- **pflags**: Use the `pflags <PIDnumber>` command to display signal and flag information for a process.
- **pcred**: The `pcred <PIDnumber>` command prints the effective, real, and saved UIDs and GIDs associated with a process. Those numbers are owner and group identification numbers of the person who executed the process.
- **pldd**: The `pldd <PIDnumber>` command displays the dynamically linked libraries called by a process.
- **pmap**: The `pmap <PIDnumber>` command prints an address map for each process.

Figure 15.10 shows the `pmap 1` command exposing the memory assignment of the initialization process.

### FIGURE 15.9
The output of various proc commands

![](img/256e02a6afce528d264a8d911fa0ff20_640_0.png)

- **psig**: Use the `psig <PIDnumber>` command to display process signal actions.
- **pstack**: The `pstack <PIDnumber>` command performs a stack trace (similar to an LWP) and outputs the results in hexadecimal form.
- **ptree**: The `ptree <PIDnumber>` command outputs the hierarchical tree representation of a process and its subprocesses. Figure 15.9 shows an example. Again, the `ptree` command is very useful for exposing operational dependencies.
- **pwait**: Use the `pwait` command to display the status of a process after it terminates.
- **pwdx**: Use the `pwdx <PIDnumber>` command to display a process's current working directory.

### FIGURE 15.10
*The pmap command for the init process*

![](img/256e02a6afce528d264a8d911fa0ff20_641_0.png)

To execute these commands, you need to specify them as follows:

```
# /usr/proc/bin/pccommand <PIDnumber>
```

If the `/usr/proc/bin` directory is in your PATH environment, you need to specify only the command itself.

The `lsof` (list open file) command is another command that isn't included in Solaris 8 but that you might find useful to download and install. The program lists information about open files used by active processes. Using `lsof`, you can identify which process gave rise to a file in the tmp directory by specifying that file as an argument to the command. You can also identify processes that continue to write to unlinked files and consume space, something that isn't tracked with other commands. The `lsof` command is useful when you want to unmount a file system that has open system files on it, something Unix doesn't allow you to do. You can use `lsof` to determine which file is open and kill the process associated with that file. You can download the `lsof` program from `ftp://vic.cc.purdue.edu/pub/tools/unix/lsof`.

Although `lsof` isn't included with Solaris, the `fuser` command is, and it performs a similar function. The `fuser` command identifies processes using a file or file structure and will display the PIDs of the processes that are using the files specified in the command as arguments. Each PID is identified by a letter code, as follows: c, the process is using a file in the current directory; m, the process is using a mapped file; o, the process is using the file as an open file; r, the process is using the file as its root directory; t, the process is using the file as a text file; and y, the process is using the file as its controlling terminal.

## Controlling Processes

Several of the proc tools can be used to control processes. The following are among the more useful:

- **pgrep**: The `pgrep <processname>` command displays information about the process. The PID is the number displayed in the first column.
- **kill**: Use the `kill <PIDnumber>` command to kill a process. An alternative is to use `pkill <processname>`.
- **prun**: The `prun <PIDnumber>` command restarts a process.
- **pstop**: The `pstop <PIDnumber>` command stops a process.
- **ptime**: When you use the `ptime <PIDnumber>` command, it times the process by using microstate accounting.
- **psig**: This command lists the signal actions of each process.
- **pwait**: The `pwait -v <PIDnumber>` command waits for a process(s) to terminate prior to execution.

As before, to execute these commands, you need to specify them as follows:

```
# /usr/proc/bin/pcommand <PID>
```

If the `/usr/proc/bin` directory is in your PATH environment, you need to specify only the command itself.

You can control processes through the use of signals, using commands that mirror many of the commands that were just described. Processes use signals to communicate with one another. Signals are created from the `signal()` call inside a C program, or they can be sent directly to a program from a shell. There are several different signal types, each providing a way for applications to communicate with one another and to call for application and system services, something that is commonly referred to as *interapplication communications*.

When you issue some keyboard commands, especially simple ones like Ctrl+C, you are issuing a signal to the foreground program to terminate or kill the current process. The kill command at the command line also terminates a process. A Ctrl+Z keystroke is the signal to suspend a foreground process but not kill it.

The kill command is a good example of a command that issues some simple signals.

The syntax of the kill command is as follows:

```
kill <option> <PID> list
```

The only significant options are the signal type followed by a process or job list. A root user can kill any process, but other users can terminate only processes that they own. If you don't specify the signal type, then the kill command uses the software termination signal, SIGTERM or signal 15. All three of Solaris's shells—the Bourne, Korn, and C
