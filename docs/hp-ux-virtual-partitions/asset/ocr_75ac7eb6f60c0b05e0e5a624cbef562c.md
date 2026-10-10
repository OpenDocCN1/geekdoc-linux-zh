current directory, use the command:

```
`df -g`
```

# EXAMPLE ONE

A software development environment typically consists of small or medium sized I/Os with a fair number of disk seeks. Therefore, `\"hfs_max_ra_blocks\"` should be set to 8-to-16 blocks and `\"hfs_ra_per_disk\"` should be set to 32-to-64 kilobytes.

# EXAMPLE TWO

An out-of-core solver for an MCAE application has a significant sequential I/O component, so `\"hfs_max_ra_blocks\"` should be set to 64-to-128 blocks and `\"hfs_ra_per_disk\"` to 128-to-256 kilobytes.

# hfs_ra_per_disk

Set the amount of HFS filesystem read-ahead per disk drive, in Kbytes.

Acceptable Values:

+   Minimum: \`\"0\"\`
+   Maximum: \`\"8192\"\`
+   Default: \`\"64\"\`

Specify an integer value or use an integer formula expression.

# Description

When data is read from a disk drive, the system may read additional data beyond that requested by the operation. This \`\"read-ahead\"\` speeds up sequential disk accesses, by anticipating that additional data will be read, and having it available in system buffers before it is requested.
This parameter specifies the amount of read-ahead permitted per disk drive.

The total amount of read-ahead is determined by multiplying \`\"hfs_ra_per_disk\"\` by the number of drives in the logical volume.
If the filesystem does not reside in a logical volume, then the number of drives is effectively one.

# hfs_revra_blocks

This parameter sets the maximum blocks read with each HFS reverse read-ahead operation.