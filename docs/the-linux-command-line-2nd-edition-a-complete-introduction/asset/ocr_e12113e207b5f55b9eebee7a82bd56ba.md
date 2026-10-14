+   1. `cd` into a given directory
+   2. List the directory contents with `ls -l`
+   3. If you see an interesting file, determine its contents with `file`
+   4. If it looks like it might be text, try viewing it with `less`

> **Remember the copy and paste trick!** If you are using a mouse, you can double click on a filename to copy it and middle click to paste it into commands.

As we wander around, don’t be afraid to look at stuff. Regular users are largely prohibited from messing things up. That’s the system administrators job! If a command complains about something, just move on to something else. Spend some time looking around. The system is ours to explore. Remember, in Linux, there are no secrets!

Table 3-4 lists just a few of the directories we can explore. Feel free to try more!

# Table 3-4: Directories Found On Linux Systems

| Directory | Comments |
|---|---|
| / | The root directory. Where everything begins. |
| /bin | Contains binaries (programs) that must be present for the system to boot and run. |
| /boot | Contains the Linux kernel, initial RAM disk image (for drivers needed at boot time), and the boot loader.

Interesting files:
- `/boot/grub/grub.conf` or `menu.lst`, which are used to configure the boot loader.
- `/boot/vmlinuz`, the Linux kernel |
| /dev | This is a special directory which contains *device nodes*. “Everything is a file” also applies to devices. Here is where the kernel maintains a list of all the devices it understands. |