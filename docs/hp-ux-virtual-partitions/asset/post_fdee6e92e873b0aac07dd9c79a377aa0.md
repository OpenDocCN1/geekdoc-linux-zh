
After emptying a logical volume, you can use this command to remove logical volumes from a volume group.

Use this if you don't want a logical volume to be root, boot, primary swap, or a dump device (this is the converse of the **lvlnboot** command). However, unless you have a disk partition to boot from, don't leave the system without a root or boot device designated with the **lvlnboot** command or the system won't know where to boot from.

There are times when mirrored data in a logical volume becomes "stale" or out-of-date. **lvsync** is used to synchronize the physical extents in a logical volume.

## Adding Disks

In this section, we're going to do some work with XP 256 disks. We want to create ten volume groups with five primary disks and five alternate disks per volume group.

Let's take a look at the file that contains the physical disks to be used for the primary and alternate paths on the XP 256. The XP 256 is an advanced storage device that has in it the capability to fail over to an alternate controller, should the primary controller fail. The same set of disks are connected to the primary and alternate controllers, but the disks are given two different sets of device files. One set is for the disks when connected to the primary controller and the second set is for the same disks when connected to the alternate controller. This is the same concept that you may have come across if you are a ServiceGuard user. There are a set of disks connected through two different paths, so you must define the disks with different names depending on whether they are connected through the primary or alternate path. The following is a listing of the file *pri*, containing the primary disks in groups of five:

c9t0d0 c9t0d1 c9t0d2 c8t0d0 c8t0d1
c7t0d0 c7t0d1 c7t0d2 c10t0d0 c10t0d1
c9t0d3 c9t0d4 c9t0d5 c8t0d3 c8t0d4
c7t0d3 c7t0d4 c7t0d5 c10t0d3 c10t0d4
c9t0d6 c9t0d7 c9t1d0 c8t0d6 c8t0d7
c7t0d6 c7t0d7 c7t1d0 c10t0d6 c10t0d7
c9t1d1 c9t1d2 c9t1d3 c8t1d1 c8t1d2
c7t1d1 c7t1d2 c7t1d3 c10t1d1 c10t1d2
c9t1d4 c9t1d5 c9t1d6 c8t1d4 c8t1d5
c7t1d4 c7t1d5 c7t1d6 c10t1d4 c10t1d5

Notice that in this listing, the disks have been grouped in fives. Each group of five disks will constitute a volume group. There are a total of 10 groups of five disks that will be placed in volume groups *vgu01* through *vgu10*.

There will also be an alternate group of five disks. The alternate disks will be used in the event of a disk controller failover as described earlier. The following is a listing of the file *alt*, which contains a list of alternate disks in groups of five:

c8t8d0 c8t8d1 c8t8d2 c9t8d0 c9t8d1
c10t8d0 c10t8d1 c10t8d2 c7t8d0 c7t8d1
c8t8d3 c8t8d4 c8t8d5 c9t8d3 c9t8d4
c10t8d3 c10t8d4 c10t8d5 c7t8d3 c7t8d4
c8t8d6 c8t8d7 c8t9d0 c9t8d6 c9t8d7
c10t8d6 c10t8d7 c10t9d0 c7t8d6 c7t8d7
c8t9d1 c8t9d2 c8t9d3 c9t9d1 c9t9d2
c10t9d1 c10t9d2 c10t9d3 c7t9d1 c7t9d2
c8t9d4 c8t9d5 c8t9d6 c9t9d4 c9t9d5
c10t9d4 c10t9d5 c10t9d6 c7t9d4 c7t9d5

There are a total of 10 groups of alternate disks shown in this listing that will also be part of volume groups *vgu01* through *vgu10*. Using these primary and alternate disks that have been set up on the XP 256, we'll set up the appropriate volumes on the host system. In this example, the host system is a V-Class system.

Let's now cover the steps to create one of these volume groups. First, we'll create a physical volume for each of the disks in the volume group with the pvcreate command. Next, we'll create a directory for the volume group with mkdir. Then we'll create a device special file for the volume group within the directory with mknod. This will set up the directory and special file required for the first of the 10 volume groups. Then we'll create the volume group in which the five primary disks will be contained using vgcreate. We'll specify the first disk when we create the volume group and then include the other disks in the volume group with vgextend. Then we extend the volume group with vgextend to include the five alternate disks. The final step is to create a single logical volume for the entire volume group. You might want to create several logical volumes within a volume group, but in our example, we need only one logical volume that consumes the entire capacity of the volume group, which is 8755 physical extents. The following procedure is the list of manual steps to create the first volume group:

```
# pvcreate /dev/rdsk/c9t0d0 # run for each of the 5 pri disks

# mkdir /dev/vgu01 # make dir for first vol group

# mknod /dev/vgu01/group -c 64 0x01000 # create special file with major
# and minor numbers shown

# vgcreate /dev/vgu01 /dev/dsk/c9t0d0 # place first disk in volume group

# vgextend /dev/vgu01 /dev/dsk/c9t0d1 # extend volume with remaining four
# primary disks

# vgextend /dev/vgu01 /dev/dsk/c8t0d0 # extend volume group to include five
# alternate disks

# lvcreate -l 8755 /dev/vgu01 # creates lv01 (lv011 by default)
# that consumes all 8755 extents
```

We completed the procedure for only one disk, and there are nine additional disks in this volume group. In addition, there are another nine volume groups for which this procedure must be completed. That is a total of an additional 99 disks for which various commands must be run. There is a lot of room for error with that much typing involved so this is an ideal process to automate.

Since there are a primary set of disks and an alternate set of disks we'll write a short program to automate each procedure. The following program performs all of the steps required to create a physical volume for each disk, create a volume group, and include the primary disks in it:

```
#!/bin/ksh
set -x            ;set tracing on
vgnum=$1          ;first item on each line is the volume group no.
shift             ;shift to get to first disk

for i in $*       ;run pvcreate for every disk name in first line
do
    pvcreate /dev/rdsk/$i
done

reada             ;pause program to view what has been run

mkdir /dev/vgs$vgnum         ;mkdir for volume group
mknod /dev/vgs$vgnum/c0g5$vgnum 0000 ;mknod for volume group
vgcreate /dev/vgs$vgnum /dev/dsk/$1 ;vgcreate 1st disk in vg

shift             ;shift over to second disk
for i in $*       ;extend volume group to include remaining four disks
do
    vgextend /dev/vgs$vgnum /dev/dsk/$i
done

lvcreate -l 8755 /dev/vgs$vgnum ;create single log vol for entire vg
```

I use **set -x** in this file to turn on execution tracing. I always do this when first debugging a shell program so I can see the lines in the shell program as they are executed. The line being executed will appear with a "+" in front of it, followed by what you would normally see when the program is run. **The read a** is a way of pausing the program to wait for input so I can review what has been run to that point of the program.

In order for this program to run, we must slightly modify the file containing the primary disk devices and add the volume group number to the beginning of each line. In addition, I decided to call the program from the file that has the primary disks in it and operate on one line of disks at a time. The following listing shows the updated file containing the name of the shell program in the previous listing (**vg.sh**), followed by the volume group number and then the list of five primary disks names for each volume group:

```
#vg.sh 01 c9t0d0 c9t0d1 c9t0d2 c8t0d0 c8t0d1
#read a
#vg.sh 02 c7t0d0 c7t0d1 c7t0d2 c10t0d0 c10t0d1
#read a
#vg.sh 03 c9t0d3 c9t0d4 c9t0d5 c8t0d3 c8t0d4
#read a
#vg.sh 04 c7t0d3 c7t0d4 c7t0d5 c10t0d3 c10t0d4
#read a
#vg.sh 05 c9t0d6 c9t0d7 c9t1d0 c8t0d6 c8t0d7
#read a
#vg.sh 06 c7t0d6 c7t0d7 c7t1d0 c10t0d6 c10t0d7
#read a
#vg.sh 07 c9t1d1 c9t1d2 c9t1d3 c8t1d1 c8t1d2
#read a
#vg.sh 08 c7t1d1 c7t1d2 c7t1d3 c10t1d1 c10t1d2
#read a
#vg.sh 09 c9t1d4 c9t1d5 c9t1d6 c8t1d4 c8t1d5
#read a
#vg.sh 10 c7t1d4 c7t1d5 c7t1d6 c10t1d4 c10t1d5
```

**The read a** between lines of this file will pause and wait for you to enter a **Return** before the next line will be executed. I did this in case I decided to run several lines and I wanted to check the results between the execution of lines.

We can now uncomment the first line of the file and type the file name **pri**, which will call **vg.sh** and run the program (you must give appropriate permissions to the files and make sure both **vg.sh** and **pri** are executable.)
