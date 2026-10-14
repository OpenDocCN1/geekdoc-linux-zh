
Let's try out the kill command:

```
[me@linuxbox ~]$ xlogo &
[1] 13546
[me@linuxbox ~]$ kill -1 13546
[1]+  Hangup                  xlogo
```

In this example, we start the xlogo program in the background and then send it a HUP signal with kill. The xlogo program terminates and the shell indicates that the background process has received a hangup signal. You may need to press the enter key a couple of times before you see the message. Note that signals may be specified either by number or by name, including the name prefixed with the letters “SIG”:

```
[me@linuxbox ~]$ xlogo &
[1] 13601
[me@linuxbox ~]$ kill -INT 13601
[1]+  Interrupt                xlogo
[me@linuxbox ~]$ xlogo &
[1] 13608
[me@linuxbox ~]$ kill -SIGINT 13608
[1]+  Interrupt                xlogo
```

Repeat the example above and try out the other signals. Remember, you can also use jobspecs in place of PIDs.

Processes, like files, have owners, and you must be the owner of a process (or the superuser) in order to send it signals with kill.

In addition to the list of signals above, which are most often used with kill, there are other signals frequently used by the system. Here is a list of other common signals:

### Table 10-5: Other Common Signals

| Number | Name | Meaning |
|---|---|---|
| 3 | QUIT | Quit. |
| 11 | SEGV | Segmentation Violation. This signal is sent if a program makes illegal use of memory, that is, it tried to write somewhere it was not allowed to. |
| 20 | TSTP | Terminal Stop. This is the signal sent by the terminal when the Ctrl-z key is pressed. Unlike the STOP signal, the TSTP signal is received by the program but the program may choose to ignore it. |
| 28 | WINCH | Window Change. This is a signal sent by the system when a window changes size. Some programs, like top and less will respond to this signal by redrawing themselves to fit the new window dimensions. |

For the curious, a complete list of signals can be seen with the following command:

```
[me@linuxbox ~]$ kill -l
```

## Sending Signals To Multiple Processes With killall

It's also possible to send signals to multiple processes matching a specified program or username by using the killall command. Here is the syntax:

```
killall [-u user] [-signal] name...
```

To demonstrate, we will start a couple of instances of the xlogo program and then terminate them:

```
[me@linuxbox ~]$ xlogo &
[1] 18801
[me@linuxbox ~]$ xlogo &
[2] 18802
[me@linuxbox ~]$ killall xlogo
[1]- Terminated              xlogo
[2]+ Terminated              xlogo
```

Remember, as with kill, you must have superuser privileges to send signals to processes that do not belong to you.

## More Process Related Commands

Since monitoring processes is an important system administration task, there are a lot of commands for it. Here are some to play with:

### Table 10-6: Other Process Related Commands

| Command | Description |
|---|---|
| pstree | Outputs a process list arranged in a tree-like pattern showing the parent/child relationships between processes. |
| vmstat | Outputs a snapshot of system resource usage including, memory, swap and disk I/O. To see a continuous display, follow the command with a time delay (in seconds) for updates. For example: vmstat 5. Terminate the output with Ctrl-c. |
| xload | A graphical program that draws a graph showing system load over time. |
| tload | Similar to the xload program, but draws the graph in the terminal. Terminate the output with Ctrl-c. |

## Summing Up

Most modern systems feature a mechanism for managing multiple processes. Linux provides a rich set of tools for this purpose. Given that Linux is the world's most deployed server operating system, this makes a lot of sense. However, unlike some other systems, Linux relies primarily on command line tools for process management. Though there are graphical process tools for Linux, the command line tools are greatly preferred because of their speed and light footprint. While the GUI tools may look pretty, they often create a lot of system load themselves, which somewhat defeats the purpose.
