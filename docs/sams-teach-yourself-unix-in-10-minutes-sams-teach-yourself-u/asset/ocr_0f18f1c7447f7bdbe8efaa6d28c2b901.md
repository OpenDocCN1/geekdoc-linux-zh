![](bbox=[0.12, 0.18, 0.18, 0.24])

> nice The nice command is yet another example of slight variations between different commands with the same name. Some versions of nice use -n <priority> instead of <priority>.

For example

```
>nice -20 analog /var/log/httpd/access_log &
```

This puts the analog command into the background and assigns it a priority level of 20. Remember, this is the lowest level priority that a process can have!

![](bbox=[0.12, 0.58, 0.18, 0.64])

> Changing Priorities Normal users can't set priorities below 0—only the root user can do this. You can think of it as follows: running the program without nice is as high priority as you can get, and you can use the nice command to make it nicer to other users.

# USING renice

Suppose, however, that you've started a command with default priority that has been running for a day—for example, analyzing that big Web server log—and you have no idea when it's going to finish. You figure you might as well lower the priority, and therefore its use of machine resources, and allow it to finish whenever it decides to. You can use renice to change the priority of a command that is already running.

To do this, follow these steps:

+   1. First, you'll need to get a listing of your processes and make a note of the PID that you want to change.
+   2. Issue the renice command using this syntax: renice <priority> <process ID>.