# TABLE 3-2 **Mount Point Locations**

| Location | Description |
| :--- | :--- |
| `/` | The root of the Linux virtual filesystem |
| `/boot` | The location of the Linux kernel used for booting the system |
| `/home` | User directories for storing personal files and individual application setting files |
| `/tmp` | Temporary files used by applications and the Linux system |
| `/usr` | A common location for multi-user application files |
| `/var` | The variable directory, commonly used for log files and spool files |
| `/srv` | A common location for files used by services running on the system |
| `/opt` | Optional package installation directory for third-party applications |
| `/usr/local` | A common alternative location for optional multi-user package installations |

![](bbox=[0.168, 0.417, 0.238, 0.489])

If you're using the manual partition method, don't forget to allocate a partition for the swap area, even if you already have lots of physical memory installed on your system. The Linux kernel uses the swap area as a temporary holding ground to move sleeping applications out of physical memory to make more room for running applications. The standard rule for this is to create as large of a swap area as you have physical memory. Thus, if you have 8GB of physical memory, create an 8GB partition and assign it as the swap area.

+   9. If you're erasing an existing partition, or creating a new one, select any advanced disk features to use, and then click OK.

Ubuntu provides the option for you to use the Logical Volume Manager (LVM) feature in Linux with your hard drive partitions. LVM provides a way for you to easily add more space to an existing directory at any time if needed, even if there's data already in the directory. You may also choose to encrypt the logical volume if you need to. The other option is to use the ZFS filesystem, which is a commercial filesystem recently released to the open source world.

+   10. Click Install Now to accept the proposed hard drive partition changes and continue with the installation.

Up until this point you can change your mind about the hard drive changes. However, after you click Install Now here you're committed to those changes and there's no going back!

+   11. Select your location, and then click Continue.

Because Ubuntu is in use worldwide, you'll need to manually select just where in the world you are located so Ubuntu can assign the correct time zone and locale settings.