# **57. w: Show who is logged in and what they are doing.**

The `w` command in Linux is used to display information about the users currently logged in and their activities. It provides a quick overview of who is logged in, what they are doing, and how long they have been idle.

**Examples:**

+   1. **Display Information about Currently Logged-In Users:**

```
```
w
```
```

This command will display information about the users currently logged in, including their username, terminal, remote host (if applicable), login time, idle time, JCPU (total CPU time used by all processes attached to the terminal), PCPU (the CPU time used by the current process), and the command being executed.

+   2. **Display Information with Header:**

```
```
w -h
```
```

Adding the `-h` option suppresses the header line, providing a more compact display of user information.

+   3. **Display Information for a Specific User:**

```
```
w username
```
```