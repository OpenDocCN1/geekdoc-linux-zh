# Chapter 5 Controlling Processes

The pgrep and pkill commands for Solaris, HP-UX, and Linux (but AIX) search for processes by name (or other attributes, such as EUID) and display or signal, respectively. For example, the following command sends a TERM signal to all processes as the user ben:

```
$ pkill -u ben
```

# 5.5 PROCESS STATES

A process is not automatically eligible to receive CPU time just because it exists. You need to be aware of the four execution states listed in Table 5.2.

# Table 5.2 Process states

| State | Meaning |
| --- | --- |
| Runnable | The process can be executed. |
| Sleeping | The process is waiting for some resource. |
| Zombie | The process is trying to die. |
| Stopped | The process is suspended (not allowed to execute). |

A runnable process is ready to execute whenever CPU time is available. It has acquired all the resources it needs and is waiting for CPU time to process its data. As as the process makes a call that cannot be immediately completed (such as a request to read a file), the kernel puts it to sleep.

Sleeping processes are waiting for a specific event to occur. Interactive shells and system daemons spend most of their time sleeping, waiting for terminal input or network connections. Since a sleeping process is effectively blocked until its request has been satisfied, it will get no CPU time unless it receives a signal or response to one of its I/O requests.

Some operations process to enter an uninterruptible state. This state is usually transient and not observed in ps output (indicated by a D in the STAT column; see Table 5.4 on page 132). However, a few situations can cause it to persist. The most common involves server problems on a filesystem mounted with the "hard" option. Since processes in the uninterruptible sleep state cannot be roused to service a signal, they cannot be killed. To get rid of them, you must fix the underlying process or reboot.

Zombies are processes that have finished execution but have not yet had their status collected. If you see zombies around, check their PPIDs with ps to find out where they are coming from.

Stopped processes are administratively forbidden to run. Processes are stopped on receipt of a STOP or TP signal and are restarted with CONT. Being stopped is similar to sleeping, but there's no way for a process to get out of the stopped state than having some other process wake it up (or kill it).