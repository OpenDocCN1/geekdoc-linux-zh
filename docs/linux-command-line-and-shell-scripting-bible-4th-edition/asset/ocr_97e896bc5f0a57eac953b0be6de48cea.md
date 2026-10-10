compromised.

For filesystems, an alternative to journaling is a technique called copy-on-write (COW). COW offers both safety and performance via snapshots. For modifying data, a clone or writable snapshot is used. Instead of writing modified data over current data, the modified data is put in a new filesystem location.

# NOTE

A true COW system modifies the old data only when the data modification is completed. If old data is never overwritten, the proper term to call this action is a redirect-on-write (ROW). However, typically ROWs are simply called COWs.

Though disk sizes have grown significantly over the years, the need for more space is constant. Storage pools, which are created from one or more disks or disk partitions, provide the ability to create what appears to be a single disk, called a volume. Using these storage pools allows volumes to be grown as needed, providing flexibility and a lot less downtime.

Filesystems with COW, snapshot, and volume-management features are gaining in popularity. Two of the most popular, Btrfs and ZFS, are briefly reviewed in the following sections as well as a newcomer, Stratis.

# Looking at the ZFS filesystem

The ZFS filesystem was initially released in 2005 by Sun Microsystems for the OpenSolaris operating system. It began being ported to Linux in 2008 and was finally available for Linux production use in 2012.

ZFS is a stable filesystem that competes well against Resier4, Btrfs, and ext4. It boasts data integrity verification along with automatic repair, provides a maximum file size of 16 exabytes, and has a 256 quadrillion Zettabytes maximum storage size. That's one large