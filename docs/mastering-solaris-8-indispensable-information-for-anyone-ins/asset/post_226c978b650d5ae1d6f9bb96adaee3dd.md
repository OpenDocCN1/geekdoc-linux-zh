
- **-e (or -A) option**  The `-e` option reports on everything, including all system processes.
- **-d option**  Lists all processes.
- **-f option**  Generates a full listing.
- **-g (or -G) option**  The `-g` option lists process information for a single group, and the `-G` option lists the processes for a list of groups.
- **-j option**  Displays the session identifier (SID).
- **-l `<format>` option**  Generates a long listing with detailed information.
- **-L `<Format>` option**  The `-L` option outputs a list of lightweight processes (LWPs) that are running on your system. LWPs are virtual CPU or execution resources that are designed to optimize the use of CPU resources based on priority and scheduling class.
- **-o `<Format>` option**  Outputs the results of `ps` command according to the format you specify. The `ps` man pages have a description of these formats in the "Display Formats" section.
- **-p `<PID>` list option**  Displays the processes belonging to the PID number(s) specified in the comma- or space-delimited list.
- **-P option**  Lists the CPU ID that a process is bound to.
- **-u `<UID>` list option**  Displays the processes belonging to the username that has the UID(s) specified as a comma- or space-delimited list.

Figure 15.3 shows the output of the `ps -ef` command on a system running several programs. The command returns a list of the active processes or jobs running on your system. The display for a workstation running only a screen capture utility runs about two screenfuls worth of information. When you use the `-c` option to display process classes, the kernel processes are the ones in the SYS class. Figure 15.4 shows the output for the `ps` command used with the `-efc` options; notice that the third column displays the class.

### FIGURE 15.3

The *ps -ef* command returns a list of the processes running on your system.

![](img/256e02a6afce528d264a8d911fa0ff20_628_0.png)

Table 15.1 includes descriptions of the columns you see in the various output displays of the *ps* command.

> **WARNING** When the *-c* option is used, the higher the PRI listing, the higher the priority. If you don't use the *-c* option, the higher the PRI, the lower the priority. This can sometimes cause much confusion.

### FIGURE 15.4

*The ps command with the -efC option returns the processes belonging to a cell.*

![](img/256e02a6afce528d264a8d911fa0ff20_629_0.png)

### TABLE 15.1: THE OUTPUT COLUMNS OF THE ps COMMAND

| **Title** | **Description** |
| :--- | :--- |
| ADDR | Memory address in hexadecimal format. |
| C | Processor utilization. |
| CLS | Class of process: SYS is a kernel process, TS is a terminal state, and IA is interactive. (This column is displayed when you use the -c option.) |
| CMD | The command line that initiated the process, truncated so that it fits on a single line. |
| F | Flags belonging to the process, used for compatibility with previous versions of Solaris. (This column is displayed when you use the -1 option.) |
| **NI** | Niceness value, used to determine the priority. (This column is displayed when you use the `-1` option.) |
| **PID** | Process ID number. |
| **PPID** | Parent process ID number. |
| **PRI** | Priority. |
| **S** | State, as follows: **O**, running; **R**, runnable (available in the run queue); **S**, sleeping; **T**, stopped or terminated; **Z**, zombie process (terminated without informing parent). (This column is displayed when you use the `-1` option.) |
| **STIME** | The time the process started. (This column is displayed when you use the `-f` option.) |
| **SZ** | Size of the process in virtual memory. (This column is displayed when you use the `-1` option.) |
| **TIME** | The time in minutes and seconds that the process has been running. |
| **TTY** | The name of the terminal device that controls the process. |
| **UID** | User ID number. |
| **WCHAN** | Wait. The address of an event that a sleeping process is waiting for in order to execute. (This column is displayed when you use the `-1` option.) |

> **TIP** Take a little time to examine the processes that run on your system, particularly those processes that are core system processes such as `init`, the scheduler, the logging system, the NIS cache, and so on. When you have a feeling for how many CPU cycles they consume normally, you can better understand what might be making your system malfunction when you see abnormal results.

As you can see in Figures 15.3 and 15.4, the *ps* command overwhelms you with information about running processes. As a system administrator, you typically want to know about the “top” processes running on a system (the processes that consume the most CPU time) that you are trying to diagnose. That’s what the *top* command is designed to do. The *top* command samples your system at specific intervals and returns the topmost 10 or 20 processes to the terminal windows, allowing you to monitor a system. You have control over the sampling period as well as the number of processes that are returned.

The top command is not a native Solaris command. To obtain this utility, download it from ftp://ftp.groupsy.com/pub/top. There are several different downloadable versions of the program at that site. Once you install top, you can call the top command from the command line.

The top command generates process statistics by reading the proc file system as a setuid process. You can run the program as root, but to allow other users and groups to run top, you need to reset the read and execute permissions. You may want to be careful about allowing nonprivileged users to run top because a setuid process allows users to make changes and presents a security risk. When compiling top for Solaris 8, make sure that the GNU gcc compiler is the right version or top will report incorrect results. Download the top program from ftp://SunSite.unc.edu/pub/solaris/sparc/ as a package called top^6 (recommended) and save yourself the trouble of compiling it.

## The truss Command

Another useful diagnostic command is the truss (trace a process) command. This command returns a list of the system calls executed by a program, the signals that that program receives from the system, and any faults that were encountered. Figure 15.5 shows the output of the truss data command. You might recall that the truss command returns the system date. Just this one very simple system command returns 43 lines from the truss command. Not all Unix systems support the truss command, but Solaris 8 does.

Here are a list of the most commonly used options that the truss command offers:

- **-a option** Reports all arguments passed to an exec() call after a fork.
- **-c option** Counts system calls, faults, and signals and outputs a summary report.
- **-e option** Shows all environmental variables that existed when exec() was called.
- **-f (fork) option** Traces all child processes.
- **-o `<outfile>` option** Outputs the results to an output file.
- **-r `<fd>` option** Shows the contents of buffers for read calls as file descriptor `<fd>`. Shows calls to other file descriptor and writes calls as `<fd>`.
- **-s [!<signal>] list option** The option -s displays signals from a comma-delimited list.
- **-t [!<call>] list option** The option -t displays system calls from a comma-delimited list.
- **-v option** Shows a verbose display.
- **-x [`<ca>`] `1`st option` The option `-x` displays data passed to the system calls as hexadecimal values in a comma-delimited list.
- **-w `<fd>` option** Shows the contents of buffers for write calls as file descriptor `<fd>`. Shows calls to other file descriptor and reads calls as `<fd>`.

### FIGURE 15.5

The output of the *truss* `date` command

![](img/256e02a6afce528d264a8d911fa0ff20_632_0.png)

When you know the PID number of the process you want to monitor, you can use the `truss -p <PidNumber>` command to follow the trace of the process and watch it run if you are a root user or the user who owns the program. If you want to monitor other people's processes, you will need root privileges. You can get the PID number from the `ps -ef` command. The `truss` command is particularly useful in tracking down client/server problems. If a process is hung, you can use the `truss` command on either the client or the server to see if the process is sleeping or has terminated.
