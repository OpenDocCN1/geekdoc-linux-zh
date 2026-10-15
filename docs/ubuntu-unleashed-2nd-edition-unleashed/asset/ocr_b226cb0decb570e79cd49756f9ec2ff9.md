The top command displays quite a bit of information about your system. Processes can be sorted by PID, age, CPU or memory usage, time, or user. This command also provides process management, and system administrators can use its k and r keypress commands to kill and reschedule running tasks, respectively.

The top command uses a fair amount of memory, so you might want to be judicious in its use and not leave it running all the time. When you've finished with it, simply press q to quit top.

# Displaying Free and Used Memory with free

Although top includes some memory information, the free utility displays the amount of free and used memory in the system in kilobytes. (The -m switch displays in megabytes.) On one system, the output looks like this:

```
$ sudo free
      total      used      free      shared     buffers     cached
Mem:       516372    484972     31400         0       19816     317420
-/+ buffers/cache:   147736    368636
Swap:      433712        0     433712
```

This output describes a machine with 512MB of RAM memory and a swap partition of 444MB. Note that some swap is being used although the machine is not heavily loaded. Linux is good at memory management and “grabs” all the memory it can in anticipation of future work.

# TIP

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