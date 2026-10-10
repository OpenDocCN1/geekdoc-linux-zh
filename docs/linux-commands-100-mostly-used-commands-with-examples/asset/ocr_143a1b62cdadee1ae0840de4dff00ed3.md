This command displays the timestamp along with various statistics, including kernal threads.

# 95. ss: Display socket statistics.

The `ss` command in Linux is a powerful tool for displaying socket statistics. It provides detailed information about network sockets on a system, including their state, type, and other relevant details. The `ss` command is part of the iproute2 package and is often used as a replacement for the older `netstat` command.

**Examples:**

+   1. **Display all Sockets:**

```
```
ss
```
```

This command displays a list of all sockets on the system.

+   2. **Display Listening Sockets:**

```
```
ss -l
```
```

This shows all listening sockets.

+   3. **Display Established Connections:**