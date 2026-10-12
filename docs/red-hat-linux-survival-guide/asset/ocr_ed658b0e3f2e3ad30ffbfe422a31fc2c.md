![](bbox=[0.09, 0.12, 0.89, 0.37])

# Figure 1-9 Assigning mount points to partitions.

You can install Linux on only two partitions: / (root) and swap. But you should have at least / (root partition), /usr, and swap partitions for server type installation. Here I will assume that you will create four partitions. Therefore you need to create at least / and /usr mount points. Note that if you place the / partition, which is where /boot directory will be stored, in a partition with more than 1024 cylinders you might get a warning message, as shown in Figure 1-11.

![](bbox=[0.09, 0.61, 0.89, 0.88])

# Figure 1-10 Editing a mount point for a partition.