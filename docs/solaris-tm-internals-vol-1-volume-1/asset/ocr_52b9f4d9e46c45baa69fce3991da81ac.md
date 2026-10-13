# Table 11-5  *File I/O System Calls*  *(Continued)*

| Function | Definition |
|---|---|
| `pwrite()` | Writes a fixed number of bytes to the given file descriptor, starting at the given offset from a byte array. |
| `read()` | Reads a fixed number of bytes from the given file descriptor into the given byte array |
| `readv()` | Equivalent to `read()` but places the input data into the buffers specified by the members of the supplied array of pointers. This is a way of initiating multiple reads from a single system call. |
| `select()` | From an array of file descriptors, selects the next file descriptor that has pending I/O. |
| `stat()` | Retrieves file attributes for the file corresponding to the given path name |
| `write()` | Writes a fixed number of bytes to the given file descriptor from the given byte array. |
| `writev()` | Equivalent to `write()` but writes data from the buffers specified by the members of the supplied array of pointers. Provides a way of initiating multiple write operations from a single system call. |

# 11.3.2  File Open Modes and File Descriptor Flags

The Solaris kernel maintains several file flags at different layers in the file code. Within the file structure, flags can be set when the file is opened (open(2) system call). Subsequent file operations using the fcntl(2) (file control) system call allow for setting and clearing file flags after the file has been opened. Some of these flags get pushed down to the file’s vnode, so that file manipulation at the vnode layer has the information available without referencing the file structure. Finally, some flags maintained in the inode are not exported to the process (application) level.

The system begins looking at file flags in the very early stages of opening a file. When the open system call is entered, the system checks to ensure that either the read or write flag is set, and the kernel looks at the O_NDELAY and O_NONBLOCK flags, which the programmer can set (see open(2)). O_NDELAY and O_NONBLOCK have the same meaning—they specify nonblocking I/O. Two flags exist because of evolving standards: the O_NDELAY flag emerged as a Unix SVR4 standard, and the O_NONBLOCK flag comes from the POSIX.1 specification. The Solaris environment supports both standards for compatibility. New applications should use the POSIX.1 standard (NONBLOCK), which is what the system chooses if both are set.

To see which flags are set, use the fcntl(2) system call with the F_GETFD flag, which retrieves the flags from the file descriptor.