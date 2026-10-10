```
```
joe:~$ who
jenny  tty1      Jan 23 11:41
jenny  pts/1     Jan 23 12:21 (:0)
jenny  pts/2     Jan 23 12:22 (:0)
jenny  pts/3     Jan 23 12:22 (:0)
joe    pts/0     Jan 20 10:13 (10.callohost.org)

joe:~$ ls -l /dev/tty1
crw-w---    1 jenny   tty  4,    1 Jan 23 11:41 /dev/tty1
```
```

```
```
joe:~$ write jenny tty1
hey Jenny, shall we have lunch together?
^C
```
```

*User jenny gets this on her screen:*

```
```
Message from joe@10.callohost.org on ptys/1 at 12:36 ...
hey Jenny, shall we have lunch together?
EOF
```
```

After receiving a message, the terminal can be cleared using the Ctrl+L key combination. In order to receive no messages at all (except from the system administrator), use the mesg command. To see which connected users accept messages from others use who -w. All features are fully explained in the Info pages of each command.

# Group names may vary

The group scheme is specific to the distribution. Other distributions may use other names or other solutions.

# 4.2  Boot process, Init and shutdown

# 4.2.1  Introduction

One of the most powerful aspects of Linux concerns its open method of starting and stopping the operating system, where it loads specified programs using their particular configurations, permits you to change those configurations to control the boot process, and shuts down in a graceful and organized way.

Beyond the question of controlling the boot or shutdown process, the open nature of Linux makes it much easier to determine the exact source of most problems associated with starting up or shutting down your system. A basic understanding of this process is quite beneficial to everybody who uses a Linux system.

A lot of Linux systems use lilo, the Linux Loader for booting operating systems. We will only discuss GRUB, however, which is easier to use and more flexible. Should