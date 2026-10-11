**Table 3.14** Flags available for the *shutdown* command (continued).

| Flag | Purpose | Arguments | Example |
| --- | --- | --- | --- |
| -r | Reboots the system. | None | `shutdown -r now` |
| -t | The time to wait before the command should go into effect. | Seconds to wait, using the word **now** signifies that the event should happen immediately (the flag is not necessary with **now**) | `shutdown -ht 30` |

# Making A Custom Boot Disk

The boot disk you got with the distribution materials is not sufficient if the machine is already installed and not booting properly. You need to have a custom boot disk on hand that has the information necessary for your configuration. To make this disk, do the following as root:

+   1. Type "uname -r" to get the exact version of the kernel you are using.
+   2. Put a floppy in the floppy drive—it must be a floppy disk, you cannot use another type of media to make a boot disk.
+   3. Type "mkbootdisk --version *version*", where *version* is the result of the command in Step 1. Press Enter.
+   4. Be sure the floppy is in the drive, and then follow the instructions on the screen. Once the program is finished writing to the floppy, it is safe to remove it from the drive.
+   5. Clearly label the floppy as a boot disk for the particular machine in question and put it in a place you can find it easily if needed.

> *NOTE: This process works on most current Linux distributions.*

# Making A Rescue Disk

Red Hat offers a special rescue disk to make system recovery easier, in conjunction with the custom boot disk. Do the following as root to create a rescue disk:

+   1. Place a floppy in the floppy drive.
+   2. Mount the Red Hat distribution CD, or copy the *rescue.img* file onto the file system from its FTP site.