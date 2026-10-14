
## Adding an NFS Mount

To add a read-only NFS-served filesystem, press [F2]. If you have not selected a network-related installation method, you will be presented with several dialog boxes concerning network configuration (turn to Network Driver Configuration for more information). Fill in the boxes appropriately. You will then see a dialog box entitled, "Edit Network Mount Point" (similar to the one in Figure 5-19). In this dialog box you will need to enter the NFS server name, the path to the exported filesystem, and the mount point for the filesystem. Select the Ok or Cancel button as appropriate, and press [Space].

## Starting Over

If you'd like to abandon any changes you've made while in Disk Druid, and would rather use fdisk instead, you can select the Back button, and press [Space]. If you want to continue using Disk Druid, but would like to start over, press [F5], and Disk Druid will be reset to its initial state.

## When You're Finished...

Once you've finished configuring partitions and entering mount points, your screen should look something like the one in Figure 5-15. Select Ok, and press [Space]. Then turn to Initializing Swap Space.

![](img/46f4935125ba89e12897afbe9d77a097_124_0.png)

## Figure 5-15: Partitions and Mount Points Defined

## Using fdisk

If you'd rather use fdisk to manage partitions, this is the section for you. Once you've selected fdisk, you'll be presented with a dialog box entitled "Partition Disks" (see Figure 5-16). In this box is a list of every disk on your computer. Move the highlight to the disk you'd like to partition, select Edit, and press [Space]. You will then enter fdisk and can partition the disk you selected. Repeat this process for each disk you want to partition. When you're done, select "Done."

## Figure 5-16: Selecting a Disk for Partitioning

## An Overview of fdisk

fdisk includes online help which is terse but useful. Here are a few tips:

- The command for help is m.
- To list the current partition table, use the p command (see Figure 5-17).
- To add a new partition, use n.
- Linux fdisk creates partitions of type Linux native by default. When you create a swap partition, don't forget to change it to type Linux swap using the t command. The value for the Linux swap type is 82. For other partition types, use the l command to see a list of partition types and values.
- Linux allows up to four (4) partitions on one disk. If you wish to create more than that, one (and only one) of the four may be an extended partition, which acts as a container for one or more logical partitions. Since it acts as a container, the extended partition must be at least as large as the total size of all the logical partitions it is to contain.
- It's a good idea to write down which partitions (e.g., /dev/hda2) are meant for which filesystems (e.g., /usr) as you create each one.
- Please Note: None of the changes you make take effect until you save them and exit fdisk using the w command. You may quit fdisk at any time without saving changes by using the q command.

![](img/46f4935125ba89e12897afbe9d77a097_126_0.png)

## Changing the Partition Table

When you are finished partitioning your disks, press Done; you may see a message indicating that the installation program needs to reboot. This is a normal occurrence after changing a disk's partition data; it usually happens if you created, changed, or deleted any extended partitions. After you press Ok, your machine will reboot. Follow the same installation steps you did up until Partitioning Disks; then simply choose Done.

## Filesystem Configuration

The next dialog box contains a list of all disk partitions with filesystems readable by Red Hat Linux, including partitions for MS-DOS or Windows. This gives you the opportunity to assign these partitions to different parts of your Red Hat Linux filesystem. The partitions you assign will be automatically mounted when your Red Hat Linux system boots. Select the partition you wish to assign and press [Enter] (or choose Edit); then enter the mount point for that partition, e.g., /usr (see Figure 5-18).

![](img/46f4935125ba89e12897afbe9d77a097_127_0.png)

## Figure 5-18: Filesystem Configuration

If you are performing an upgrade, the installation program tries to find your root partition automatically; if it does, it obtains all this information automatically, and goes on to the next step.

## Adding an NFS Mount

Red Hat Linux also allows you to mount read-only NFS volumes when your system boots; this allows directory trees to be shared across a network. To do so, press [F2]. If you have not selected a network-related
