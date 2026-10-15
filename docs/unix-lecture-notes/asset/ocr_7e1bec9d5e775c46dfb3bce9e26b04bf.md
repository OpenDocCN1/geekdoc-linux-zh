+   - playing an audio track from a CD-ROM drive, and
+   - maintaining routing tables for a network.

The ioctl() function was designed to overcome these problems. It was first introduced in Version 7 AT&T UNIX as a general purpose I/O control program, to allow user level programs to access device drivers, hidden within the depths of the kernel. As time went on, more and more devices were handled through ioctl() calls. However, POSIX separated out the terminal control functions into the termios structure and functions, and for the most part, the ioctl() function is used today for accessing other devices. POSIX does not define ioctl(), but GNU includes the ioctl() function in its distribution of the C Standard Library.

The various device operations, known as IOCTLs, are assigned code numbers and multiplexed through the ioctl() function, which is defined in <sys/ioctl.h>. The code numbers themselves are defined in many different headers.

The ioctl() system call is given a file descriptor of a device file, and an IOCTL, which is an integer that represents a particular request that ioctl() should execute. If the request requires arguments, these are included after the command number. The man page begins as follows:

```
NAME
    ioctl - control device
SYNOPSIS
    #include <sys/ioctl.h>
    int ioctl(int fildes, int request, /* arg */ ...);
DESCRIPTION
    The ioctl() function manipulates the underlying device parameters of special files. In particular, many operating characteristics of character special files (e.g., terminals) may be controlled with ioctl() requests. The argument d must be an open file descriptor.

    The second argument is a device-dependent request code. The third argument is an untyped pointer to memory. ...
```

There are over 400 different request types, each defined by a different mnemonic code. The ioctl_list man page contains the list of valid request mnemonics that can be passed to ioctl() together with their argument types. Each device driver can define its own set of ioctl commands. The system, however, provides generic ioctl commands for different classes of devices. Generally speaking, the commands for the different classes have a prefix that identifies the type of command. For example, the magnetic tape commands are of the form MTIOxxx and can be found in <sys/mtio.h>, and the terminal I/O commands are of the form TIOxxx.

A simple example of an ioctl() is the call to retrieve the size of a terminal window. Terminal window sizes are defined by the winsize structure in the <ioctl-types.h> header file, which is included in <sys/ioctl.h>. The winsize structure looks like: