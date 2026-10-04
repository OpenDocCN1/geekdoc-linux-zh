The following is an overview of the primary elements of a logical volume:

+   - **Concatenation and striping**
  Concatenations and stripes work much the way the UNIX cat(1) command program is used to concatenate two or more files to create one larger file. When partitions are concatenated, the addressing of the component blocks is done on the components sequentially. The file system can use the entire concatenation.

  Striping is similar to concatenation, except the addressing of the component blocks is interlaced on the slices rather than sequentially. Striping is used to gain performance. When data is striped across disks, multiple controllers can access data simultaneously.
- **Mirroring (mirrors and submirrors)**
  Mirroring replicates all writes to a single logical device (the mirror) and then to multiple devices (the submirrors), and distributes read operations. This provides redundancy of data in the event of a disk or hardware failure.
- **UFS logging (journaled file system)**
  UFS logging records UNIX file system (UFS) updates in a log (the logging device) before the updates are applied to the UNIX file system. With this technique, the risk of file system corruption due to a power failure or unsafe shutdown is greatly reduced.
- **Hot spare pools**
  A hot spare pool is a group of spare disk drives that automatically replace failed components.
- **Disksets**
  A diskset is an association of two hosts (servers) and a group of disk drives in which all of the drives are accessible by each host. If one host fails, the other takes over. This scenario is used where high availability is critical.
- **RAID devices**
  RAID is an acronym for "redundant arrays of inexpensive disks." Many disks are housed in a cabinet to provide large amounts of disk space.
- **Ability to expand mounted file systems**
  On a server requiring high availability, disk space can be added to a file system without shutting down the system or unmounting the file system.

Logical volumes can be made up of one or more component slices. You can configure the component slices of one disk or use slices from multiple disks. After you create the logical volumes, they are used like physical disk slices. Logical volumes provide increased capacity, higher availability, and better performance. To gain increased capacity, you create logical volumes that are concatenations, stripes, or RAID devices. Disk concatenations and