# ## ACTIVITY 15-4
### Configuring RAID Level 5

**Before You Begin:**

1. On srvA, you logged in as root in the CLI.
2. The first terminal is displayed.
3. Enter cd /root to change to the root directory.

**Scenario:**

You allocated 3 GB memory on your system to store sensitive transaction details. You want to effectively use the space and build fault tolerance in the hard disk so that you can recover data if the hard disk crashes.

![](bbox=[0.07, 0.35, 0.16, 0.43])

*In a real life scenario, for RAID 5 to be implemented with fault tolerance, the logical partitions need to be created on separate disks. However, for demonstration purposes this activity is being done by defining logical partitions on the same disk.*

**What You Do**

+   1. Create three logical partitions in the hard disk.

**How You Do It**

+   a. Enter `fdisk /dev/sdb` to invoke the *fdisk* utility for the /dev/sdb device.
b. Enter `n` to create a new partition.
c. Press `Enter` to accept the default first cylinder size.
d. Enter `+1024M` to set the partition size.
e. Enter `t` to change the partition type.
f. Enter `7` to set the partition number.
g. At the *Hex code (type L to list codes):* prompt, enter `fd` to change the partition from type 83 (Linux partition) to type fd (Linux raid auto).
h. Create two logical partitions with size 1 GB each and type `fd`
i. Enter `w` to write the changes onto the partition table.
j. Enter `reboot` to reboot the system.
k. Enter `ourglobalcompany` as the passphrase for starting the httpd server.
l. Switch to the first terminal of the CLI and log in as `root`.