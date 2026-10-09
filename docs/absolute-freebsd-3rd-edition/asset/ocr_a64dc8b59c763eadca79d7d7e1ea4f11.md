Aliases to directories are always symlinks; you cannot use a hard link for those.

# # UFS Resiliency

UFS dates from the age when a power loss meant data loss. After decades of use and debugging, UFS almost never loses data, especially when compared with other open source filesystems. UFS achieves this resiliency by careful integrity checking, especially after an unexpected shutdown like a power failure.

The point of resiliency isn't to verify the data on disk—UFS is pretty good at that. It's to speed integrity verification and filesystem recovery after that unexpected shutdown. The size of modern disks means that verification can take a long time without additional resiliency. An integrity check of a 100MB filesystem is much faster than the same integrity check of a multiterabyte filesystem! Adding resiliency improves recovery times.

UFS offers several ways to improve the resilience of a UFS filesystem, such as soft updates and journaling. Before creating a filesystem, choose one that fits your needs.

# ## Soft Updates

*Soft updates* is a technology used to organize and arrange disk writes so that filesystem metadata remains consistent at all times, giving nearly the performance of an async mount with the reliability of a sync mount. That doesn't mean that all data will be safely written to disk—a power failure at the wrong moment can still lose data. The file being written to disk at the exact millisecond the power dies can't get to the disk no matter what the operating system does. But what's actually on the disk will be internally consistent. Soft updates lets UFS quickly recover from failure.

You can enable and disable soft updates when mounting or creating the filesystem.