For example

```
>ps
PID TTY STAT TIME COMMAND
8832 p1 R 0:00 ps
30674 p1 S 0:00 /bin/login -h
=>NEW93114217.columbus.here.com -p
30675 p1 S 0:00 -bash
31136 p1 R 0:00 analog /var/log/httpd/access_log
```

If you want to change analog PID 31136 so that it is running with a lower priority, you can use the renice command in the following manner:

```
>renice +15 31136
31136: old priority 0, new priority 15
```

PID 31136 is now running with the priority 15, as opposed to the original priority 0.

> Super User Power It is important to note that only the super user (root) has the capability to raise the priority of a running process. You can only lower the priority of a process--so don't lower a priority thinking you can raise it if it runs too slowly. After it's lowered, it's stuck there unless your system administrator fixes it for you.

# CHECKING THE PROCESSES ON YOUR COMPUTER: top

Viewing the busy processes on your system is as simple as running the top command. top displays a continually updated list of processes, the amount of time they are using, and the process priority. To exit out of top press the UNIX break-sequence Ctrl+c.