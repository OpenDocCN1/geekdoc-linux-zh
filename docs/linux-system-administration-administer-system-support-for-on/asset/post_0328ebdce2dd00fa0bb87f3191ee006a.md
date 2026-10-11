
The -a option turns quotas on for all file systems. You can specify specific file systems (for example, `quota /home`), which enables quotas for the /home directory where most user files are stored. You can also define quotas on all file systems (or on a specific file system) for a particular user or group. Use the -u option for a user or -g for groups.

To turn quota off, use the command `quotaoff`. It accepts the same options as `quotaon`.

If you are a user on the system, and you type `quota`, you should see this message:

```
$ quota
Disk quotas for user stripes (uid 1000): none
```

Turn on quotas after you mount your file systems as read-write. To do so, do a couple of things. The first one is defining your file systems as quota-enabled in the /etc/fstab.

To do so, edit the /etc/fstab and add the quotatype after the defaults option. The quota types you can have are `usrquota` and `grpquota`. If you want both, be sure to place a comma after each type.

```
/dev/sda2        /home     ext2    defaults,usrquota,grpquota        1 1
```

Quota is only available on ext2fs, so make sure you don’t try to enable it for any other type of file systems.

Next, you’ll need to turn on quota in your startup script (for example, /etc/rc.d/rc.M). Be sure to turn on quota after the file systems are mounted as read-write, otherwise your computer will complain.

![](img/8ad518fddafc7f5e73715a2604b61d50_106_0.png)

You should already have quota turned off in the scripts /etc/rc.d/rc.0 and /etc/rc.d/rc.6, which shut down and reboot respectively. If not, make sure you correct that situation.

Always create quota.user and quota.group in the partition(s) on which you want to impose disk quotas. To do so, just touch the files and change their permissions to root read-writable only. For the user file, you can do this:

```
# touch /dev/sda2/quota.user
# chmod 600 /dev/sda2/quota.user
```

Because you made a change to the file system, you’ll need to reboot. After rebooting, run `quotacheck -avug` to check the file systems and make sure the quota is working properly.

To edit a quota for a particular user, first make sure you are root and type the command

```
# edquota username
```

This should bring up your default editor and the user's quota you want to edit. You can change the soft limits, which warn users that they are above quota, and hard limits, which the user cannot exceed. These can be changed to increase disk space for users. You can also change the amount of inodes a user can have.

![](img/8ad518fddafc7f5e73715a2604b61d50_107_0.png)

> Don't edit a user's quota file with only the editor; use the **edquota** command.

You can enable a grace period for a time limit before the soft quota is enforced. In other words, if a user goes over their soft quota, you can enable them to have a certain amount of time before that soft quota is enforced. Time can be defined in any basic increment (from seconds to months).

To define a grace period, use the -t option. Replace 0 days with whatever time you feel is reasonable.

```
# edquota -t
```

Now that you've enabled quotas, let's look at bob's disk usage and quotas.

```
# quota bob
Quotas for user bob:
  /dev/sda2: blocks in use: 879, limits (soft = 4000, hard = 5000)
  inodes in use: 894, limits (soft = 1000, hard = 2000)
```

If bob wants to look at his disk quota and usage, all he has to type is *quota*.

```
$ quota
Quotas for user bob:
  /dev/sda2: blocks in use: 879, limits (soft = 4000, hard = 5000)
  inodes in use: 894, limits (soft = 1000, hard = 2000)
```

For quota reporting, the command `repquota -avug` should display all the quotas enabled for each disk, group, and user.

# Swap Space

If you have kids, what do they do when they clean up their rooms? They shift the mess from the floor to everywhere else – the closet, desk drawers, under the bed. In a sense, swap space works the same way.

If you are using `gcc`, X-Window, or any other resource-intensive applications, your system will slow considerably unless you use **swap**. As a child would do when he’s done with a toy – throwing it in the closet and taking out another to play with – Slackware Linux moves the stuff it’s not using to hard drive storage freeing memory for other programs it is currently using. So, Linux is putting away one toy and taking out another. However, if you have a lot of RAM, you may not need swap space because the memory can move around in itself, as opposed to using disk space.

## Creating Swap Space

Before you add your swap space, decide how much you need. If you have 64 megabytes or less, double that amount and allocate it for swap space. For example, my PC has 32 megabytes of RAM, so, I’ve allocated 64 megabytes of swap space.

To create swap space, go into `fdisk` and add it. I’ll use my computer as an example.

> **TIP** For initially configuring swap space, configure your other partitions first; and your swap space last. That way you have your partitions in numerical order (1, 2, 3, and so on), without skipping any.

So, we’ll run `fdisk` on my computer, which will default to using `/dev/hda`.

```
# fdisk
Using /dev/hda as default device!
```

Now, let’s look at the partition table. This shows everything that the `df` command does (except how much space is being used on each disk), and it also displays the swap space.

```
Command (m for help): p

Disk /dev/hda: 128 heads, 63 sectors, 525 cylinders
Units = cylinders of 8064 * 512 bytes

Device   Boot    Begin     Start       End     Blocks    Id    System
/dev/hda1             1         1       127      512032+  83    Linux native
/dev/hda2           128       128       254      512064   83    Linux native
/dev/hda3           288       288       525      959616   83    Linux native
```

Great. We still have cylinders 288 to 525 left for swap space. This is somewhere around 120 megabytes. To create a swap partition, we need to create a new partition in much the same way we did while creating the file system.

```
Command (m for help): n
Command action
   e   extended
   p   primary partition (1-4)
p
Partition number (1-4): 4
First cylinder (255-525): 255
Last cylinder or +size or +sizeM or +sizeK ([255]-287): 287
```

We can use the rest of the disk space for swap space, even though it's over the 64 megabytes I want for 32 megabytes of RAM. The amount required varies from system to system. Some applications don't need all that swap space, but if you're using many applications with little memory, swap space can make your performance a little better.

We'll print out the partition table again to see that the new partition, /dev/hda4, has been created. Here's what it looks like:

```
Command (m for help): p

Disk /dev/hda: 128 heads, 63 sectors, 525 cylinders
Units = cylinders of 8064 * 512 bytes

Device   Boot    Begin     Start       End     Blocks    Id    System
/dev/hda1             1         1       127      512032+  83    Linux native
/dev/hda2           128       128       254      512064   83    Linux native
/dev/hda3           288       288       525      959616   83    Linux native
/dev/hda4           255       255       287      133056   83    Linux native
```

The new partition is there, but it defaults to Linux native if it's not already formatted for another operating system besides Linux. So, we'll have to go into the partition table and change the type of file it is.

```
Command (m for help): t
Partition number (1-4): 4
Hex code (type L to list codes): 82
Changed system type of partition 4 to 82 (Linux swap)
```

The `t` command in `fdisk` tells Linux you want to redefine the new partition. The code, in hexadecimal notation, is `82`. This changes the partition to `swap`.

```
Command (m for help): p

Disk /dev/hda: 128 heads, 63 sectors, 525 cylinders
Units = cylinders of 8064 * 512 bytes

Device    Boot    Begin     Start     End     Blocks  Id  System
/dev/hda1        1         127      512032+   83  Linux native
/dev/hda2       128       128      254      512064   83  Linux native
/dev/hda3       288       288      525      959616   83  Linux native
/dev/hda4       288       288      525      959616   82  Linux swap
```

From here, you can see that the swap space has been defined. Save the partition table.

```
Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.

WARNING: If you have created or modified any DOS 6.x partitions, please see the fdisk manual page for additional information.
```

You can ignore the warning, as this is only the Linux part of the computer you are modifying.

Next, you'll want to add your partition to the `/etc/fstab` file. In my case, I add this line:

```
/dev/hda4        swap      swap       defaults 1 1
```

Then you want to make the swap space and turn it on. Do so by issuing the commands `mkswap` and `swapon`.

```
# mkswap /dev/hda4
# swapon -a
```

These commands activate the swap partition. If you ever want to deactivate it, issue the following command:

```
# swapoff -a
```

The `-a` option affects all the swap partitions in the `/etc/fstab` file.
