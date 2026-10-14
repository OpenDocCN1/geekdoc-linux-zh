that this field starts with a "1" in it, meaning that unless you change it, you'll end up with a 1 MB partition. Delete it using the {Backspace} key, and enter the desired partition size.

+   - **Growable?** — This check box indicates whether the size you entered in the previous field is to be considered the partition's exact size, or its minimum size. Press [Space] to check and uncheck the box. When checked, the partition will grow to fill all available space on the hard disk. In this case, the partition's size will expand and contract as other partitions are modified. Note that you can make more than one partition growable; if you do so, the additional free space will be shared between all growable partitions.

+   - **Type** — This field contains a list of different partition types. Select the appropriate partition type by using the [\uparrow] and [\downarrow] keys.

+   - **Allowable Drives** — This field contains a list of the hard disks installed on your system, with a check box for each. If a hard disk's box is checked, then this partition may be created on that hard disk. If the box is not checked, then the partition will never be created on that hard disk. By using different check box settings, you can direct Disk Druid to place partitions as you see fit, or let Disk Druid decide where partitions should go.

+   - **Ok** — Select this button and press [Space] when you are satisfied with the partition's settings, and wish to create it.

+   - **Cancel** — Select this button and press [Space] when you don't want to create the partition.

# Problems When Adding a Partition

**Please Note:** If you are having problems setting up your partitions, please refer to Appendix B for more information. If you attempt to add a partition and Disk Druid can't carry out your request, you'll see a dialog box like the one in Figure 5-14. In the box are listed any partitions that are currently unallocated, along with the reason they could not be allocated. Select the Ok button, and press [Space] to continue. Note that the unallocated partition(s) are also displayed on Disk Druid's main screen (though you may have to scroll the "Current Disk Partitions" section to see them).