# SuSE System Administration
PART III

output. The device /dev/full produces a stream of zero bytes when read; /dev/null, on the other hand, produces no output at all.

# Memory Devices

The memory devices have the same device number as /dev/null and /dev/full are used differently. They are as follows:

+   * /dev/mem Provides access to physical memory
* /dev/kmem Provides access to the kernel's virtual memory
* /dev/port Provides access to I/O ports

These devices are not frequently used in many programs; the X Window system's X server uses memory mapping on /dev/mem the video memory, and many programs use /dev/port to access I/O ports on those architectures that have a separate I/O space. (Many modern processors do not.)

# Virtual Console Screen Devices

The virtual console devices exist to provide screen capture capabilities for virtual consoles (VCs). They are not readable by ordinary users; hence, other users cannot eavesdrop on your session.

There are two sets of device nodes for this purpose:

```
$ ls -1 /dev/vcs[012] /dev/vcsa[012]
crw-rw---- 1 root tty 7, 0 Jul 22 19:04 /dev/vcs0
crw-rw---- 1 root tty 7, 1 Jul 22 19:04 /dev/vcs1
crw-rw---- 1 root tty 7, 2 Jul 22 19:04 /dev/vcs2
crw-rw---- 1 root tty 7, 128 Jul 22 19:04 /dev/vcsa0
crw-rw---- 1 root tty 7, 129 Jul 22 19:04 /dev/vcsa1
crw-rw---- 1 root tty 7, 130 Jul 22 19:04 /dev/vcsa2
```

Each set is numbered from 0 to 63, considering the numbering system for the /dev/tty* console device. The /dev/vcs device, like the /dev/tty device, always refers to the currently selected VC.

The /dev/vcs* files provide a snapshot of what is in on the corresponding VC. This snapshot contains no newlines because there are none actually on the screen; after all, a newline character just moves the cursor. To make the captured data into the kind of thing you usually see in text files or send to printers, you need to add newlines in the appropriate places. This can be done with dd:

```
$ dd bs=80 conv=unblock < /dev/vcs1 ; lpr
```