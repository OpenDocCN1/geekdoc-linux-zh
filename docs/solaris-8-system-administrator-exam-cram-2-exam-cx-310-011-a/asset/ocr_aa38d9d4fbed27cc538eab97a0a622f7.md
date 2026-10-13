```
```text
/dev/fd on fd read/write on Tue Apr 3 21:39:12 2001
/etc/mnttab on mnttab read/write on Tue Apr 3 21:39:17 2001
/var/run on swap read/write on Tue Apr 3 21:39:17 2001
/tmp on swap read/write on Tue Apr 3 21:39:19 2001
/export/home on /dev/dsk/c0d0s7 read/write on
    Tue Apr 3 21:39:19 2001

#
```
```

# The prtconf Command

The **prtconf** command displays system configuration information. Devices are identified by using the driver binding name and instance number, which compose the instance name. The following example shows the output from the **prtconf** command on an x86 Solaris 8 system:

```
```text
# prtconf
System Configuration:  Sun Microsystems  i86pc
Memory size: 128 Megabytes
System Peripherals (Software Nodes):

i86pc
    +boot (driver not attached)
        memory (driver not attached)
    aliases (driver not attached)
    chosen (driver not attached)
    i86pc-memory (driver not attached)
    i86pc-mmu (driver not attached)
    openprom (driver not attached)
    options, instance #0
    packages (driver not attached)
    delayed-writes (driver not attached)
    itu-props (driver not attached)
    isa, instance #0
        motherboard (driver not attached)
            asy, instance #0
            lp, instance #0 (driver not attached)
        fdc, instance #0
            fd, instance #0
            fd, instance #1 (driver not attached)
    i8042, instance #0
        keyboard, instance #0
        mouse, instance #0
    bios (driver not attached)
    bios (driver not attached)
    pnpTCM,5090, instance #0
```
```

# The sysdef Command

The **sysdef** command displays the system configuration or definition that lists all hardware devices, including pseudo and system devices, loadable modules, and tunable kernel parameters. Like the **prtconf** command, **sysdef** identifies devices by using the driver binding name and instance number, which compose the instance name. The following example shows the partial output of the **sysdef** command: