One disadvantage worth noting is that dump is unable to back up single directories or files; it can only be used to back up an entire file system. To back up individual files or directories, use tar or cpio. For information on how to use these programs, refer to your Linux documentation.

# Techno Talk: Booting in Single-User Mode

Linux can be booted into single-user mode. This setting skips all system configuration and, after asking your root password, starts you in a root shell. This mode should only be used for special maintenance tasks, such as doing a dump at level 0 or some other emergency-type task. To start your system in single-user mode, at the boot prompt, type the name of the Linux image (tab to see a list of available images) followed by the word single.

A running system can also be “brought down” to single user mode using the shutdown command without the -r (for reboot) or the -h (for halt) options by issuing the following command at the command prompt:

```
shutdown now
```

After a few moments, you’ll be asked for the root password, and then you’ll be “dropped” into single-user mode.

Note that tapes created under one hardware/software configuration are not usually portable to other operating systems or drives. In some environments, even tapes created with older versions of the dump program are unreadable by newer versions of the restore program. So test your backups when you do an upgrade, and keep old versions of the program close by.

# Tape Capacity

The one issue with dump is that it doesn’t calculate how much data your tape can hold for you. Therefore, you’ll need to figure capacity by yourself in order to make correct use of your tape.

This might seem easy enough—but it isn’t. Each tape system has a different density (the amount of data that can be written to one inch of tape). Tapes are of different lengths, and dump calculates all these settings based on a nine-track tape running at 1600 bytes/inch and with a default tape length of 2300 feet. Sound confusing? Don’t give up.

The basic math for calculating your tape drive’s capacity is as follows:

+   1. Write the tape capacity in GB (make sure you don’t use the compressed capacity for this purpose, because that “maximum” capacity will depend on the compressability of your data! If your tape capacity is expressed in terms of megabytes, divide that capacity by 1024.

+   2. Convert your tape length to inches. If the length of your tape is in meters, multiply it by 39.37 to obtain the number of inches. If your tape length is in feet, multiply this number by 12.

+   3. Multiply your tape capacity from step 1 by 1,073,741,824 to obtain the capacity of your tape in bytes.

+   4. Divide your calculation from step 3 by the number you calculated in step 2. This is your tape density.