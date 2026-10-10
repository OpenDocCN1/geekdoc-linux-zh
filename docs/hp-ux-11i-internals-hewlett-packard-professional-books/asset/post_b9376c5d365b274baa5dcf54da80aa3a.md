
The key factor affecting the time to transfer data from one track to another is the seek time. Sometimes the data you are seeking is one track away, and sometimes it might be 1,000 tracks away. The average seek time is the time it takes to reposition the head across 1/2 of its total track count (250 in our example of 500 tracks).

The other factor affecting disk access time is *rotational latency*. Consider a rotating disk platter with a number of sectors located around each track. The sector you require might be the next to come under the head, or it might have just passed by, in which case you will have to wait for a complete revolution of the disk. As such, the average rotational latency is the time it takes for half a revolution of the disk media.

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_249_0.png)

## Figure 8-8 The HFS File System Layout

From a designer’s point of view, the only way to reduce the rotational latency is to get a faster disk (you may have noticed the trend from 5400 rpm disks to 10,000 rpm or higher in the PC market recently). The disadvantage of speeding up a drive is that the tolerances of the heads must be increased and that speed equals heat—the faster the drive spins, the more heat dissipation the hardware designer has to deal with. These two issues add up to increased cost. As far as the seek time is concerned, the trend is to increase the number of tracks, not decrease them, as hardware designers are constantly trying to increase the capacity of their drives.

This is where the file system designer chose to implement a “soft” solution to the challenge. By dividing the disk into multiple cylinder groups and allocating inodes and their related data blocks within a cylinder group whenever possible, the average seek time may be greatly improved. Each cylinder group contains a portion of the inode table, a redundant copy of the superblock (the `fsck` utility can use one of these copies to recover a corrupted superblock), and localized metadata to manage and monitor utilization of the local cylinder group space.

Reconsider our example; assume that the whole disk was divided into 100 cylinder groups. Each cylinder group (CG) would be mapped to 10 adjacent tracks. While the rotational latency would be constant, all the individual blocks containing a file's data would be located within a 10-track area. For access to this single file, the average seek time would be reduced from the time to move 500 tracks to the time to move 5 tracks! Simply by following these conventions for the placement of a file's data, we could see a vast improvement in access time. We realize that this is an over-simplified explanation, but it points our thinking in the right direction.

## Direct and Indirect Block Pointers

You may be wondering how a fixed-size inode can point to all the data blocks of files of varying sizes. If the block size is fixed and the inode size is fixed, it seems that there would be an implied maximum file size. To work around this issue, the HFS inode employs four types of block pointers:

-   Direct pointers (12 per inode)
-   Single indirect pointers (one per inode)
-   Double indirect pointers (one per inode)
-   Triple indirect pointers (one per inode)

The original AT&T file system had a 512-byte block, and the inode was 128 bytes and had room for 15 block pointers (each pointer was 32 bits). Let's examine the limits of this model (Figure 8-9).

There are 12 direct pointers that locate the first 12 blocks containing file data, allowing for 12 * 512, or 6 KB of storage. If the file grew beyond this size, then the 13th pointer (the single indirect pointer) was used to point to a data block that could hold additional direct pointers (a block size of 512 meant that an indirect block would hold an additional 128 pointers). The 14th pointer (the double indirect) could point to a block containing additional single indirect pointers, and the 15th pointer (the triple indirect) could point to a block containing additional double indirect pointers. In this manner, a fixed-size inode could map a very large number of file data blocks.

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_251_0.png)

For a file system with 8K byte blocks, the maximum file size would be:

| Pointer Type | Calculation | Result |
| :--- | :--- | :--- |
| 12 Direct Pointers | 12 x 8K | 96 KBytes |
| + Single Indirect | 2K x 8K | 16 MBytes |
| + Double Indirect | 2K x 2K x 8K | 32 GBytes |
| + Triple Indirect | 2K x 2K x 2K x 8K | 64 TBytes |

## Figure 8-9 The Inode

With the original 512-byte block size, we get the following capabilities:
-   Direct pointers → 12 × 512 = 6 KB
-   Single indirect → 128 × 512 = 64 KB
-   Double indirect → 128 × 128 × 512 = 8 MB
-   Triple indirect → 128 × 128 × 128 × 512 = 2 GB

With the more modern 8-KB block size, we get the following:
-   Direct pointers → 12 × 8 KB = 96 KB
-   Single indirect → 2 KB × 8 KB = 16 MB
-   Double indirect → 2 KB × 2 KB × 8 KB = 32 GB
-   Triple indirect → 2 KB × 2 KB × 2 KB × 8 KB = 64 TB

## The HFS inode

The inode is the end-all, be-all metadata structure when it comes to defining a file. All the attributes of a file—all permissions, type, size, credentials, timestamps, linkage counts, and data block pointers—are held in this structure. The only attribute of the file that isn’t held in the inode is its name! In actuality, a name is an abstraction used to locate a specific file’s data and exists to make it easier for humans to reference a file.

By maintaining this degree of separation between a file's attributes (its inode data) and its name (directory entry), it is a simple task to create multiple file names pointing to the same inode. This is the basis for the creation of hard links (referenced by the `ln` command).

To study the structure of a HFS inode, let's examine the `icommon` structure in the HP-UX kernel (Listing 8.1).

## Listing 8.1 `icommon` struct fields

```c
inode type (upper 4 bits) and access mode (lower 12 bits)
   0 0 2 0 u_short ic_mode

   0x1000 IFIFO       FIFO or named pipe
   0x4000 IFDIR       Directory
   0x6000 IFBLK       Block special file
   0x7000 IFCONT      Continuation inode
   0x8000 IFREG       Regular file
   0x9000 IFNWK       Network special file (retired)
   0xA000 IFLNK       Symbolic Link
   0xC000 IFSOCK      Socket

   current number of directory links (hard links) to this inode,
   2 0 2 0 short ic_nlink
   low 16 bits of the owner's UID and GID
   4 0 2 0 u_short ic_uid_lsb
   6 0 2 0 u_short ic_gid_lsb
   file size in bytes
   8 0 8 0 long ic_size
   timestamps (access, inode modification, and creation)

   Note: the modification timestamp refers to the last time the
   contents of the inode were modified and does not necessarily
   mean that the file's contents were changed

   16 0 4 0 u_int ic_atime.tv_sec
   20 0 4 0 u_int ic_atime.tv_usec
   24 0 4 0 u_int ic_mtime.tv_sec
   28 0 4 0 u_int ic_mtime.tv_usec
   32 0 4 0 u_int ic_ctime.tv_sec
   36 0 4 0 u_int ic_ctime.tv_usec
   next are the 12 direct block pointers
   40 0 4 0 int ic_un2.ic_reg.ic_db[0]
   44 0 4 0 int ic_un2.ic_reg.ic_db[1]
   48 0 4 0 int ic_un2.ic_reg.ic_db[2]
   52 0 4 0 int ic_un2.ic_reg.ic_db[3]
   56 0 4 0 int ic_un2.ic_reg.ic_db[4]
   60 0 4 0 int ic_un2.ic_reg.ic_db[5]
   64 0 4 0 int ic_un2.ic_reg.ic_db[6]
   68 0 4 0 int ic_un2.ic_reg.ic_db[7]
   72 0 4 0 int ic_un2.ic_reg.ic_db[8]
   76 0 4 0 int ic_un2.ic_reg.ic_db[9]
   80 0 4 0 int ic_un2.ic_reg.ic_db[10]
   84 0 4 0 int ic_un2.ic_reg.ic_db[11]
   followed by the single indirect, double indirect, and triple 
   indirect block pointers  
   88 0 4 0 int ic_un2.ic_reg.ic_un.ic_ib[0]  
   92 0 4 0 int ic_un2.ic_reg.ic_un.ic_ib[1]  
   96 0 4 0 int ic_un2.ic_reg.ic_un.ic_ib[2]

   If this is a fast symbolic link, the block pointers are replaced with  
   40 0 60 0 char[60] ic_un2.ic_gsymlink  
   A fast symbolic link allows the symbolic or “soft link” pathname to be stored in the inode  
   instead of a data block. This is possible as long as the linkage path doesn't exceed 59  
   characters in length.

   the status flags  
   100 0 4 0 int ic_flags  
   0x01 IC_FASTLINK enable fast symbolic links  
   0x02 IC_LARGEUIDS enable use of large UIDs

   blocks held  
   104 0 4 0 int ic_blocks  
   108 0 4 0 int ic_gen  
   upper 16 bits of the owner's UID and GID if large UIDs have  
   been enabled  
   112 0 2 0 u_short ic_uid_msb  
   114 0 2 0 u_short ic_gid_msb  
   116 0 4 0 int ic_spare[0]  
   120 0 4 0 int ic_spare[1]  
   continuation inode number (if needed)  
   124 0 4 0 u_int ic_contin
```

As we see from this listing, the size of the HFS inode is 128 bytes. If access control lists (ACLs) are being used, the last four bytes in an inode point to a *continuation* inode, which holds up to 13 additional access control settings. For more on ACLs, reference the manual pages on `chacl` and `lsacl`.

## Following Metadata Using fsdb

Another useful tool for studying the internals of file systems is *fsdb*. It is similar to the classic *adb* debugging utility except that it is designed to allow the root user to examine disk-resident metadata structures. To reinforce the information about HFS inodes and the basic organization of file system metadata, we use *fsdb* to examine an HFS file system mounted on `/dev/vg00/lvol10` (Listing 8.2). The file system's mount point is `/chriss`, and it has a data file stored under it named `/chriss/stuff` containing the following three lines of text:
