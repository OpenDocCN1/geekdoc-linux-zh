implemented using persistent superblocks placed on each RAID disk to hold configuration information. A persistent superblock needs to be created when you create the RAID device using mkraid. To instruct mkraid to create a persistent superblock, you specify the persistent-superblock option in the /etc/raidtab file, the RAID configuration file. Without the persistent superblock option, you would have to manually start your RAID devices with the raidstart command. raidstart -a starts up all your devices.

# RAID Tools

The RAID tools are useful for managing software RAID devices on Linux. mkraid creates a RAID device, raidstop stops the device, and raidstart turns it on (see Table 31-2). These are discussed in detail in the next section.

# Creating and Installing RAID Devices

If you created your RAID devices and their partitions during the installation process, you should already have working RAID devices. Your RAID devices will be configured in the /etc/raidtab file, and the status of your RAID devices will be listed in the /proc/mdstat file. You can manually start or stop your RAID devices with the raidstart and raidstop commands. The -a option operates on all of them, though you can specify particular devices if you want.

To create a new RAID device manually for an already installed system, follow these steps:

+   1. Make sure that your kernel supports the RAID level you want for the device you are creating. To enable support for a RAID level in the kernel, use the kernel configuration tool to create a module for it, as discussed previously.
+   2. If you have not already done so, create the RAID disks (partitions) you will use for your RAID device.
+   3. Configure your RAID device (/dev/md n) in the /etc/raidtab file, specifying the RAID disks to use. Be sure to specify the persistent superblock option to have your RAID devices automatically detected when you boot.
+   4. Create your RAID device with mkraid.
+   5. Activate the RAID device with raidstart.
+   6. Create a file system on the RAID device (mkfs) and then mount it.

# TABLE 31-2
RAID Tools

| Tool | Description |
|------|-------------|
| mkraid | Creates (configures) RAID devices from a set of block devices, initializing them. |
| raidstart | Activates RAID devices. |
| raid0start | Activates older nonpersistent linear and RAID 0 RAID devices. |
| raidstop | Turns off a RAID device. |