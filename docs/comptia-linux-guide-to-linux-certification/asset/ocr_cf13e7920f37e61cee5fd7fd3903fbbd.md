![](bbox=[0.17, 0.07, 0.82, 0.48])

partitions). To overcome this limitation, you can optionally label one of these primary partitions as “extended”; this extended partition can then contain an unlimited number of smaller parti-tions called logical drives. Each logical drive within the extended partition and all other primary partitions can contain a filesystem and be used to store data. The table of all partition informa-tion for a certain hard disk or SSD is stored in the first readable sector outside all partitions; it is called the Master Boot Record (MBR).

![](bbox=[0.16, 0.64, 0.33, 0.7])

The MBR is limited to hard disks that are less than 2TB in size. Newer hard disks and hard disks larger than 2TB use a GUID Partition Table (GPT) instead of an MBR. The MBR and GPT are functionally equivalent.

Recall that, in Linux, the first SATA/SCSI device in your system is referred to as sda, the first primary partition on this device is labeled sda1, the second sda2, and so on. Because there are only four primary partitions allowed, logical drives inside the extended partition are labeled sda5, sda6, and so on. An example of this partition strategy is listed in Table 2-3.

![](bbox=[0.16, 0.83, 0.33, 0.9])

For the primary master PATA hard disk device, simply replace sda with hda in Table 2-3.

Partitioning divides a hard disk into sections, each of which can contain a separate filesystem used to store data. Each of these filesystems can then be accessed by Linux if it is attached (or mounted) to a certain directory. When data is stored in that particular directory, it is physi-cally stored on the respective filesystem on the hard disk. The Fedora installation program