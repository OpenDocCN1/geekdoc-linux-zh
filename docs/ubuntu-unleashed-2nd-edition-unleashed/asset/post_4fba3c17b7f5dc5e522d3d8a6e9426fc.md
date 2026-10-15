
```
real 1.20
user 0.14
sys 0.71
```

Output of the command displays the time from start to finish, along with the user and system time required. Other factors you can query include memory, CPU usage, and file system input/output (I/O) statistics. See the time command's man page for more details.

Nearly all graphical process-monitoring tools include some form of process control or management. Many of the early tools ported to Linux were clones of legacy UNIX utilities. One familiar monitoring (and control) program is top. Based on the ps command, the top command provides a text-based display of constantly updated console-based output showing the most CPU-intensive processes currently running. It can be started like this:

```
$ sudo top
```

After you press Enter, you will see a display as shown in Figure 16.1. The top command has a few interactive commands: pressing h displays the help screen; pressing k prompts you to enter the PID of a process to kill; pressing n prompts you to enter the PID of a process to change its nice value. The top man page describes other commands and includes a detailed description of what all the columns of information top can display actually represent; have a look at top's well-written man page.

![](img/e464b828c497c99e41f61d4c55f1c0db_382_0.png)

FIGURE 16.1 You can use the top command to monitor and control processes. Here, we are prompted to renice a process.

The top command displays quite a bit of information about your system. Processes can be sorted by PID, age, CPU or memory usage, time, or user. This command also provides process management, and system administrators can use its k and r keypress commands to kill and reschedule running tasks, respectively.

The top command uses a fair amount of memory, so you might want to be judicious in its use and not leave it running all the time. When you've finished with it, simply press q to quit top.

## Displaying Free and Used Memory with free

Although top includes some memory information, the free utility displays the amount of free and used memory in the system in kilobytes. (The -m switch displays in megabytes.) On one system, the output looks like this:

```
$ sudo free
      total      used      free      shared     buffers     cached
Mem:       516372    484972     31400         0       19816     317420
-/+ buffers/cache:   147736    368636
Swap:      433712        0     433712
```

This output describes a machine with 512MB of RAM memory and a swap partition of 444MB. Note that some swap is being used although the machine is not heavily loaded. Linux is good at memory management and “grabs” all the memory it can in anticipation of future work.

## TIP

A useful trick is to employ the watch command; it repeatedly reruns a command every 2 seconds by default. If you use

```
$ sudo watch free
```

you will see the output of the free command updated every 2 seconds.

Another useful system-monitoring tool is vmstat (virtual memory statistics). This command reports on processes, memory, I/O, and CPU, typically providing an average since the last reboot; or you can make it report usage for a current period of time by telling it the time interval in seconds and the number of iterations you desire, as follows:

```
$ sudo vmstat 5 10
```

The preceding command runs vmstat every 5 seconds for 10 iterations.

Use the uptime command to see how long it has been since the last reboot and to get an idea of what the load average has been; higher numbers mean higher loads.

## Disk Quotas

Disk quotas are a way to restrict the usage of disk space either by user or by groups. Although rarely—if ever—used on a local or standalone workstation, quotas are definitely a way of life at the enterprise level of computing. Usage limits on disk space not only conserve resources, but also provide a measure of operational safety by limiting the amount of disk space any user can consume.

Disk quotas are more fully covered in Chapter 14, “Managing Users.”

## Graphical Process and System Management Tools

The GNOME and KDE desktop environments offer a rich set of network and system-monitoring tools. Graphical interface elements, such as menus and buttons, and graphical output, including metering and real-time load charts, make these tools easy to use. These clients, which require an active X session and (in some cases) root permission, are included with Ubuntu.

If you view the graphical tools locally while they are being run on a server, you must have X properly installed and configured on your local machine. Although some tools can be used to remotely monitor systems or locally mounted remote file systems, you have to properly configure pertinent X11 environment variables, such as $DISPLAY, to use the software or use the ssh client’s -X option when connecting to the remote host.

A handy little application is the xosview client, which provides load, CPU, memory and swap usage, disk I/O usage and activity, page swapping information, network activity, I/O activity, I/O rates, serial port status, and if APM is enabled, the battery level (such as for a laptop). You will have to obtain xosview using either synaptic or apt-get.

For example, to see most of these options, start the client like this:

```
$ sudo xosview -geometry 406x488 -font 8x16 +load +cpu +mem +swap \
+page +disk +int +net &
```

After you press Enter, you will see a display as shown in Figure 16.2.

The display can be customized for a variety of hardware and information, and the xosview client (like most well-behaved X clients) obeys geometry settings such as size, placement, or font. If you have similar monitoring requirements, and want to try a similar but different client from xosview, try xcpustate, which has features that enable it to monitor network CPU statistics foreign to Linux. Neither of these applications is installed with the base set of packages; you have to install them manually if you want to use them.

Some of the graphical system- and process-monitoring tools included with Ubuntu are as follows:

- vncviewer—AT&T’s open-source remote session manager (part of the xvnc package), which can be used to view and run a remote desktop session locally. This software (discussed in more detail in Chapter 19, “Remote Access with SSH and Telnet”) requires an active, but background, X session on the remote computer.
