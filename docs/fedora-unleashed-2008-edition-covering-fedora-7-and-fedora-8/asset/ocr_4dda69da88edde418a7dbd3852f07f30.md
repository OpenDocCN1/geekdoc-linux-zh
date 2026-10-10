often pipe the output of `ps` through a member of the `grep` family of commands to display information about a specific program, perhaps like this:

```
```
$ ps aux | grep system-config-display
root 4286 0.0 0.3 13056 3172 pts/0 S 11:57 0:00 system-config-
→display
```
```

This example returns the owner (the user who launched the program) and the PID, along with other information, such as the percentage of CPU and memory use, size of the command (code, data, and stack), time (or date) the command was launched, and name of the command. Processes can also be queried by PID, as follows:

```
```
$ ps 4286
4286 pts/0 S 0:00 system-config-display
```
```

You can use the PID to stop a running process by using the shell’s built-in `kill` command. This command asks the kernel to stop a running process and reclaim system memory. For example, to stop the `system-config-display` client in the example, use the `kill` command like this:

```
```
$ kill 4286
```
```

After you press Enter (or perhaps press Enter again), the shell might report the following:

```
```
[1]+ Terminated system-config-display
```
```

Note that users can kill only their own processes, but root can kill them all. Controlling any other running process requires root permission, which should be used judiciously (especially when forcing a kill (by using the -9 option); by inadvertently killing the wrong process through a typo in the command, you could bring down an active system.

# ## Using the kill Command to Control Processes

The `kill` command is a basic UNIX system command. You can communicate with a running process by entering a command into its interface, such as when you type into a text editor. But some processes (usually system processes rather than application processes) run without such an interface, so you need a way to communicate with them, too, so we use a system of signals. The `kill` system accomplishes that by sending a signal to a process, and you can use it to communicate with any process. The general format of the `kill` command is as follows:

```
```
# kill option PID
```
```

A number of signal options can be sent as words or numbers, but most are of interest only to programmers. One of the most common is this:

```
```
# kill PID
```
```