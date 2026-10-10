+   • Basic - configuration and environment information.

+   • Software - ability to choose optional software to be installed. Mostly the same options that appear under Guided Installation.

+   • System - networking parameters. Also configurable via the set_params command.

+   • File System - disk space allocation.

+   • Advanced - advanced disk, file system, logical volume, and volume group parameters.

We configure our system beginning with the Basic screen as shown in Figure 1-4.

Items of particular importance are discussed below:

+   • Configuration - we use HP-UX B.11.11 Default. HP-UX 11i is called by its original name, 11.11, in some cases.

+   • Environments - there are four 11i environments to select from at the time of this writing. This is a major change in the software distribution method for HP-UX 11i. The Operating Environments are bundles of software that make installing 11i easier. We'll select the first of the four, which is the top level, or most elaborate, of the Operating Environments as shown in the following example:

![](bbox=[0.15, 0.65, 0.85, 0.74])

+   • Root Disk - the default selection for the root disk is the first internal disk drive, which is the disk with a path of 0/0/1/2.0 in our example.

+   • File System - we are given the option of choosing holedisk (not LVM) with HFS, Logical Volume Manager with HFS, or Logical Volume Manager with VxFS. If you have not reviewed the Logical