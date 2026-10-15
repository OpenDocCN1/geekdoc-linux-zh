# 6.4.2 Disk management

# Enabling a disk in Linux

After the new disk has been defined, is in the directory, and is dynamically attached to the guest (as explained in section 5.3.9, “Managing DASD” on page 258), it can be enabled in Linux.

Use the lscss command, which stands for List Channel Subsystem to show all the devices that are attached to your system. Example 6-1 shows the output of the lscss command before and after attaching the disk as device 0200.

# Example 6-1 The lscss command output, before and after attaching new DASD to guest

```
lnxguill:~ # lscss
Device   Subchan. DevType CU Type Use  PIM PAM POM CHPID
------------------------------------------------------------
0.0.0191 0.0.0000 3390/0A 3990/E9     F0 F0 FF 52565A5E 00000000
0.0.0100 0.0.0001 3390/0C 3990/E9 yes F0 F0 FF 5054585C 00000000
0.0.0101 0.0.0002 9336/10 6310/80 yes 80 80 FF 00000000 00000000
0.0.0150 0.0.0003 3390/0C 3990/E9 yes F0 F0 FF 5054585C 00000000
[...]
lnxguill:~ # lscss
Device   Subchan. DevType CU Type Use  PIM PAM POM CHPID
------------------------------------------------------------
0.0.0191 0.0.0000 3390/0A 3990/E9     F0 F0 FF 52565A5E 00000000
0.0.0100 0.0.0001 3390/0C 3990/E9 yes F0 F0 FF 5054585C 00000000
0.0.0101 0.0.0002 9336/10 6310/80 yes 80 80 FF 00000000 00000000
0.0.0150 0.0.0003 3390/0C 3990/E9 yes F0 F0 FF 5054585C 00000000
[...]
0.0.0200 0.0.0012 3390/0C 3990/E9     F0 F0 FF 5054585C 00000000
lnxguill:~ #
```

At this point, the disk is seen by Linux, but it has to be enabled for the operating system to be able to use it. The disk is enabled with chccwdev command, as shown in Example 6-2, is provided by IBM and delivered in the s390-tools package.

# Example 6-2 Enabling a disk for Linux

```
lnxguill:~ # chccwdev -e 0.0.0200
Setting device 0.0.0200 online
Done
lnxguill:~ #
```

To enable a device, use the -e switch; to disable a device, use the -d switch. When the disk is brought online, the Linux kernel assigns the disk a device node