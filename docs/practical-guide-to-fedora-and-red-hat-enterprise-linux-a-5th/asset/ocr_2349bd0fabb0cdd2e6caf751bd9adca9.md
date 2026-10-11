penalty associated with this change is minimal. The benefit of the move is that a bug in udev cannot compromise or crash the kernel.

The udev utility is part of the hotplug system (discussed next). When a device is added to or removed from the system, the kernel creates a device name in the /sys pseudofilesystem and notifies hotplug of the event, which is received by udev. The udev utility then creates the device file, usually in the /dev directory, or removes the device file from the system. The udev utility can also rename network interfaces. See docs.fedoraproject.org/udev and www.kernel.org/pub/linux/utils/kernel/hotplug/udev.html for more information.

The hotplug system allows you to plug a device into the system and use it immediately. Although hotplug was available in the Linux 2.4 kernel, the 2.6 kernel integrates hotplug with the unified device driver framework (the driver model core) so that any bus can report an event when a device is added to or removed from the system. User software can be notified of the event so it can take appropriate action. See linux-hotplug.sourceforge.net for more information about hotplug.

# FIFO SPECIAL FILE (NAMED PIPE)

A FIFO special file, also called a named pipe, represents a pipe: You read from and write to the file to read from and write to the pipe. The term FIFO stands for first in, first out—the way any pipe works. In other words, the first information that you put in one end is the first information that comes out the other end. When you use a pipe on a command line to send the output of a program to the printer, the printer outputs the information in the same order that the program produced it and sent it to the pipe.

Unless you are writing sophisticated programs, you will not be working with FIFO special files. However, programs that you use on Linux use named pipes for inter-process communication. You can create a pipe using mkfifo:

```
$ mkfifo AA
$ ls -l AA
prw-rw-r-- 1 zach zach 0 Apr 26 13:11 AA
```

The p at the left end of the output of ls -l indicates that the file is a pipe.

The UNIX and Linux systems have included pipes for many generations. Without named pipes, only processes that were children of the same ancestor could use pipes to exchange information. Using named pipes, any two processes on a single system can exchange information. When one program writes to a FIFO special file, another program can read from the same file. The programs do not have to run at the same time or be aware of each other's activity. The operating system handles all buffering and information storage. This type of communication is termed asynchronous (async) because programs on the ends of the pipe do not have to be synchronized.

# SOCKETS

Like a FIFO special file, a socket allows asynchronous processes that are not children of the same ancestor to exchange information. Sockets are the central mechanism of