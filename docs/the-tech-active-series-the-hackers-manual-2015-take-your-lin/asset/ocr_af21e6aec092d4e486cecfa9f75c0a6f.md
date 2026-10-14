# Advanced hacks

Tighten up swap space and indexing and streamline your kernel.

The tricks in the previous pages will help you get good traction out of your Linux distro with minimal effort. But if these don’t satiate your appetite for speed, lets move on to some advanced tweaks. However, before you apply these hacks, remember that not only are they more involved, but if applied carelessly they can have serious ramifications on your system setup.

Let’s start with a RAM disk, which is a memory-based filesystem that creates a storage area directly in your computer’s RAM as if it were a partition on a disk drive. The major benefit to this is that RAM disks are very fast. Since the data inside them is lost when you reboot the machine, a RAM disk is only suitable for apps which need repetitively small data areas for caching or using as temporary space.

Before creating a RAM disk use the free command to check the amount of unused RAM on your distro. Then create a folder to use as a mount point for your RAM disk with sudo mkdir /mnt/ramdisk and mount it with:

```
sudo mount -t tmpfs -o size=1024M tmpfs /mnt/ramdisk
```

This will create a 1GB RAM disk using the tmpfs file system designed specifically for creating RAM disks.

To make sure the RAM disk is mounted automatically whenever you boot into the distro, you’ll have to add it to the /etc/fstab file. Open it in a text editor and enter the following in a new line:

```
tmpfs /mnt/ramdisk tmpfs nodev,nosuid,noexec,nodiratime,size=2048M 0 0
```

Once you’ve created the RAM disk, you can use it to house your browser’s cache. If you use the Chromium browser, all you have to do is modify the launcher entry to point to the RAM disk with the appropriate switch such as --disk-cache-dir="/mnt/ramdisk".

If you use Firefox, type about:config in the location bar. Right-click somewhere in the list and select New > String. When asked for the name of the preference, type browser.cache.disk.parent_directory and then for its value type the path to where you want to store the cache, such as /mnt/ramdisk. Next locate the preference browser.cache.disk.enable and make sure it’s set to True, otherwise double-click on it to toggle it.

# Control swap usage

Wondering why your RAM-laden machine is still slow off the blocks? Chances are it’s because your distro is still using swap space on the hard disk, which has a slower read/write speed than RAM.

If your system has enough memory to handle whatever you throw at it, you should minimise the use of swap space. The swappiness parameter manages the ability of the kernel to shift processes out of physical memory and onto the swap disk, which can increase application response times when processes are moved out of memory vigorously.

The command cat /proc/sys/vm/swappiness will display the current level of swappiness set by your distro. Ubuntu’s default swappiness value is 60. The parameter will

![](bbox=[0.15, 0.55, 0.55, 0.78])

> Consider using a benchmarking tool such as the Phoronix Test Suite to gauge the performance of your rig regularly.

# Analyse and optimise boot up

We’ve already looked at the graphical tools that most distros bundle to help curtail unnecessary applications and services. Here we’ll look at ways to further optimise the boot using Systemd. This is a system management daemon that’s designed to replace the ageing init system. Like init, Systemd is a master daemon that manages other daemons.

Major desktop distributions, such as Fedora, Mageia, and OpenSUSE have already switched to the Systemd daemon while others like Debian and Ubuntu have announced plans to switch in forthcoming releases.

On a Systemd distro, you can measure boot times with the systemd-analyze command which will print the time taken to boot the kernel and load the services and the user space.

You can use systemd-analyze blame | head to get a list of the processes that take up most of the boot time and they are ordered by the time they took to initialise. The systemd-analyze plot > boot.svg command will visualise the entire boot process in the boot.svg image file. You can view this file in the browser to get an idea about the chains of processes.

Once you’ve identified a problematic service, you can mask the service. When you do this to a service, it cannot be started using Systemd, and in essence becomes invisible. If you don’t use LVM, RAID or any encrypted devices, you can mask nearly all Fedora storage services, such as sudo systemctl mask lvm2-monitor.service and sudo systemctl mask mdmonitor.service.

![](bbox=[0.75, 0.85, 0.9, 0.95])

> You can also manage Systemd services with the graphical Systemadm tool.