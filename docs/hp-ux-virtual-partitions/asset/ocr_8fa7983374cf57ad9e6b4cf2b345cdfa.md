Maximum: `"1"`
Default: `"0"`

Specify integer value.

# Description

In an `open()` or `fcntl()` call, the `O_SYNC` and `O_DSYNC` flags are used to ensure that data is properly written to disk before the call returns. If these flags are not set, the function returns as soon as the disk access request is initiated, and assumes that the write operation will be successfully completed by the system software and hardware.

Setting the `O_SYNC` or `O_DSYNC` flag prevents the function from returning to the calling process until the requested disk I/O operation is complete, thus ensuring that the data in the write operation has been successfully written on the disk. Both flags are equivalent in this regard except for one important difference: if `O_SYNC` is set, the function does not return until the disk operation is complete !land;! until all file attributes changed by the write operation (including access time, modification time, and status change time) are also written to the disk. Only then does it return to the calling process.

Setting `o_sync_is_o_dsync` to `"1"` allows the system to convert any `open()` or `fcntl()` calls containing an `O_SYNC` flag into the same call using the `O_DSYNC` flag instead. This means that the function returns to the calling process before the file attributes are updated on the disk, thus introducing the risk that this information might not be on the disk if a system failure occurs.

Setting this parameter to a non-zero value allows the function to return before file time-stamp attributes are updated, but still ensures that actual file data has been committed to disk before the calling process can continue. This is useful in installations that perform large volumes of disk I/O and require file data integrity, but which can gain some performance advantages by not forcing the updating of time stamps before proceeding. When the benefits of performance improvement exceeds the risks associated with having incorrect file-access timing information if a system or disk crash occurs, this parameter can be set to `"1"`. If that is not the case, it should remain set to its default value of zero.

The setting of this parameter does not affect disk I/O operations where `O_SYNC` is not used.