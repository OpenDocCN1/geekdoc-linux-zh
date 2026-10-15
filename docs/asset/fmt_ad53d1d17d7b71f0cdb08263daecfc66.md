
| New Hardware Delivery (NHD) Kit Installation and Patch Kit Installation | × | × | ✓ | 1. `nhd_install`<br>2. `dupatch` |
| Update Installation, New Hardware Delivery (NHD) Kit Installation, and Patch Kit Installation* | × | × | ✓ | 1. `installupdate`<br>2. `nhd_install`<br>3. `dupatch` |

* This is only supported if you have previously installed the NHD kit on a TruCluster Server version 5.1A cluster.

Table 25-3: Rolling Upgrade Tasks

For more information on this topic, we refer you to Compaq’s Tru64 UNIX New Hardware Delivery Release Notes and Installation Instructions when they become available.

### 25.5.4.1 Install Stage for an Update Install

Let’s now follow the individual steps required to perform the Install Stage for an Update Installation:

1. Shutdown the lead member.

```
# shutdown -hs now
System going down IMMEDIATELY
...
```

2. Update the system firmware on the lead cluster member. Please review the Warning in section 25.5.1.3.

3. Boot to single user mode.

```
P00>>> boot -fl s

Loading vmunix ...
..
INIT: SINGLE-USER MODE
...
```

4. Manually run the `bcheckrc(8)` command to check and mount all file systems.

```
# bcheckrc
Checking device naming:
Passed.
Checking local filesystems
Mounting / (root)
user_cfg.pt: reconfigured
root_mounted_rw: reconfigured
Mounting /cluster/members/member1/boot_partition (boot filesystem)
user_cfg.pt: reconfigured
root_mounted_rw: reconfigured
user_cfg.pt: reconfigured
dsfmgr: NOTE: updating kernel basenames for system at /
scp kewm tty00 tty01 lp0 dmapi scp0 dsk0 dsk1 dsk2 dsk3 dsk4 dsk5 dsk6 dsk7 dsk8 dsk9 dsk10 floppy0 cdrom0 dsk13
Mounting local filesystems
exec: /sbin/mount_advfs -F 0x14000 cluster_root#root /
cluster_root#root on / type advfs (rw)
exec: /sbin/mount_advfs -F 0x4000 cluster_usr#usr /usr
cluster_usr#usr on /usr: Device busy
exec: /sbin/mount_advfs -F 0x4000 cluster_var#var /var
cluster_var#var on /var: Device busy
...
```

```
You selected the following kernel options:
System V Devices
NTP V3 Kernel Phase Lock Loop (NTP_TIME)
Kernel Breakpoint Debugger (KDEBUG)
Packetfilter driver (PACKETFILTER)
STREAMS pktl module (PKCT)
Digital Versatile Disk File System (DVDFS)
ISO 9660 Compact Disc File System (CDFS)
Audit Subsystem
Is that correct? (y/n) [y]: y
```

11. A check is then made for file type conflicts. If obsolete files are detected, you are given the option to archive them, view them, or continue with the Update Installation. In our case, we were not really interested in archiving or viewing obsolete files. You may choose to do otherwise.

```
*** Checking for file type conflicts ***
Working...
Obsolete files are files that were shipped with the previous version
of the operating system that the current version does not require.
Obsolete files are removed during the Update Installation. To save
any of these files, archive them now.
File Administration Menu
--------------------------
a) Archive Files
v) View List of Files
x) Return to Previous Menu
Enter your choice: x
Continuing update install...
```

12. The Update Installation again checks to make sure that we have enough space in our file systems. As you can see, the designers of Tru64 UNIX software are being very careful to ensure that there is indeed enough space to perform an Update Installation.

```
*** Checking file system space ***
Update Installation is now ready to begin software load. Please check the
/var/adm/smlogs/update.log file for errors after the installation is complete.
Do you want to continue the Update Installation? (y/n) [n]: y
```

13. The new version of the Operating System files is copied to a predetermined area for faster and easier access during the roll of the other cluster members. The upgraded Tru64 UNIX Operating System is then loaded.
