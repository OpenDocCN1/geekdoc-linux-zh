+   9. On a Debian system, which of the following would build a boot disk?
+   - A. `mkboot /dev/floppy`
+   - B. `makeboot --device /dev/fd0 2.4.18-12`
+   - C. `mkbootdisk --device /dev/fd0 2.4.18-12`
+   - D. `mkboot /boot/vmlinuz`

Answer D is correct because it’s the only one that contains all the right elements to create a Debian boot disk: **mkboot** and the full path of the link to the compressed kernel. Answer A is incorrect because the **mkboot** command doesn’t use the raw floppy device for an argument. Answer B is incorrect because the **makeboot** command is a Windows command. Answer C is incorrect because the **mkbootdisk** command is a Red Hat command.

10. After mapping more `mingetty` to `tty` connections in the `/etc/inittab` file, you want the system to recognize the new configuration but not experience any downtime. In the blank below, enter the exact command with any needed options to accomplish this:

The correct answer is `init q`. There are no alternative answers.