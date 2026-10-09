# ## Supported Foreign Filesystems

Here are some of the most commonly used foreign filesystems, along with a brief description of each and the appropriate mount command.

# ### FAT (MS-DOS)

FreeBSD includes extensive support for FAT, the DOS/Windows 9x File Allocation Table filesystem, commonly used on removable media and some dual-boot systems. This support covers the FAT12, FAT16, and FAT32 varieties. You *can* format a thumb drive with a non-FAT filesystem, however, so don’t blindly assume that all thumb drives use FAT. As the most common use for a thumb drive these days is transferring files between machines, however, most are FAT32. The mount type is *msdosfs* (mount -t msdosfs).

If you handle a lot of FAT32 disks, investigate the `mtools` package, a collection of programs for working with FAT filesystems that offer greater flexibility than the default FreeBSD tools.

# ### ISO 9660

ISO 9660 is the standard filesystem for CDs and is occasionally used on DVDs. FreeBSD supports reading and writing CDs if you have a CD burner. Just about every CD you encounter is formatted with *ISO 9660*. The mount command is `mount -t cd9660`.

The `cdrtools` package, in `/usr/ports/sysutils/cdrtools`, contains many helpful tools for working with CD images, including tools that build an ISO image from files on disk.

# ### UDF

UDF, or Universal Disk Format, is a replacement for *ISO 9660*. You’ll find UDF on some DVDs and Blu-Ray disks and on a few thumb drives larger than the 32GB supported under FAT32. As the capacity of removable media increases, you’ll see more and more UDF filesystems. The mount command is `mount -t udf`.