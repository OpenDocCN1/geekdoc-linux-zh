
Many system administrators like the BSD-style l parameter because it produces a more detailed state code for processes (the STAT column). The multicharacter code defines exactly what’s happening with the process more precisely than the single-character Unix-style output.

The first character uses the same values as the Unix-style s output column, showing when a process is sleeping, running, or waiting. The following characters further define the process’s status:

-   `<`: The process is running at high priority.
-   `N`: The process is running at low priority.
-   `L`: The process has pages locked in memory.
-   `s`: The process is a session leader.
-   `l`: The process is multithreaded.
-   `+`: The process is running in the foreground.

From the simple example shown previously, you can see that the `bash` command is sleeping, but it is a session leader (it’s the main process in my session), whereas the `ps` command is running in the foreground on the system.

## The GNU long parameters

Finally, the GNU developers put their own touches on the new, improved `ps` command by adding a few more options to the parameter mix. Some of the GNU long parameters copy existing Unix- or BSD-style parameters, whereas others provide new features. Table 4-3 lists the available GNU long parameters.

**TABLE 4-3** The `ps` Command GNU Parameters

| Parameter | Description |
| :--- | :--- |
| `--deselect` | Show all processes except those listed in the command line. |
| `--Group grp-list` | Show processes whose group ID is listed in `grp-list`. |
| `--User user-list` | Show processes whose user ID is listed in `user-list`. |
| `--group grpulist` | Show processes whose effective group ID is listed in `grpulist`. |
| `--pid pidlist` | Show processes whose process ID is listed in `pidlist`. |
| `--ppid pidlist` | Show processes whose parent process ID is listed in `pidlist`. |
| `--sid sidlist` | Show processes whose session ID is listed in `sidlist`. |
| `--tty ttylist` | Show processes whose terminal device ID is listed in `ttylist`. |
| `--user userlist` | Show processes whose effective user ID is listed in `userlist`. |
| `--format format` | Display only columns specified in the `format`. |
| `--context` | Display additional security information. |
| `--cols n` | Set screen width to n columns. |
| `--columns n` | Set screen width to n columns. |
| `--cumulative` | Include stopped child process information. |
| `--forest` | Display processes in a hierarchical listing showing parent processes. |
| `--headers` | Repeat column headers on each page of output. |
| `--no-headers` | Don't display column headers. |
| `--lines n` | Set the screen height to n lines. |
| `--rows n` | Set the screen height to n rows. |
| `--sort order` | Define the column(s) to use for sorting the output. |
| `--width n` | Set the screen width to n columns. |
| `--help` | Display the help information. |
| `--info` | Display debugging information. |
| `--version` | Display the version of the `ps` program. |

You can combine GNU long parameters with either Unix- or BSD-style parameters to customize your display. One cool feature of GNU long parameters that we really like is the `--forest` parameter. It displays the hierarchical process information but uses ASCII characters to draw cute charts:

```
1981 ? 00:00:00 sshd
3078 ? 00:00:00 \ sshd
3080 ? 00:00:00 \ sshd
3081 pts/0 00:00:00 \ bash
16676 pts/0 00:00:00 \ ps
```

This format makes tracing child and parent processes a snap!

## Real-time process monitoring

The `ps` command is great for gleaning information about processes running on the system, but it has one drawback. The `ps` command can display information for only a specific point in time. If you're trying to find trends about processes that are frequently swapped in and out of memory, it's hard to do that with the `ps` command.

Instead, the `top` command can solve this problem. The `top` command displays process information similarly to the `ps` command, but it does so in real-time mode. Figure 4-1 is a snapshot of the `top` command in action.

![](img/a5025f22e05b92f409563a958cac7312_147_0.png)

**FIGURE 4-1** The output of the top command while it is running

The first section of the output shows general system information. The first line shows the current time, how long the system has been up, the number of users logged in, and the load average on the system.

The load average appears as three numbers, the 1-minute, 5-minute, and 15-minute load averages. The higher the values, the more load the system is experiencing. It's not uncommon for the 1-minute load value to be high for short bursts of activity. If the 15-minute load value is high, your system may be in trouble.

### NOTE

The trick in Linux system administration is defining what exactly a high load average value is. This value depends on what's normally running on your system and the hardware configuration. What's high for one system might be normal for another. The best practice is to note the load levels of your system under normal conditions, which will make it easier to detect when your system is under load.

The second line shows general process information (called tasks in top): how many processes are running, sleeping, stopped, and zombie (have finished but their parent process hasn't responded).

The next line shows general CPU information. The top display breaks down the CPU utilization into several categories depending on the owner of the process (user versus system processes) and the state of the processes (running, idle, or waiting).

Following that, there are two lines that detail the status of the system memory. The first line shows the status of the physical memory in the system, how much total memory there is, how much is currently being used, and how much is free. The second memory line shows the status of the swap memory area in the system (if any is installed), with the same information.

Finally, the next section shows a detailed list of the currently running processes, with some information columns that should look familiar from the ps command output:

-   **PID:** The process ID of the process
-   **USER:** The username of the owner of the process
-   **PR:** The priority of the process
-   **NI:** The nice value of the process
-   **VIRT:** The total amount of virtual memory used by the process
-   **RES:** The amount of physical memory the process is using
-   **SHR:** The amount of memory the process is sharing with other processes
-   **S:** The process status (D = interruptible sleep, R = running, S = sleeping, T = traced or stopped, or Z = zombie)
-   **%CPU:** The share of CPU time that the process is using
-   **%MEM:** The share of available physical memory the process is using
-   **TIME+:** The total CPU time the process has used since starting
-   **COMMAND:** The command-line name of the process (program started)

By default, when you start `top` it sorts the processes based on the %CPU value. You can change the sort order by using one of several interactive commands while `top` is running. Each interactive command is a single character you can press while `top` is running that changes the behavior of the program. Pressing `f` allows you to select the field to use to sort the output, and pressing `d` allows you to change the polling interval. Press `q` to exit the top display. You have lots of control over the output of the top command. Using this tool, you can often find offending processes that have taken over your system. Of course, once you find one, the next job is to stop it, which brings us to the next topic.

## Stopping processes

A crucial part of being a system administrator is knowing when and how to stop a process. Sometimes a process gets hung up and just needs a gentle nudge to either get going again or stop. Other times, a process runs away with the CPU and refuses to give it up. In both cases, you need a command that will allow you to control a process. Linux follows the Unix method of interprocess communication.

In Linux, processes communicate with each other using *signals*. A process signal is a predefined message that processes recognize and may choose to ignore or act on. The developers program how a process handles signals. Most well-written applications have the ability to receive and act on the standard Unix process signals. These signals are shown in Table 4-4.

**TABLE 4-4 Linux Process Signals**

| Signal | Name | Description |
| :--- | :--- | :--- |
| 1 | HUP | Hang up. |
