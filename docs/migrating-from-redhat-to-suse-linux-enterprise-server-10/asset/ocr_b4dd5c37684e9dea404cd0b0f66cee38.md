# Boot a System Directly into a Shell

The boot screen of the GRUB boot loader lets you pass parameters that modify the Linux kernel before the kernel is actually loaded.

At the bottom of the GRUB boot screen is a Boot Options field. To add a boot option, select an operating system and type the additional boot option in the Boot Options field.

One way to access a system that is not booting anymore is to set a different program for the init process. Normally, the Linux kernel tries to find a program with the name init and starts this program as the first process. All other processes are then started by init.

With the boot parameter init=new_init_program, you can change the first program loaded by the kernel. For example, by entering the boot parameter init=/bin/bash, the system is started directly into a bash shell. You are directly logged in as root without being asked for a password.

> You could consider this somewhat equivalent to RHEL’s runlevel 1, where you are not asked for the root password before getting a shell.

You can use this bash file to access the file system and to fix a misconfiguration.

> The file systems are mounted as read-only after booting into a shell. To change configuration files, you need to remount the file system with the following command:
> **mount -o remount,rw,sync -t filesystem_type device_name mount_point**
> Enter **exec /sbin/init** at the bash prompt replaces the shell by the init program and continues the boot process until the default runlevel is reached.

**1 HARDCOPY PERMITTED-NO DISTRIBUTION ALLOWED**