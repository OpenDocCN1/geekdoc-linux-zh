primary and alternate disks that have been set up on the XP 256, we'll set up the appropriate volumes on the host system. In this example, the host system is a V-Class system.

Let's now cover the steps to create one of these volume groups. First, we'll create a physical volume for each of the disks in the volume group with the pvcreate command. Next, we'll create a directory for the volume group with mkdir. Then we'll create a device special file for the volume group within the directory with mknod. This will set up the directory and special file required for the first of the 10 volume groups. Then we'll create the volume group in which the five primary disks will be contained using vgcreate. We'll specify the first disk when we create the volume group and then include the other disks in the volume group with vgextend. Then we extend the volume group with vgextend to include the five alternate disks. The final step is to create a single logical volume for the entire volume group. You might want to create several logical volumes within a volume group, but in our example, we need only one logical volume that consumes the entire capacity of the volume group, which is 8755 physical extents. The following procedure is the list of manual steps to create the first volume group:

```
# pvcreate /dev/rdsk/c9t0d0 # run for each of the 5 pri disks

# mkdir /dev/vgu01 # make dir for first vol group

# mknod /dev/vgu01/group -c 64 0x01000 # create special file with major
# and minor numbers shown

# vgcreate /dev/vgu01 /dev/dsk/c9t0d0 # place first disk in volume group

# vgextend /dev/vgu01 /dev/dsk/c9t0d1 # extend volume with remaining four
# primary disks disks

# vgextend /dev/vgu01 /dev/dsk/c8t0d0 # extend volume group to include five
# alternate disks

# lvcreate -l 8755 /dev/vgu01 # creates lv01 (lv011 by default)
# that consumes all 8755 extents
```