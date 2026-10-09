The top(1) tool displays a PRI column for process priority. FreeBSD calculates a process's priority from a variety of factors, including niceness, and runs high-priority processes first whenever possible. Niceness affects priority, but you can't directly edit priority.

If you know that your system is running at or near capacity, you can choose to run a command with nice(1) to assign the process a niceness. Specify niceness with `nice -n` and the nice value in front of the command. For example, to start a very selfish `make buildworld` at nice 15, you'd run:

```
# nice -n 15 make buildworld
```

Only root can assign a negative niceness to a program, as in `nice -n -5`. For example, if you want to abuse your superuser privileges to make a compile finish as quickly as possible, use a negative niceness:

```
# nice -n -20 make
```

![](bbox=[0.14, 0.52, 0.86, 0.71])

Usually, you don't have the luxury of telling a command to be nice when you start it but instead have to change its niceness when you learn that it's absorbing all of your system capacity. You can use renice(8) to reprioritize running processes by their process IDs or owners. To change the niceness of a process, run renice with the new niceness and the PID as arguments.

In my career, I've run several logging hosts. In addition to general syslog services, they usually also run several instances of flow-capture,