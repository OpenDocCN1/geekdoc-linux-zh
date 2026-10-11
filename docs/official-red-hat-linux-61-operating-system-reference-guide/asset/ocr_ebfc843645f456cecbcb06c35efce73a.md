+   Linux fdisk creates partitions of type Linux native by default. When you create a swap partition, don't forget to change it to type Linux swap using the t command. The value for the Linux swap type is 82. For other partition types, use the I command to see a list of partition types and values.

+   Linux allows up to four (4) partitions on one disk. If you wish to create more than that, one (and only one) of the four may be an extended partition, which acts as a container for one or more logical partitions. Since it acts as a container, the extended partition must be at least as large as the total size of all the logical partitions it is to contain.

+   It’s a good idea to write down which partitions (e.g., /dev/hda2) are meant for which file systems (e.g., /usr) as you create each one.

# Please Note

None of the changes you make take effect until you save them and exit fdisk using the w command. You can quit fdisk at any time without saving changes by using the q command.