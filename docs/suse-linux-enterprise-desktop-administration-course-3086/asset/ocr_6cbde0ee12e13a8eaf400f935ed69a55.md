Table 7-10 shows directories that cannot be imported from other computers. They must always be located locally on each computer.

| Directory | Description |
|---|---|
| `/bin` | Basic programs and utilities (ls, cat, mount, vi, and so on) |
| `/boot` | Kernel and boot files |
| `/dev` | Device files |
| `/etc` | Configuration files |
| `/lib` | Libraries |
| `/sbin` | Programs needed for system administration |

Table 7-10

![](bbox=[0.037, 0.378, 0.222, 0.45])

# Exercise 7-1: Explore the SUSE Linux File System Hierarchy

In this exercise, describe what directories the characters `/` and `~` refer to. Then, find out the mount point of the DVD. Mount the DVD manually at another position (`/mnt`) in the file system.

# Detailed Steps to Complete This Exercise

+   1. Describe what directories the following characters refer to:
+      - `/`
+      - `~`
+   2. From the GNOME desktop, open the main menu.
+   3. Select More Applications.
+   4. In the Filter text box, enter `term`.
+   5. Select the GNOME Terminal icon to start a terminal emulation.
+   6. Log in as root by entering `su -` with a password of `n0v3ll`.
+   7. Insert a *SUSE Linux Enterprise Desktop 10 SP1 Product DVD* into your DVD-ROM drive.
+      A Nautilus window appears, showing the content of the DVD. Note the name of the directory used for mounting here.
+   8. Find out the device of the DVD drive by entering `mount`. Note the device (for instance `/dev/hdc`) that is listed in the same line as the mountpoint noted in the previous step.
+   9. Display the content of the `/media/mountpoint` directory by entering:

```
ls /media/mountpoint
```

The content of the DVD is listed.