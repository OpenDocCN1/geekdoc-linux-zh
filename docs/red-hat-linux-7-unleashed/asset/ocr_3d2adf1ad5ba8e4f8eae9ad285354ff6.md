As mentioned, Linux also supports software RAID. This offers the same capabilities as the hardware version. The main difference is that it puts a bigger load on the system. Apart from having software RAID support in the Linux kernel, there is a suite of tools to set up and maintain RAID disks on your system.

Don't include IDE disks that are on the same controller in a RAID set. Switching between a slave and a master IDE disk is quite slow. If you have such disks in a RAID set they will constantly tend to switch back and forth. This will result in a huge performance hit. Should you also be using disk space on the same disks or controller for swap memory as well, your system can become excruciatingly slow. If you have to use IDE disks for your RAID set, be sure to put them on different IDE interfaces.

The following commands are used to create and use software RAID sets:

+   * /sbin/mkraid—This will create a RAID set. As its parameter you name a RAID set that is specified in /etc/raidtab or an alternative configuration file. All data on the devices that are involved will be destroyed.
+   * /sbin/raidstart—This activates the specified RAID set and makes it available for usage as a "normal" block device or disk.

The configuration file for a RAID set is not at all hard to set up. Take a look at Listing 18.1, which is one of the sample configuration files that comes with the RAID tool suite. The usage and format of the options should be pretty obvious.

# **LISTING 18.1 raid0.conf.sample**

```
# Sample raid-0 configuration

raideev			/dev/md0

raid-level		0	# it's not obvious but this *must* be
			# right after raideev

persistent-superblock	0	# set this to 1 if you want autostart;
			# BUT SETTING TO 1 WILL DESTROY PREVIOUS
			# CONTENTS if this is a RAID0 array created
			# by older raidtools (0.40-0.51) or mdtools!

chunk-size		16

nr-raid-disks		2
nr-spare-disks		0

device			/dev/hda1
raid-disk		0

device			/dev/hdb1
raid-disk		1
```