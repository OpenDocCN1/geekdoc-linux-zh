# The /dev Directory

Once the Linux kernel can communicate with a device on an interface, it must be able to transfer data to and from the device. For many devices, this is done using device files. Device files are files that the Linux kernel creates in the special /dev directory to interface with hardware devices.

To retrieve data from a specific device, a program just needs to read the Linux device file associated with that device. The Linux operating system handles all the unskillfulness of interfacing with the actual hardware. Likewise, to send data to the device, the program just needs to write to the Linux device file.

As you add hardware devices such as USB drives, network cards, or hard drives to your system, Linux creates a file in the /dev directory representing that hardware device. Application programs can then interact directly with that file to store and retrieve data on the device. This is much easier than requiring each application to know how to directly interact with a device.

There are two types of device files in Linux, based on how Linux transfers data to the device:

+   * Character device files: Transfer data one character at a time. This method is often used for serial devices such as terminals and USB devices.
+   * Block device files: Transfer large blocks of data. This method is often used for high-speed data transfer devices such as hard drives and network cards.

The type of device file is denoted by the first letter in the permissions list, as shown in Listing 23.1.

# Listing 23.1: Partial output from the /dev directory

```
$ ls -al sd* tty*
brw-rw---- 1 root disk  8, 0 Feb 16 17:49 sda
brw-rw---- 1 root disk  8, 1 Feb 16 17:49 sda1
crw-rw-rw- 1 root tty   5, 0 Feb 16 17:49 tty
crw-w----- 1 root tty   4, 0 Feb 16 17:49 tty0
crw-w----- 1 gdm  tty   4, 1 Feb 16 17:49 tty1
```

The hard drive devices, sda and sda1, show the letter b, indicating that they are block device files. The tty terminal files show the letter c, indicating that they are character device files.

There are also a few special character device files that provide useful features for the shell. Ones of note are as follows:

+   * /dev/null: When data is redirected to this device, the data is discarded. This is handy for redirecting program messages that you don’t want displayed.
+   * /dev/random and /dev/urandom: These device files provide access to the kernel’s random number generator. The /dev/random device blocks requests until enough random data has been generated to calculate a true random number.