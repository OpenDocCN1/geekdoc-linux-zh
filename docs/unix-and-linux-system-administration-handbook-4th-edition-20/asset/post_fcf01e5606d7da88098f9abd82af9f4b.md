
## Chapter 8 Storage

You can put individual partitions under the control of a logical volume manager, but you can't partition a logical volume. Partitioning is the lowest possible level of disk management.

On Solaris, partitioning is required but essentially vestigial; ZFS hides it well enough you may not be aware that it's occurring. This section contains some general background information that may be useful to Solaris administrators, from a procedural standpoint, the Solaris path diverges sharply from that of Linux, HP-UX, and AIX. Skip may be broken out all your problems solved on page 264 for details. (Or don't: zpool create newdevice pretty much covers basis.)

Both partitions and logical volumes make backups easier, prevent users from poaching each disk's space, and contain potential damage of runaway programs. All systems have a root "partition" that includes / most of the host's configuration data. Everything needed to bring the system to single-user mode is part of the root partition. Various subdirectories (most commonly /var, /usr, /tmp, /share, and /home) may be broken out into their partitions or volumes. Most systems also have at least one swap area.

Opinions on the best way to divide up disks, as the defaults used by various systems. Here are some general points to guide you:

- A good idea to have a backup root device that you can boot to if something goes wrong with the normal root partition. Ideally, the backup root lives on a different disk from the normal root so that it can protect against hardware problems and corruption. However, even a backup root on the same disk has some value.⁹

- Since the root partition is often duplicated, it should also be so small that having two copies doesn't consume an unreasonable amount of disk space. The major reason that /usr is often a separate volume; it holds the bulk of the system's libraries and data.

- Putting /tmp on a separate filesystem limits temporary files to a finite size and saves you from having to back them up. Some systems use a memory-based filesystem to hold /tmp for performance reasons. The memory-based filesystems are still backed by swap space, so they work well in a broad range of situations.

⁹ Solaris and HP-UX even have "dynamic root disk" systems to facilitate the maintenance and use of multiple roots. See the man pages for beadm, lucreate for Solaris and drd for HP-UX.

## Traditional partitioning

- Since log files are kept in /var, it's a good idea for /var to be a separate disk partition. Leaving /var as part of a small root partition makes it easy to fill the root and bring the machine to a halt.

- It's useful to put users' home directories on a separate partition or even if the root partition is corrupted or destroyed, user data has a good chance of remaining intact. Conversely, the system can continue to operate after a user's misguided shell script fills up to /home.

- Splitting swap space among several physical disks increases performance. This technique works for filesystems, too; but the busy ones on different disks. See page 1129 for notes on this subject.

- As you add memory to your machine, you should also add swap space. See page 1124 for more information about virtual memory.

- Backups of a partition may be simplified if the entire partition can fit on one piece of media. See page 294.

- Try to cluster quickly-changing information on a few partitions that are backed up frequently.

## Traditional partitioning

Systems that allow partitions implement them by writing a "label" at the beginning of the disk to define the range of blocks included in each partition. The exact details vary; the label must coexist with other startup information (such as a boot block), and it often contains extra information such as a name or unique ID that identifies the disk as a wheel. Under Windows, the label is known as the MBR, or master boot record.

The device driver for representing the disk reads and uses the partition table to calculate the physical location of each partition. Typically, one or two devices represent each partition (one block device and one character device; Linux has only block devices). Also, a separate set of device files represents the disk.

Solaris calls partitions "slices", or more accurately, it calls them slices when they are implemented with a Solaris-style label and partitions that are implemented with a Windows-style MBR. Slice 2 includes the entire expanse of the disk, illustrating the rather truth that not one slice can claim a given disk. Perhaps the word "slices" was selected because "partition" gets a simple division, whereas slices overlap. The terms are otherwise interchangeable.

Despite the universal availability of logical volume managers, some situations still require or benefit from traditional partitioning.

- On PC hardware, the boot disk must have a partition table. Most systems require MBR partitioning (see Windows-style partitioning, next), but

![](img/579efec8c67772f31ecf34844bbb71a2_281_0.png)

## Chapter 8 Storage

Itanium systems require GPT partitions (page 235). Data disks may remain unpartitioned.

See page 85 for more information about dual booting with Windows.

- Installing a Windows-style MBR makes the disk incomprehensible to Windows, even if the contents of the individual partitions are not. If you want to operate with Windows (say, by dual booting), you'll need to install a Windows MBR. But even if you have no partitions along those lines, it may be helpful to consider the ubiquity of Windows and the likelihood that your disk will one day come in contact with it.

## Windows-style partitioning

The MS-DOS command that partitioned disks supports Windows-style partitions have adopted this name for their own partitioning commands, but there are many variations among fdisk. Windows itself has moved on: the command-line tool in recent versions is diskpart. Windows also has a partitioning GUI that's available through the Disk Management plug-in of mmc.

It does not matter whether you partition a disk with Windows or some other operating system. The end result is the same.

## GPT: GUID partition tables

Partitions that you create within the extended partition are called secondary partitions. They are proper subsets of the.

Keep the following rules of thumb in setting up Windows-partitioned disks. The first is an actual rule. The others exist only because certain BIOSes require them.

- There can be only one extended partition on a disk.
- The extended partition should be the last of primary partitions; no primary partitions should come after it.
- Some older operating systems don't be installed secondary partitions. To avoid trouble, stick to primary partitions for OS installations.

The Windows partitioning system lets only one partition marked "active". Boot loaders for the active partition try to load the operating system from it.

Each partition has a one-byte attribute that is supposed to indicate the partition's contents. Generally, the codes represent filesystem types or operating systems. These codes are not centrally assigned, but over time some conventions have evolved. They are summarized by Andries B. Brouwer at tinyurl.com/part-types.

Intel's extensible firmware interface (EFI) project aims to replace the rickety PC BIOSes with a more modern and functional architecture.¹ Although systems that use full EFI firmware are still uncommon, EFI's partitioning scheme has widespread support among operating systems. The main reason for this is that MBR does not support disks larger than 2TB in size. Since 2TB disks are already widely available, this problem becomes a matter of some urgency.

¹². Microsoft has recently introduced UEFI, a "unified" EFI effort supported by multiple vendors. However, EFI remains the more common term in general use. UEFI and EFI are essentially interchangeable.
