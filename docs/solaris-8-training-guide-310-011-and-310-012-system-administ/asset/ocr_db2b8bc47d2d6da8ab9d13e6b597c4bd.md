# TABLE 21.10

# <SIZE> VALUES

| Value | Description |
|---|---|
| num | The size of the file system in MB. |
| existing | The current size of the existing file system. |
| auto | The size of the file system is determined automatically, depending on the selected software. |
| all | The specified slice uses the entire disk for the file system. When you specify this value, no other file systems can reside on the specified disk. |
| free | The remaining unused space on the disk is used for the file system. |
| <start>:<size> | The file system is explicitly partitioned. <start> is the cylinder where the slice begins, and <size> is the number of cylinders for the slice. |

file_system is an optional field when slice is specified as any or c?t?d?s?. If file_system is not specified, unnamed is set by default, but you can't specify the optional_parameters value.

The values listed in Table 21.11 can be used for file_system.

# TABLE 21.11

# FILE_SYSTEM VALUES

| Value | Description |
|---|---|
| <mount_pt_name> | The file system's mount point name, such as /opt. |
| <swap> | The specified slice is used as swap. |
| <overlap> | The specified slice is defined as a representation of the whole disk. overlap can be specified only when <size> is existing, all, or start:size. |
| <unnamed> | The specified slice is defined as a raw slice, so the slice does not have a mount point name. If file_system is not specified, unnamed is set by default. |
| <ignore> | The specified slice is not used or recognized by the Solaris installation program. This can be used to ignore a file system on a disk during an installation so that the Solaris installation program can create a new file system on the same disk with the same name. ignore can be used only when existing partitioning is specified. |