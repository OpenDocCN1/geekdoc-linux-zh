+   3. Do a reconfiguration reboot by entering **ok boot -r** on a SPARC system or **b -r** on an IA system. (A `reboot -r` on either system when you are logged in to the shell as root will also do a reconfiguration reboot.)

The `-r` option reconfigures the system upon reboot. Your system will query all devices on internal and external buses to see if they are operable. Then the `reconfiguration` dynamically rebuilds the `/devices` and `/dev` directories based on the device hierarchy it sees.

+   4. At the OpenBoot prompt enter the following:

```
```
# touch /reconfiguration
# sync; sync; init 6
```
```

+   5. Insert a disk into the drive, boot your computer, then enter **format** at the command line to format the disk.

+   6. Create a file system on your disk by entering the following at the command line (where `n` is the drive number for your device):

```
``` # newfs -v/dev/sdnc ```
```

+   7. Make a mount point directory by entering **mkdir /zip** or **mkdir /jaz** at the command line.

+   8. Create a mount point by typing **mount /dev/sdnc /zip** or **mount /dev/sdnc /jaz** at the command line.

So in truth, adding a *Zip* or *Jaz* drive isn’t very different than adding a hard drive to your system, as you will see in the next section. The key differences are that you need to know what to enter into the `format.dat` file, and you don’t typically slice and dice a *Zip* or *Jaz* drive. You can surmount the limitation of not being able to work with read-only disks for these devices by using a program called *ziptool* (see `fy.chalmers.se/~appro/ziptool.html`).

# # Hard Drives

Hard drive or disk management is among the most critical tasks that you face when you administer Solaris systems. An understanding of how hard drives are configured is also essential to a number of operating system functions that you may need to perform on a day-to-day basis and is helpful to even the average Solaris user. For the following discussion on dealing with internal disks, I’ll assume that you are familiar at a basic level with standard computer terms such as *tracks*, *cylinders*, *sectors*, and *partitions*.