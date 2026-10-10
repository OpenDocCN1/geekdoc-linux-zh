filesystem!

Unfortunately, its biggest detractor is that ZFS does not have a GNU General Public License (GPL) and thus cannot be included in the Linux kernel. Fortunately, most Linux distributions provide a way for it to be installed.

# Looking at the Btrfs filesystem

The *Btrfs* filesystem (typically pronounced *butter-fs*) is also called the B-tree filesystem. Oracle started development on Btrfs in 2007. It was based on many of Reiser4's features but offered improvements in reliability. Over time, additional developers joined in and helped Btrfs quickly rise toward the top of the popular filesystems list. This popularity is due to stability and ease of use, as well as the ability to dynamically resize a mounted filesystem.

While the openSUSE Linux distribution established Btrfs as its default filesystem, in 2017 Red Hat deprecated it, meaning that it would no longer support the filesystem (as of RHEL version 8 and beyond). Unfortunately, for those organizations who are married to RHEL, it means that Btrfs is not the filesystem of choice.

# Looking at the Stratis filesystem

When Red Hat deprecated Btrfs, the decision was made to create a new filesystem, *Stratis*. But you cannot accurately call Stratis a filesystem using the standard definition. Instead, it provides more of a management perspective. The storage pools it maintains are made up of one or more XFS filesystems. And it also offers COW functionality like the more traditional volume-management filesystems, such as ZFS and Btrfs. The terms “ease of use” and “advanced storage features” are often used to describe it, but at this point, it's too early to tell how close to those concepts Stratis performs.

# NOTE

**XFS in recent years has been improving its COW offerings. For example, it now has an always_cow mode,**