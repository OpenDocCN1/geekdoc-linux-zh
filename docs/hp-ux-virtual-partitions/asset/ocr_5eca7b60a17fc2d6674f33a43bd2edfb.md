This parameter was initially created to allow clients in an NFS cluster to use disk space on the server for swap. NFS clusters are no longer supported on HP-UX systems, and this parameter is set to zero by default (remote NFS swap not allowed). Setting this parameter to allow remote NFS swap is not very useful unless the system where it is allowed has extremely fast NFS capabilities.

# scsi_maxphys

Set the maximum record size for the SCSI I/O subsystem, in bytes.

Acceptable Values:

+   * Minimum: `1048576 (1 MB)`
+   * Maximum: `16777215 (16MB - 1)`
+   * Default: `1048576 (1 MB)`

Specify integer value.

Description

This parameter is used in conjunction with `*st_large_recs*` to enable large tape record support without logical record breakup and recombination.

# scsi_max_qdepth

Set the maximum number of SCSI commands queued up for SCSI devices.

Acceptable Values:

+   * Minimum: `1`
+   * Maximum: `255`
+   * Default: `8`

Specify integer value.

Description

For devices that support a queue depth greater than the system default, this parameter controls how many I/Os the driver will attempt to queue to the device at any one time. Valid values are (1-255). Some disk devices will not support the maximum queue depth settable by this command. Setting the queue depth in software to a value larger than the disk can handle will result in I/Os being held off once a QUEUE FULL condition exists on the disk.