Enter the device name of the cluster root partition []: dsk6a
Checking the cluster root partition: dsk6a

You entered 'dsk6a' as the device name of the cluster root partition.
Is this correct? [yes]: <Enter>

The cluster usr partition is the disk partition (for example, dsk6g) that will contain the clusterwide usr (/usr) file system.

Note: The default 'g' partition on most disks is usually large enough to hold the clusterwide usr AdvFS domain.

Enter the device name of the cluster usr partition []: dsk6g
Checking the cluster usr partition: dsk6g

You entered 'dsk6g' as the device name of the cluster usr partition.
Is this correct? [yes]: <Enter>

The cluster var device is the disk partition (for example, dsk6h) that will hold the clusterwide var (/var) file system.

Note: The default 'h' partition on most disks is usually large enough to hold the clusterwide var AdvFS domain.

Enter the device name of the cluster var partition []: dsk6h
Checking the cluster var partition: dsk6h

You entered 'dsk6h' as the device name of the cluster var partition.
Is this correct? [yes]: <Enter>

# 10.4.1.4 Enter the Quorum Disk

In planning this cluster, we set aside a quorum disk as we plan to have an even number of members in the cluster. In this section, we are prompted for the name of the quorum disk that was set aside.

Do you want to define a quorum disk device at this time? [yes]: <Enter>
The quorum disk device is the name of the disk (for example, dsk5) that will be used as this cluster's quorum disk.

Enter the device name of the quorum disk []: dsk5
Checking the quorum disk device: dsk5
The device you have selected for the quorum disk must be re-labeled with new cxn partition data. Performing this operation may cause data contained on this device to be destroyed.

Do you want to use this device anyway? [yes]: <Enter>