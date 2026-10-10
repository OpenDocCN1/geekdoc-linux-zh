Follow the prompts as the command offers *repair* options. Portions of files or data collected during the repair option will be placed in your system's *lost+found* directory. After the repair is complete, you'll use the `exit` command, and Linux will reboot.

Here's the best way to avoid any hard drive problems with Linux: Always perform a proper shutdown or reboot! The `shutdown` command may be used with the `-h` (halt) option or the `-r` (reboot) option, followed by the word *now* or the number `r` to immediately shut down or reboot the notebook. You can also specify a time delay in seconds and include a message to send to all logged-on users. For example:

```
# /sbin/shutdown -r -t 300 “System is going down in 5 minutes.”
```

This will reboot your notebook in 5 minutes and send the message to everyone who is logged on. You can cancel a shutdown by using the `-c` (cancel) option:

```
# /sbin/shutdown -c
```

Never just turn off your computer! Mobile Linux users need to be sure that APM is properly working and configured in order to suspend or hibernate the laptop before power runs out. This will save you untold headaches!

# # Restoring Your Hard Drive

If you use Mandrake or Red Hat Linux and you did not create an emergency boot disk when you installed Linux, follow these steps right now:

+   1.  Insert a blank floppy in your notebook's floppy drive.
+   2.  Use the `uname` command and its `-r` (revision) option to get the revision number of the current Linux kernel:
+       ```
+       # uname -r
+       ```
+       ```
+       2.2.14-15mdk
+       ```
+   3.  Use the `mkbootdisk` command along with the information returned by the `uname` command:
+       ```
+       # mkbootdisk --device /dev/fd0 2.2.14-15mdk
+       ```
+       ```
+       Insert a disk in /dev/fd0. Any information on the disk will be lost.
+       ```
+       ```
+       Press “Enter” to continue or “C” to abort:
+       ```
+   4.  After you press Enter, your boot disk will be created. Keep this disk in a safe place.