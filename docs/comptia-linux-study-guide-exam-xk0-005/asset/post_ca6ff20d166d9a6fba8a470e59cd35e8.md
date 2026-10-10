
## Listing 20.22: Displaying a swap partition with the swapon utility

```
$ swapon -s
Filename  Type      Size  Used  Priority
/dev/dm-1 partition  1769468 0  -2
$
```

Notice that on this Rocky Linux distro, the swap space is a partition. The priority column within the preceding example’s swap space statistics is shown as a negative 2 (−2). If there are multiple swap spaces, this priority number determines which swap is used first.

Another swapon -s example is enacted on an Ubuntu distribution and shown in Listing 20.23. Notice that in this case, the swap space is a file.

## Listing 20.23: Displaying a swap file with the swapon utility

```
$ swapon -s
Filename  Type      Size  Used  Priority
/swapfile  file      483800 0  -2
$
```

During the Linux OS installation, typically a swap partition or file is created and added to the /etc/fstab configuration file. However, you may need to create additional swap partitions/files—for example, if you increase your system’s RAM.

![](img/c0a399aca0d18f8822d714ad0a173123_662_0.png)

> If your swap partition is on a logical volume, add additional space via the LVM tools. Simply follow the steps covered in the section “Troubleshooting Storage Issues” earlier in this chapter as well as the following section. However, you can have more than one system swap space. In fact, in many cases it is desirable to do so for performance reasons.

For a new partition swap space, once you’ve created a new disk partition, use the mkswap command to “format” the partition into a swap partition. You use the same command for a new swap file and a logical volume. An example on a Rocky Linux system, using super user privileges, is shown in Listing 20.24.

## Listing 20.24: Making a swap partition with the mkswap command

```
# mkswap /dev/sde1
Setting up swap space version 1, size = 1048572 KiB
no label, UUID=e5bd150a-2f06-42ed-a0a9-a7372abd9dee
# # blkid /dev/sde1
/dev/sde1: UUID="e5bd150a-2f06-42ed-a0a9-a7372abd9dee" TYPE="swap"
#
```

Now that the swap partition or file has been properly prepared, activate it using the swapon command. The free command is very useful here because it provides a simple view of your current free and used memory. An example of these two commands is shown in Listing 20.25.

## Listing 20.25: Activating a swap partition with the swapon command

```
$ free -h
Mem:  3.7G  359M  3.0G  9.3M  352M  3.1G
Swap: 1.5G  0B  1.5G
#
# swapon /dev/sde1
#
# swapon -s
Filename  Type  Size Used  Priority
/dev/dm-1  partition 1572860 0  -1
/dev/sde1  partition 1048572 0  -2
#
# free -h
Mem:  3.7G  366M  3.0G  9.3M  352M  3.1G
Swap: 2.5G  0B  2.5G
#
```

You can see that the swap space size has increased 1 GB by adding a second swap partition. The -h option on the free command displays memory information in a more human-readable format.

> The free command’s buffer cache output is displayed in the buff/cache column. Older versions of this command would show two columns for this data—buffers and cache. Linux divides up its buffer cache into distinct categories. Buffers are memory used by kernel buffers, while cache is memory used by process page caches and slabs (contiguous memory pages set aside for individual caches). The buff/cache column in the modern free command’s output is simply a summation of these two memory use categories.

If desired, change the new swap partition's priority from its current negative 2 (-2) to a higher priority, using the swapon command, as shown in Listing 20.26. A higher number designates that the swap partition is used before other partitions for swap.

## Listing 20.26: Changing a swap priority with the swapon command

```
# swpoff /dev/sde1
# 
# swapon -p 0 /dev/sde1
#
# swapon -s
#
Filename	Type	Size	Used	Priority
/dev/dm-1	partition	1572860	0	-1
/dev/sde1	partition	1048572	0	0
#
```

You must first use the swpoff command on the swap partition to disengage it from swap space. After that, the swapon -p priority is used to change the preference priority. You can set priority to any number between 0 and 32767.

> **WARNING** If you want to move your system to a new swap partition or file, do not use the swpoff command on a current swap partition/file until your new swap partition is added to swap space. Otherwise, you may end up with a hung system.

If all is well with the new swap partition, add it to the /etc/fstab file so that it is persistent through system reboots. You can closely mimic the current swap file record’s settings, but be sure to change the name to your new swap partition/file.

## Running Out of Memory

By default, the Linux kernel allows itself to overcommit memory to various processes. This is done for efficiency and performance. However, due to this allowance, the system can become very low on free memory. In a critical low-memory situation, Linux first reclaims old memory pages. If it doesn’t reclaim enough RAM to come out of a critical status, it employs the *out-of-memory killer* (also called the OOM killer).

When triggered, the OOM killer scans through the various processes using memory and creates a score. The score is based on the total memory a process (and its child processes) is using and the smallest number of processes that can be killed to come out of a critical low-memory status. The kernel, root, and crucial system processes are automatically given low scores. If a process has a high score, it is killed off. The OOM killer scans and kills off high-scoring processes until the system is back to normal memory status.

![](img/c0a399aca0d18f8822d714ad0a173123_665_0.png)

If you want to modify the behavior of the OOM killer, you can do so via the following kernel parameters with the `sysctl` command:

`vm.panic_on_oom` and `kernel.panic`.

You can force the kernel to prevent memory overcommit via the `sysctl` command, changing the `vm.overcommit_memory` kernel parameter from its default of 0 to 1. However, this may not be the best solution. In many systems, it is better to fine-tune the memory overcommit by setting `vm.overcommit_memory` to 2. This allows you to allocate as much memory as defined in another kernel parameter, the `overcommit_ratio`. In this case, when a process requests memory that causes the system to exceed the set overcommit ratio, the allocation fails.

![](img/c0a399aca0d18f8822d714ad0a173123_665_1.png)

While you can modify kernel parameters with the `sysctl` command, the settings are not persistent. To make the settings persistent, make the appropriate edits to `/etc/sysctl.conf` or your distribution’s applicable `sysctl` configuration file.

## Surviving a Lost Root Password

Forgetting the root account’s password is troublesome for many reasons. The quick fix is to reset it via the `passwd` command using your own account’s super user privileges. However, if you were using the root account to gain super user privileges (which is a bad practice) or your privileges do not allow you to change the root password, you are in trouble. But all hope is not lost.

On older Linux distros and a few modern ones (Ubuntu), booting the system into single user mode will allow you to access the root account and change its password via the `passwd` command. To do so, follow these steps:

1. Boot (or reboot) the system. When the boot process reaches the boot menu, press the **E** key on the boot menu line you wish to edit (the kernel version the system typically runs).
2. Find the line that contains `linux` or `linux16` via an arrow key.
3. Go to the line’s end, press the spacebar once, and type **1**.
4. Press **Ctrl+X** to boot the system.
5. Once the system is booted, press the **Enter** key if it states you are in Emergency or Rescue mode.
6. Change the root account’s password using the `passwd` command.
7. Reboot the system using the `reboot` command.

On some modern Linux systems, such as Rocky Linux and Fedora distros, you’ll need a slightly different approach. Follow these steps:

1. Boot (or reboot) the system. When the boot process reaches the boot menu, press the **E** key on the boot menu line you wish to edit (the kernel version the system typically runs).
2. Find the line that contains `linux` or `linux16` via an arrow key.
3. On that line, find `ro`. This is somewhere in the line’s middle.
4. Replace `ro` with `rw init=/sysroot/bin/sh`. Don’t replace anything else in that line but `ro`.
5. Press Ctrl+X to boot the system.
6. Once the system is booted, press the Enter key if it states you are in Emergency or Rescue mode.
7. Type `chroot /sysroot` to set up a jailed root environment.
8. Change the root account’s password using the `passwd` command.
9. If the system uses SELinux (Rocky Linux and Fedora typically do), force SELinux to automatically relabel the system on the next boot by typing the `touch /.autorelabel` command.
10. Reboot the system with the `reboot` command. (Note: You may need to type `exit` and press Enter before trying to reboot your system.)

You’ll have to wait a while for the system to go through its SELinux relabel process.

## Summary

Troubleshooting Linux performance issues requires planning ahead for adverse incidents. In addition, you must understand the interactions between the various system properties, such as processors, disks, networks, and memory. Properly sizing system components and configuring Linux will provide a more trouble-free environment.

## Exam Essentials

Describe network troubleshooting tools. If your network is experiencing high latency, the tools to help troubleshoot this are iperf, iperf3, iftop, nr (netcat), ping, ping6, ss, tracepath, traceroute6, traceroute, and tracroute6. These utilities also assist in detecting network saturation problems. If failing or faulty adapters are a problem, the tools to diagnose this issue are ethtool, ifconfig, ip, and netstat. These utilities along with nmcli also help with NIC configuration problems. For incorrect or duplicate MAC
