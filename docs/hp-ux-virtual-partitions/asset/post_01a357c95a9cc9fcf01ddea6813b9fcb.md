
## PV Move

0017 current /dev/vg00/lvol2 0005
0018 current /dev/vg00/lvol2 0006
0019 current /dev/vg00/lvol2 0007
0020 current /dev/vg00/lvol2 0008
0021 current /dev/vg00/lvol2 0009
0022 current /dev/vg00/lvol2 0010
0023 current /dev/vg00/lvol2 0011
0024 current /dev/vg00/lvol3 0000
0025 current /dev/vg00/lvol3 0001
0026 current /dev/vg00/lvol3 0002
0027 current /dev/vg00/lvol3 0003
0028 current /dev/vg00/lvol3 0004
0029 current /dev/vg00/lvol4 0000
0030 current /dev/vg00/lvol4 0001
0031 current /dev/vg00/lvol4 0002
0032 current /dev/vg00/lvol4 0003
0033 current /dev/vg00/lvol4 0004
0034 current /dev/vg00/lvol4 0005
0035 current /dev/vg00/lvol4 0006

...

0156 free 0000

From this listing, you can see that *lvol1*, which is roughly 48 MBytes, has many more physical extents assigned to it than *lvol3*, which is roughly 20 MBytes.

### pvmove

You can move physical extents from one physical volume to other physical volumes with this command. By specifying the source physical volume and one or more destination physical volumes, you can spread data around to the various physical volumes you wish with this command.

## Volume Group Commands

- **vgcfgbackup**
This command is used to save the configuration information for a volume group. Remember that a volume group is made up of one or more physical volumes. SAM automatically runs this command after you make an LVM change.

- **vgcfgrestore**
This command is used to restore the configuration information for a volume group.

- **vgchange**
This command makes a volume group active or inactive. With the *-a* option, you can deactivate (*-an*) a volume group or activate (*-ay*) a volume group.

- **vgcreate**
You can create a volume group and specify all of its parameters with this command. You specify a volume group name and all of the associated parameters for the volume group when creating it.

- **vgdisplay**
This displays all information related to the volume group if you use the verbose (*-v*) option, including the volume group name; the status of the volume group; the maximum, current, and open logical volumes in the volume group; the maximum, current, and active physical volumes in the volume group; and physical extent-related information.

The following is an example of using **vgdisplay** for the volume group *vg00*:

```
$ vgdisplay /dev/vg00
```

--- Volume groups ---
VG Name            /dev/vg00
VG Write Access    read/write
VG Status          available
Max LV             255
Cur LV             7
Open LV            7
Max PV             16
Cur PV             1
Act PV             1
Max PE per PV      2000
VGDA               2
PE Size (Mbytes)   4
Total PE           157
Alloc PE           149
Free PE            8
Total PVG          0

- **vgexport**
This command removes a logical volume group from the system, but does not modify the logical volume information on the physical volumes. These physical volumes can then be imported to another system using **vgimport**.

- **vgextend**
Physical volumes can be added to a volume group with this command by specifying the physical volume to be added to the volume group.

- **vgimport**
This command can be used to import a physical volume to another system.

- **vgreduce**
The size of a volume group can be reduced with this command, by specifying which physical volume(s) to remove from a volume group. Make sure that the physical volume to be removed has no data on it before doing this.

- **vgremove**
A volume group definition can be completely removed from the system with this command.

- **vgscan**
In the event of a catastrophe of some type, you can use this command to scan your system in an effort to rebuild the /etc/lvmtab file.

- **vgsync**
There are times when mirrored data in a volume group becomes "stale" or out-of-date. **vgsync** is used to synchronize the physical extents in each mirrored logical volume in a volume group.

## Logical Volume Commands

- **lvcreate**
This command is used to create a new logical volume. A logical volume is created within a volume group. A logical volume may span multiple disks, but must exist within a volume group. SAM will execute this command for you when you create a logical volume using SAM. Many options exist for this command, and two that you would often use are -L to define the size of the logical volume and -n to define the name of the logical volume.

- **lvchange**
This command is used to change the logical volume in some way. For example, you may wish to change the permission on a logical volume to read-write (w) or read (r) with the -p option. Or, you may want to change the strict policy (described under Disk Mirroring) to strict (y), not strict (n), or PVG strict (g).

- **lvdisplay**
This command shows the status and characteristics of every logical volume that you specify. If you use the verbose (-v) option of this command, you get a lot of useful data in many categories, including:

    - 1) Information about the way in which the logical volumes are set up, such as the physical volume on which the logical extents appear; the number of local extents on a physical volume; and the number of physical extents on the physical volume.
    - 2) Detailed information for logical extents, including the logical extent number and some information about the physical volume and physical extent for the logical extent.

The following is an example of **lvdisplay** for the first of the logical volumes (*vol1*) shown in the earlier **bdf** example:

```
$ lvdisplay -v /dev/vg00/lvol1

--- Logical volumes ---
LV Name /dev/vg00/lvol1
VG Name /dev/vg00
LV Permission read/write
LV Status available/syncd
Mirror copies 0
Consistency Recovery MWC
Schedule parallel
LV Size (Mbytes) 48
Current LE 12
Allocated PE 12
Stripes 0
Stripe Size (Kbytes) 0
Bad block off
Allocation strict/contiguous

--- Distribution of logical volume ---
PV Name LE on PV PE on PV
/dev/dsk/c0t1d0 12 12

--- Logical extents ---
LE PV1 PE1 Status 1
0000 /dev/dsk/c0t1d0 0000 current
```

## Logical Volume Manager Background

```
0001 /dev/dsk/c0t1d0  0001 current
0002 /dev/dsk/c0t1d0  0002 current
0003 /dev/dsk/c0t1d0  0003 current
0004 /dev/dsk/c0t1d0  0004 current
0005 /dev/dsk/c0t1d0  0005 current
0006 /dev/dsk/c0t1d0  0006 current
0007 /dev/dsk/c0t1d0  0007 current
0008 /dev/dsk/c0t1d0  0008 current
0009 /dev/dsk/c0t1d0  0009 current
0010 /dev/dsk/c0t1d0  0010 current
0011 /dev/dsk/c0t1d0  0011 current
```

Although most of what is shown in this example is self-explanatory, some entries require explanation. The size of the logical volume is 48 MBytes, which consists of 12 Logical Extents (LEs) and 12 Physical Extents (PE). This means that each physical extent is 4 MBytes in size (4 MBytes x 12 extents = 48 MBytes). We can verify this by running the command to display the characteristics of the physical volume. At the bottom of this listing, you can see the mapping of logical extents onto physical extents. In this case a direct mapping takes place between logical extents 0000 - 0011 and physical extents 0000 - 0011.

- **lvextend**

This command is used to increase the number of physical extents allocated to a logical volume. We sometimes underestimate the size required for a logical volume, and with this command, you can easily correct this problem. You may want to extend a logical volume to increase the number of mirrored copies (using the -m option), to increase the size of the logical volume (using the -L option), or to increase the number of logical extents (using the -l option).

- **extendfs**

Use this command after **lvextend**. Whereas the **lvextend** command expands the logical volume, **extendfs** expands the filesystem within the logical volume. If you forget to issue the **extendfs** command, the logical volume inside SAM will look expanded, but issuing the **bdf** command will not show the expansion.

### lvlnboot

Use this to set up a logical volume to be a root, boot, primary swap, or dump volume (this can be undone with **lvrmbboot**). Issuing the **lvlnboot** command with the -v option gives the current settings.

### lvsplt and lvmerge

These commands are used to split and merge mirrored logical volumes, respectively. If you have a mirrored logical volume, **lvsplt** will split this into two logical volumes. **lvmerge** merges two logical volumes of the same size, increasing the number of mirrored copies.

### lvmmigrate

This command prepares a root file system in a disk partition for migration to a logical volume. You would use this if you had a partition to convert into a logical volume.

### lvreduce

Use this to decrease the number of physical extents allocated to a logical volume. When creating logical volumes, we sometimes overestimate the size of the logical volume. This command can be used to set the number of mirrored copies (with the -m option), decrease the number of logical extents (with the -l option), or decrease the size of the logical volume (with the -L option). Be careful when decreasing the size of a logical volume. You may make it smaller than the data in it. If you choose to do this, make sure that you have a good backup of your data.
