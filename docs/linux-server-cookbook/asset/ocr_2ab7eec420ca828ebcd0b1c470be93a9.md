```
root@ubuntu:~/examples# history
    1  mkdir examples
    2  cd examples/
    3  mkdir -v example1
    4  /usr/bin/mkdir -v example2
    5  ../../usr/bin/mkdir -v /root/examples/example3
    6  ls
    7  ls -l
    8  ls -l --all
    9  pwd
```

![](bbox=[0.31, 0.33, 0.69, 0.36])

It is possible to repeat the last command writing to exclamation (\u00a1\u00a1) or repeat a specific command using exclamation and the number from the history output (for example !9 to run the command pwd from the output of figure 3.10)

# Command uptime

This simple tool shows valuable information about the current time, how long the system has been running, how many users are currently logged on, and the system load average for the last minute, 5 minutes, and 15 minutes. This command does not accept any argument, and the useful option is -p(-pretty) to show only the uptime information. The following figure shows the output example:

```
root@ubuntu:~# uptime
    20:16:03 up  4:36,   5 users,  load average: 0.00, 0.00, 0.00
root@ubuntu:~# uptime -p
up 4 hours, 36 minutes
```

![](bbox=[0.31, 0.76, 0.69, 0.79])

# CLI commands to identify resources

Linux distributions include some system commands to identify system resources. These utilities are usually available after the installation and do not require any package installation to run the following commands. These