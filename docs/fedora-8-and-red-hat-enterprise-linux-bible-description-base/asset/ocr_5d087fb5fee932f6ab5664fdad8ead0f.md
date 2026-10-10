> **CAUTION:** By default, the floppy-disk drive can be read from or written to only by the root user and the floppy group. To make the floppy drive accessible to everyone (assuming it is floppy drive A:), type the following as root user: `chmod 666 /dev/fd0`.

# Using DOSBox

To run your classic DOS applications, Fedora includes the dosbox package. To install dosbox, type the following as root user:

```
# yum install dosbox
```

With DOSBox installed, just type **dosbox** to open a DOSBox window on your desktop. From that window, you have an environment when you can run many classic DOS applications. Assuming you have some DOS applications you want to run already stored on your Fedora system, you can make those applications available by mounting the directory containing them. For example, to mount the `/home/chris` directory to drive C in DOSBox, type the following:

```
Z:> mount c /home/chris
```

At this point, you can use standard DOS commands to access and run applications from the directory you just mounted. For example, type **dir c:** to see the contents of the directory you just mounted. Type **c:** to go to that directory. Then just run the DOS applications stored in that directory by typing its name.

To mount a CD-ROM, you need to indicate the file system type when you mount it. For example:

```
Z:> mount d /media/disk -t cdr
```

For information on using special keys and features in dosbox, refer to the dosbox README file (`/usr/share/doc/dosbox-*/README`).

# Running Microsoft Windows applications in Linux

There are several promising approaches you can take to get your Windows applications to work during a running Linux session. Here are a few of them:

+   • **WINE** — The WINE project (www.winehq.org) has been making great strides in getting applications that were created for Microsoft Windows to run in Linux and other operating systems. WINE is not really an emulator because it doesn't emulate the entire Windows operating system. Instead, because it implements Win32 application programming interfaces (APIs) and Windows 3.x interfaces, the WINE project is more of a “Windows compatibility layer.” WINE doesn't require that Windows be installed. It can, however, take advantage of Windows dll files if you have some to add.
+   
+   • **Win4Lin** — Win4Lin (www.win4lin.com) is a commercial product for running a Windows system in Linux. You can try the software free for 14 days. Installation