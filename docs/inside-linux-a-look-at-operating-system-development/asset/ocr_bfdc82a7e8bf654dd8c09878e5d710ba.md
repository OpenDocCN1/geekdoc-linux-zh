Each directory in the search path must be accessible to the process, i.e., the program need only reference specific directories or files within each directory in the search path. This capability is noted by execute bits which apply to the user, members of the group, or others. The permission conveyed by these execute (access) bits is distinct from the permission to read the contents of a directory conveyed by the read bits.

Once that parent directory’s inode is identified, the desired directory’s or file’s inode is found or created.

When files are created, they normally acquire the owner and group of the process which created them. But if they are created in a directory which has the SGID bit set, files acquire the group of the directory in which they are created. $^{11}$

The rest of the code in `sys_open` and `do_open` notes the inode and other information in a structure, and a pointer to that structure is placed in the file descriptor table.

# Other I/O calls

The file descriptor is used to index into a per-process set of structures that hold information about that file’s use as well as an indirect index into a system wide set of structures regarding that file.

It indexes into a per-process table which in turn leads to a element of a linked list of structures, one per open file on the system.

These structures are accessed through one level of indirection—the virtual file system mentioned above.

Once a file has been opened, the application program moves to the desired offset (using `lseek`) and reads or writes a stream of bytes. The system kernel imposes no structure on the file, e.g., lines or records. This allows (requires) the application to interpret the data as appropriate.

The file system dependent code will ensure that data blocks will be allocated (and so noted in the bitmap) and data will be written to the correct place on the disk. In a similar manner, that code will locate the correct data block for read operations.

> $^{11}$I’ll leave it to others to determine if giving different meanings to the execute and SGID bits is good practice or not.