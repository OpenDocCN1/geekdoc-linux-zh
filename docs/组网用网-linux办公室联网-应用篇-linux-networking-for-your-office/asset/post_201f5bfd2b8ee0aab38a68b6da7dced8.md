
## Checking Your Device File

Linux uses device files to connect to hardware devices such as serial ports, parallel ports, hard disks, and so on. These files typically appear in the /dev directory. Serial ports use the /dev/ttySx names, where x is a number 0 or higher. What you know as COM1: under DOS or Windows is /dev/ttyS0 under Linux, and COM2: in DOS is /dev/ttyS1 in Linux. In addition, many systems create a hard or symbolic link between the device that holds your modem and the file /dev/modem. This allows you to use the more mnemonic /dev/modem when configuring PPP networking or other tasks that use the modem. Throughout this chapter, I use /dev/modem as a reference to your modem device.

### Note

> In earlier incarnations of Linux, /dev/cuax was an alternative method of addressing serial ports, and you might run into scripts or documentation that refers to this series of device files. As of kernel 2.2.0, however, /dev/cuax shouldn’t be used; though it may still work now, it likely won’t for many more kernel revisions.

To check that your serial port devices exist, type the following command at an xterm or command prompt:

```
ls -l /dev/ttyS? /dev/modem
```

You should see output similar to this:

```
crw------ 2 root tty 4, 65 Jul 28 13:05 /dev/modem
crw------ 1 root tty 4, 64 Jul 26 22:20 /dev/ttyS0
crw------ 2 root tty 4, 65 Jul 28 13:05 /dev/ttyS1
crw------ 1 root tty 4, 66 May 5 1998 /dev/ttyS2
crw------ 1 root tty 4, 67 May 5 1998 /dev/ttyS3
```

The numbers ranging from 64 through 67 just before the dates are the device minor numbers, and they, in conjunction with the device major number 4, are a code that tells the kernel what hardware device to use when a program accesses the file. Note that /dev/modem shares the device major and device minor numbers with /dev/ttyS1, because /dev/modem is a hard link to /dev/ttyS1. If you don’t have a /dev/modem file but want to create one, you can use a command such as this:

```
ln /dev/ttyS1 /dev/modem
```

You should use the device name that corresponds to the port on which your modem resides. If you don’t see any of the serial port devices, first be sure that you typed the filenames correctly, including the case (note that the S in ttyS is uppercase). If you still don’t see the appropriate device files, you can run the /dev/MAKEDEV script to create the standard device files. If that doesn’t work, you can use the mknod command to create the files individually, as in this example:

```
mknod /dev/ttyS0 c 4 64
```

You need to change the device filename and minor number as appropriate to create your devices.

One final point about the serial port device files is to note their permissions: crw-------, with ownership by root and group tty. The leading c indicates that these are character devices, and the remainder of the string indicates that the owner has full read/write permissions on the device, and other users have no access. Depending on your configuration, you might want to give other users read/write access to the serial devices by using the chmod and chgrp commands. Providing such access could be a potential security problem, though, because users (or crackers who’ve broken into a user account) can then use the modem devices for just about anything, potentially racking up heavy phone bills or even engaging in illegal activities traceable to your system.

## Using a Terminal Program to Test Your Modem

After you’ve set up your serial ports in what you believe to be the correct way, you should check them by using a simple terminal program. Two common terminal programs for Linux are minicom and seyon. The former is a text-mode program that you can run from a command line or xterm, and the latter is a graphical user interface (GUI) program that requires X. minicom is described in this section, but you can use seyon if you prefer.

To begin the test, type minicom -s to enter the minicom configuration utility. You need to select the Serial port setup option from the menu that appears, and then check that the serial device is correct. It defaults to /dev/modem, so you should either have a /dev/modem device or change the setting as appropriate for your system. You might also want to change the port speed by selecting option E, Bps/Par/Bits. For a 56Kbps modem, a speed of 115200bps is appropriate.

After you’ve configured the program, you can select the Save setup as dfl option, and then the Exit option to run the terminal emulator. minicom displays a few lines of welcoming information, and then initializes the modem with a string like this:

```
AT S7=45 S0=0 L1 V1 X4 &c1 E1 Q0
```
