# 1.11.3 Device Special Files

The UNIX system deviated from the design of all other operating systems of the time by simplifying the way in which programs handled I/O. Every I/O device (disk, printer, modem, etc.) is associated with a device special file, which is one kind of special file. Special files can be accessed using the same system calls as regular files, but the way the kernel handles the system call is different when the file argument is a device special file; the system call activates the device driver for that device rather than causing the direct transfer of data. This frees the programmer from having to write different code for different types of devices: he or she can write a program that performs output without having to know whether the output will go to a disk file, a display device, a printer, or any other device. The program just connects to a file variable, which may be associated at run time with any of these files or devices. This is the essence of device-independent I/O.

To illustrate, suppose a portion of C++ code writes to an output stream as follows:

```
ofstream outfile;
cout << "Where should output be sent? ";
cin >> filename;
outfile.open(filename);
```

On a UNIX system, the user can enter the filename "/dev/console" at the prompt, and the output will go to the display device. If the user enters "myfile" the output will go to myfile. The kernel will take care of the details of transferring the data from the program to the device or the file.

There is another type of special file called a named pipe, also called a FIFO special file, or a FIFO for short. Named pipes are used for inter-process communication on a single host; they will be covered in Chapter 8.

The last type of special file is a socket. Sockets were introduced into UNIX in 4.2BSD, and provide inter-process communication across networks. Sockets are special files in the sense that they are part of the special file system, but they are different than other special files because there are different system calls needed to manipulate them. Sockets will be covered in Chapter 9.

An entry for each device file resides in the directory /dev, although system administrators often create soft links to them in other parts of the file system. The advantages of device files are that

+   - Device I/O is treated uniformly, making it easier to write programs that are device independent;
+   - Changes to the hardware result only in changes to the drivers and not to the programs that access them;
+   - Programs can treat files and devices the same, using the same naming conventions, so that a change to a program to write to a device instead of a file is trivial;
+   - Devices are accorded the same protections as files.

Device files are described in greater depth in Chapter 4 of these notes.

> 30 This is not completely true, since certain versions of UNIX have other special files, such as the door in Sun Solaris. The ones listed here are part of most standards.