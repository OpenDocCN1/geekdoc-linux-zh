$ sudo csh sam
Password:
Changing the login shell for sam
Enter the new value, or press ENTER for the default
Login Shell [/bin/bash]: /bin/tcsh

See page 293 for more information.

| clear | Clears the screen. You can also use CONTROL-L from the bash shell to clear the screen. The value of the environment variable TERM (page 1106) determines how to clear the screen. |
| dmesg | Displays recent system log messages (page 589). |
| e2label | Displays or creates a volume label on an ext2, ext3, or ext4 filesystem. You must run this utility with root privileges. An e2label command has the following format: |
|         | $ e2label device [newlabel] |
|         | where device is the name of the device (e.g., /dev/hda2, /dev/sdb1, /dev/fd0) you want to work with. When you include the optional newlabel parameter, e2label changes the label on device to newlabel. Without this parameter, e2label displays the label. You can also create a volume label with the -L option of tune2fs (page 512). |
| lshw | Lists hardware. This utility provides complete information only when run with root privileges. Use the -short option to display a brief listing. See page 640 for more information. |
| mkfs | Creates a new filesystem on a device, destroying all data on the device as it does so. This utility is a front-end for many utilities, each of which builds a different type of filesystem. By default, mkfs builds an ext2 filesystem and works on either a hard disk partition or a floppy diskette. Although it can take many options and arguments, you can use mkfs simply as |
|         | $ sudo mkfs device |
|         | where device is the name of the device (/dev/hda2, /dev/sdb1, /dev/fd0, and so on) you want to make a filesystem on. Use the -t option to specify a type of filesystem. As an example, the following command creates an ext4 filesystem on /dev/sda2: |
|         | $ sudo mkfs -t ext4 /dev/sda2 |
|         | An example using mkfs to create a filesystem on a floppy diskette appears on page 509. |
| ping | Sends packets to a remote system. This utility determines whether you can reach a remote system through the network and tells you how long it takes to exchange messages with the remote system. Refer to “ping: Tests a Network Connection” on page 393. |
| reset (link to tset) | Resets terminal characteristics. The value of the TERM environment variable (page 1106) determines how the screen will be reset. The screen is cleared, the kill and interrupt characters are set to their default values, and character echo is turned on. When given from a graphical terminal emulator, this command also changes the size of the window to its default. The reset utility is useful for restoring the screen to |