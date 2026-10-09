![](bbox=[0.13, 0.09, 0.87, 0.4])

*Figure 3-17: ZFS disk selection*

Use the spacebar to select the disks you want to include in this pool. As this host has only one disk, I select it and then select OK to continue.

The installer returns me to the main ZFS configuration screen. I double-check my selections (GPT partitioning and 4GB swap) and then arrow up to select Install. The installer gives me a final “Are you really, really sure?” warning. I’m sure.

# Network and Service Configuration

Once you approve the disk layout, bsdinstall writes the new partition table to disk, creates filesystems, and extracts the distributions you’ve chosen without further intervention. The installer moves on to set up the network, services, and users.

First, you are prompted for the system’s new root password. The root user can do absolutely anything to the system, so make it a good password. You’ll have to enter it twice to have it accepted.

Arrow up and down to choose a network interface. This host has only a single interface, so I hit ENTER to configure it (see Figure 3-18).