# Disk Druid's Buttons

These buttons control Disk Druid's actions. They are used to add and delete partitions, and to change partition attributes. In addition, there are buttons that are used to accept the changes you've made, or to exit Disk Druid entirely. Let's take a look at each button in order.

Add — The "Add" button is used to request a new partition. When selected, a dialog box will appear containing fields that must be filled in.

Edit — The "Edit" button is used to modify attributes of the partition currently highlighted in the "Current Disk Partitions" section. Selecting this button will cause a dialog box to appear. Some or all of the fields in the "Edit Partition" dialog box may be changed, depending on whether the partition information has already been written to the disk.

Delete — The "Delete" button is used to delete the partition currently highlighted in the "Current Disk Partitions" section. Selecting this button will cause a dialog box to appear asking you to confirm the deletion.

Ok — The "Ok" button causes any changes made to your system's partitions to be written to disk. You will be asked to confirm your changes before Disk Druid rewrites your hard disk partition table(s). In addition, any mount points you've defined are passed to the installation program, and will eventually be used by your Red Hat Linux system to define the filesystem layout.

Back — This button causes Disk Druid to abort without saving any changes you've made. When this button is selected, the installation program will take you back to the previous screen, so you can start over.

# Handy Function Keys

While there is some overlap between Disk Druid's buttons and the available functions keys, there are two function keys that have no corresponding buttons:

+   - **[F2] (Add NFS)** — This function key is used to add a read-only NFS-served filesystem to the set of mount points on your Red Hat Linux system. When selected, a dialog box will appear containing fields that must be filled in.
+   - **[F5] (Reset)** — This function key is used to discard all changes you may have made while in Disk Druid, and return the list of partitions to those read from the partition table(s) on your hard disk(s). When selected, you'll be asked to