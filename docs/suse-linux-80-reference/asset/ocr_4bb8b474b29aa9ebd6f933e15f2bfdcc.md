+   2. *Another possibility, but not always feasible:* Install LILO to the MBR and pretend that it is DOS (as described in the above example). This method apparently no longer works for newer NT versions, as it only seems to start if it detects special (undocumented) sequences in the MBR, which are unfortunately, not recognized by LILO.

> **Caution**
> 
> NT 3.5x and 4.0 do not recognize Linux partition types 82 and 83. Be sure that no NT program tries to “repair” your partition table. This would result in loss of data. Always have valid backups of the LILO boot sector available.

# OS/2 and Linux

+   1. *Option:* Use the OS/2 boot manager for booting. It launches unlimited primary and logical partitions within the 1024-cylinder limit. The user is responsible to check those partitions can really be started. This boot manager is configured by OS/2’s fdisk.

*Preparation on the Linux side:* use LILO to make a primary partition bootable (usually the root partition).

However, first you should consider the following:

*Preparation on the OS/2 side:* OS/2 not only writes the conventional and obvious entries for existing partitions in the MBRs of hard disks and the partitioning sectors of extended and logical partitions, but also uses free space left in these sectors for additional information. If these are inconsistent, OS/2’s fdisk considers these partitions faulty and refuses to provide boot manager services. The fdisk commands of other systems do not use that extra information and do not know how to deal with it. Conflicts are inevitable.

Therefore, *before* installing Linux, load OS/2 (the installation system is sufficient) and create the Linux partitions (at least the logical partitions) with OS/2’s fdisk. This initially creates additional OS/2 partitions, which might get in the way.

*Solution:* immediately after creating the partitions, load the Linux installation system (or the rescue system from the SuSE Linux CD) and change the partition types to 83 (Linux native) using Linux fdisk. Now these partitions will be ignored by OS/2.