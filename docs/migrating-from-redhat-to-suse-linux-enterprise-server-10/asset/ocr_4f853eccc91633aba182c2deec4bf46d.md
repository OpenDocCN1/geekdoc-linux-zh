# Change the Runlevel

When starting the system, you can choose a runlevel different from the default runlevel defined in /etc/inittab. The runlevel can also be changed in the running system.

To change the runlevel, you need to understand:

+   Change the Runlevel at Boot

+   Manage Runlevels from the Command Line

# Change the Runlevel at Boot

The standard runlevel is 3 or 5, as defined in the file /etc/inittab by the entry initdefault. However, it is also possible to boot to another runlevel by specifying the runlevel on the kernel command line of GRUB.

Any parameters that are not evaluated by the kernel itself are passed to init as parameters by the kernel. The desired runlevel is simply appended to the boot options already specified in GRUB (in the file /boot/grub/menu.lst), as in the following example:

```
root=/dev/hda1 vga=0x317 resume=/dev/hda2 splash=silent showopts 1
```

As root partition /dev/hda1 is transmitted to the kernel, various parameters including the framebuffer are set, and the system boots to runlevel 1 (single user mode for administration).

# Manage Runlevels from the Command Line

You can change to another runlevel once the system is running by using the command **init**. For example, you can change to runlevel 1 from a command line by entering **init 1**.