# Handy Function Keys

While there is some overlap between Disk Druid's buttons and the available functions keys, there are two function keys that have no corresponding buttons:

+   - **[F2] (Add NFS)** — This function key is used to add a read-only NFS-served filesystem to the set of mount points on your Red Hat Linux system. When selected, a dialog box will appear containing fields that must be filled in.

+   - **[F5] (Reset)** — This function key is used to discard all changes you may have made while in Disk Druid, and return the list of partitions to those read from the partition table(s) on your hard disk(s). When selected, you'll be asked to confirm whether you want to discard the changes. Note that any mount points you've specified will be lost, and will need to be reentered.

**Please Note:** You will need to dedicate at least one partition to Red Hat Linux, and optionally more. This is discussed more completely in **Partition Naming Scheme.**

Now let's see how Disk Druid is used to set up partitions for your Red Hat Linux system.

# Adding a Partition

To Add a new partition, select the Add button, and press [Space] or [Enter]. A dialog box entitled "Edit New Partition" will appear (see Figure 4-6). It contains the following fields: