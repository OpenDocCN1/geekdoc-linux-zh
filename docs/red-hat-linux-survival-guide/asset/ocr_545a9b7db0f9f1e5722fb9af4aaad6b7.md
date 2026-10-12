# Finding the PID of a process’s parent

To find the PID of a process’s parent, you can run the following command, where PID is the process ID:

```
ps l PID
```

For example, if you want to find the parent of a process with PID 123, you can run the ps l 123 command. The parent’s PID will be listed in the PPID field of the report.

# Displaying environment information

Knowing a program’s environment information is often a great way to determine bugs and also configuration problems. To determine what initial environment variables are available to processes, you can run the following command, which appends the environment information to the COMMAND field of the resulting ps report:

```
ps e
```

![](bbox=[0.08, 0.75, 0.16, 0.83])

A regular (non-superuser or root) user cannot use the -e option to see the environment information of another user's processes. This is a security feature. Only root or other superusers can view environment information of all the processes.

# Monitoring a process over time

At times you find that you need to run ps to monitor a specific process for a certain amount of time. For example, say that you installed a new sendmail mail server patch and want to make sure the server is up and running and determine whether it is using an excessive amount of system resources. In such a case you can combine a few Linux commands as follows:

```
watch --interval=n "ps auxw | grep process_you_want_to_monitor"
```

For example, you can run watch --interval=30 "ps auxw | grep sendmail" to see how much resource sendmail is using by running the ps program every 30 seconds.