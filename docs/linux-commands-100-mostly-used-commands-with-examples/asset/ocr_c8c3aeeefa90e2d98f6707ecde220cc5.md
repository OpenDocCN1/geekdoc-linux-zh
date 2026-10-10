```
ss -t -i
```

Show extended socket information.

# 11. Display Timers:

```
ss -o
```

Display socket timers.

# 12. Display More Information:

```
ss -t -i -o -e
```

Display detailed information about TCP sockets.

# 96. renice: Alter priority of running processes.

The `renice` command in Linux is used to alter the scheduling priority of running processes. This command allows you to change the nice value of a process, which determines its priority in the system scheduler. The nice value ranges from -20 to 19, with lower values indicating higher priority.