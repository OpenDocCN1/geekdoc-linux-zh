# Booting from the Hard Disk with Special Boot Parameters

Sometimes it is enough to boot the system from hard disk, but into runlevel 1 (by simply typing the digit 1 as a boot parameter in the initial boot screen). Runlevel 1 is single-user mode, with no networking and without starting most services. So if there is a problem that is causing the boot process to fail at a later stage, you may be able to solve the problem by booting into runlevel 1 and making the necessary changes. You can run YaST or edit configuration files in this state, and then reboot or boot the system up to runlevel 3 or 5 with one of the commands `init 3` or `init 5`.

Chapter 4 has more information on booting into special runlevels.

If you have lost the password, you can boot with the following parameter:

```
init=/bin/bash rw
```

This starts the system that bypasses the normal `init` system, instead taking you straight to a shell, without the need to log in, and mounting the root partition read-write. You can then, if necessary, remove the root password by editing the file `/etc/shadow` using `vi` and removing the encrypted password. You need to change it from looking something like the first line to something like the second.

```
root:cJLGWoEn1Ngqk:12629:0:10000:::
```

```
root::12629:0:10000::
```

You can then reboot to runlevel 1 as described previously and you will be able to log in as root without a password, and reset the password using `passwd` command.

# Booting into the Rescue System

The SUSE installation media offers a special option when you boot from them: One of the menu items is `Rescue System`. If you boot from the first CD or DVD and choose this option, a Linux system that runs in memory loads and does not mount any hard disk partitions. You can log into it as the `root` user without a password.

You can then mount any of the partitions on the hard disk to `/mnt` and make changes before rebooting. For example, if your root partition is `/dev/hda1`, you could do the following:

```
Rescue:- # mount /dev/hda1 /mnt
```