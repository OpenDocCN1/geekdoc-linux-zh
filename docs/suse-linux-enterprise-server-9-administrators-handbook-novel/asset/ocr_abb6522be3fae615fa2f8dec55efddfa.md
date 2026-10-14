# LISTING 3.2

**Grub menu.lst (continued)**

```
###Don't change this comment - YaST2 identifier: Original
  name: failsafe###
title Failsafe
    kernel (hd0,0)/boot/vmlinuz root=/dev/sda1 showopts
    ide=nodma acpi=off acpi=off vga=normal noresume
    selinux=0 barrier=off nosmp noapic maxcpus=0 3
        initrd (hd0,0)/boot/initrd
```

Grub is different from LILO in that the information in the file is interpreted dynamically as the machine is being booted. This has the benefit of allowing new kernels to be quickly added to the system. The Grub menu.lst file can be updated with any text editor, and unlike LILO, no further steps are necessary to make the option available at boot time. Additional information on GRUB can be found in the man pages or at the GRUB home page at http://www.gnu.org/software/grub/grub.html.

An additional feature available through Grub is the capability to modify the menu entries. Pressing Esc when the graphical Grub menu is present triggers Grub to offer the curses version of the boot menu. In this version of the menu, you can edit individual lines controlling the kernel parameters. Instructions on how to do this are provided at the bottom of the boot option screen, as shown in Figure 3.1.

![](bbox=[0.068, 0.618, 0.815, 0.922])

One of the benefits of this option is that you can boot directly into single user mode. In the case of a machine going down for an unknown reason, you can