# HP-UX kernel configuration

431

asy, instance #0 (driver not attached)
asy, instance #1 (driver not attached)
fdc, instance #0
fd, instance #0 (driver not attached)
pit_beep, instance #0

The prcntf -D display shows drivers to load in /etc/system.

```
solaris$ sudo prcntf -D
System Configuration: Sun Microsystems i86pc
Memory size: 580 Megabytes
System Peripherals (Software Nodes):
```

+   - i86pc (driver name: rootnox)
- scsi_vhci, instance #0 (driver name: scsi_vhci)
- isa, instance #0 (driver name: isa)
- 8042, instance #0 (driver name: 8042)
- keyboard, instance #0 (driver name: kb8042)
- mouse, instance #0 (driver name: mouse8042)
- lp, instance #0 (driver name: eccp)
- asy, instance #0 (driver name: asy)
- asy, instance #1 (driver name: asy)
- fdc, instance #0 (driver name: fdc)
- fd, instance #0 (driver name: fd)
- pit_beep, instance #0 (driver name: pit_beep)

**sysdef** on steroids. In addition to the information given by prcntf, it also lists pseudo-device drivers, tunable kernel parameters, and the filenames of loaded modules. If you modify the default kernel for an important machine, consider including the output of **sysdef** in your documentation for the machine.

The **modinfo** command reports information about dynamically loaded modules. Solaris dynamically loads drivers, STREAMS and filesystem drivers, among other things. Don't be surprised if **modinfo** output contains more than 200 entries. See page 435 for more information about **modinfo**.

# 13.5 HP-UX KERNEL CONFIGURATION

HP-UX is the most monolithic among our example operating systems, and it prefers to load modules statically. It has a complex and confusing configuration file. Fortunately, HP provides a hardware configuration tool known as **kcweb**, which runs as a GUI if X Windows and a browser are available, or on the command line alone. To force command-line operation, use **kcweb -t**.

HP-UX reads kernel configuration parameters (such as modules and tunable variables) from the **/stand/system file**. This file is maintained by **kcweb** and other, and administrators should not modify it directly.

Modules and configuration options can be static or dynamic. A static value or module is one that requires a kernel rebuild and a reboot to change or install.

![](bbox=[0.953, 0.658, 0.996, 0.781])