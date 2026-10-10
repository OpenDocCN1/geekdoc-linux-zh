
The original ext filesystem had quite a few limitations, such as restraining files to only 2 GB in size. Not too long after Linux was first introduced, the ext filesystem was upgraded to create the second extended filesystem, called ext2.

The ext2 filesystem maintained the same ext filesystem structure but expanded its abilities:

- Created, modified, and last accessed time values for files were added to the inode table.
- The maximum file size allowed was increased to 2 TB, and then later to 32 TB.
- Disk blocks were allocated in groups when a file was saved.

The ext2 filesystem too had limitations. If something happened to the system between a file being stored and the inode table being updated, a potential result was losing the file's data location on the disk. The ext2 filesystem was notorious for experiencing these corruptions due to system crashes and power outages. And it wasn't long before developers were exploring a different avenue of Linux filesystems.

## Digging into journaling filesystems

Journaling filesystems provide a new level of safety to the Linux system. Instead of writing data directly to the storage device and then updating the inode table, journaling filesystems write file changes into a temporary file (called the journal) first. After data is successfully written to the storage device and the inode table, the journal entry is deleted.

If the system should crash or suffer a power outage before the data can be written to the storage device, the journaling filesystem reads through the journal file and processes any uncommitted data.

Linux commonly uses three different methods of journaling, each with different levels of protection. These are shown in Table 8-1.

### Table 8-1 Journaling Filesystem Methods

| Method | Description |
| :--- | :--- |
| Data mode | Both inode and file data are journaled. Low risk of losing data, but poor performance |
| Ordered mode | Only inode data is written to the journal, but not removed until file data is successfully written. Good compromise between performance and safety |
| Writeback mode | Only inode data is written to the journal; no control over when the file data is written. Higher risk of losing data but still better than not using journaling |

The data mode journaling method is by far the safest for protecting data, but it is also the slowest. All the data written to a storage device must be written twice, once to the journal and again to the actual storage device. This can cause poor performance, especially for systems that do lots of data writing.

Over the years, a few different journaling filesystems have appeared in Linux. The following sections briefly describe the popular Linux journaling filesystems available.

## Looking at the ext3 filesystem

The *ext3* filesystem is a descendant of ext2 that supports files up to 2 TB, with a total file system size of 32 TB. By default, it uses the ordered mode method of journaling, but the other modes are available via command-line options. It doesn't provide any recovery from accidental file deletion or allow data compression by default.

## Looking at the ext4 filesystem

A still popular descendant of ext3, the *ext4* filesystem supports files up to 16 tebibytes (TiB), with a total file system size of 1 exbibyte (EiB). By default, it uses the ordered mode method of journaling, but the other modes are available via command-line options. It supports encryption, compression, and unlimited subdirectories within a single directory. Old ext2 and ext3 filesystems can be mounted as if they were ext4 to improve their performance.

## Looking at the JFS filesystem

Possibly one of the oldest journaling filesystems around, the *Journaled File System (JFS)* was developed by IBM in 1990 for its AIX (Advanced Interactive Executive) flavor of Unix. However, it wasn't until its second version that it was ported to the Linux environment.

> **NOTE**
>
> The official IBM name of the second version of the JFS filesystem is JFS2, but most Linux systems refer to it as just JFS.

The JFS filesystem uses the ordered journaling method, storing only the inode table data in the journal and not removing it until the actual file data is written to the storage device.

## Looking at ReiserFS

In 2001, Hans Reiser created the first journaling filesystem for Linux, called *ReiserFS*, which provides features now found in both ext3 and ext4. Linux has dropped support for the most recent version, Reiser4.

## Looking at XFS

The *X File System (XFS)* was created by Silicon Graphics for their (now defunct) advanced graphical workstations. The filesystem provided some advanced high-performance features that make it still popular in Linux.

The XFS filesystem uses the writeback mode of journaling, which provides high performance but does introduce an amount of risk because the actual data isn't stored in the journal file.

## Understanding the volume-managing filesystems

With journaling, you must choose between safety and performance. Although data mode journaling provides the highest safety, performance suffers because both inode and data are journaled. With writeback mode journaling, performance is acceptable but safety is compromised.

For filesystems, an alternative to journaling is a technique called copy-on-write (COW). COW offers both safety and performance via snapshots. For modifying data, a clone or writable snapshot is used. Instead of writing modified data over current data, the modified data is put in a new filesystem location.

> **NOTE**
>
> A true COW system modifies the old data only when the data modification is completed. If old data is never overwritten, the proper term to call this action is a redirect-on-write (ROW). However, typically ROWs are simply called COWs.

Though disk sizes have grown significantly over the years, the need for more space is constant. Storage pools, which are created from one or more disks or disk partitions, provide the ability to create what appears to be a single disk, called a volume. Using these storage pools allows volumes to be grown as needed, providing flexibility and a lot less downtime.

Filesystems with COW, snapshot, and volume-management features are gaining in popularity. Two of the most popular, Btrfs and ZFS, are briefly reviewed in the following sections as well as a newcomer, Stratis.

## Looking at the ZFS filesystem

The ZFS filesystem was initially released in 2005 by Sun Microsystems for the OpenSolaris operating system. It began being ported to Linux in 2008 and was finally available for Linux production use in 2012.

ZFS is a stable filesystem that competes well against Reiser4, Btrfs, and ext4. It boasts data integrity verification along with automatic repair, provides a maximum file size of 16 exabytes, and has a 256 quadrillion Zettabytes maximum storage size. That's one large filesystem!

Unfortunately, its biggest detractor is that ZFS does not have a GNU General Public License (GPL) and thus cannot be included in the Linux kernel. Fortunately, most Linux distributions provide a way for it to be installed.

## Looking at the Btrfs filesystem

The *Btrfs* filesystem (typically pronounced *butter-fs*) is also called the B-tree filesystem. Oracle started development on Btrfs in 2007. It was based on many of Reiser4's features but offered improvements in reliability. Over time, additional developers joined in and helped Btrfs quickly rise toward the top of the popular filesystems list. This popularity is due to stability and ease of use, as well as the ability to dynamically resize a mounted filesystem.

While the openSUSE Linux distribution established Btrfs as its default filesystem, in 2017 Red Hat deprecated it, meaning that it would no longer support the filesystem (as of RHEL version 8 and beyond). Unfortunately, for those organizations who are married to RHEL, it means that Btrfs is not the filesystem of choice.

## Looking at the Stratis filesystem

When Red Hat deprecated Btrfs, the decision was made to create a new filesystem, *Stratis*. But you cannot accurately call Stratis a filesystem using the standard definition. Instead, it provides more of a management perspective. The storage pools it maintains are made up of one or more XFS filesystems. And it also offers COW functionality like the more traditional volume-management filesystems, such as ZFS and Btrfs. The terms “ease of use” and “advanced storage features” are often used to describe it, but at this point, it's too early to tell how close to those concepts Stratis performs.

> **NOTE**
>
> XFS in recent years has been improving its COW offerings. For example, it now has an always_cow mode.
