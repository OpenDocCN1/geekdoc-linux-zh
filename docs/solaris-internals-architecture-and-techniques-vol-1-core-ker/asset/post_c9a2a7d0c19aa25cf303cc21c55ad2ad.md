
# Files in Solaris

```bash
# crash
dumpfile = /dev/mem, namelist = /dev/ksym, outfile = stdout
> file
```

| ADDRESS | RCNT | TYPE/ADDR | OFFSET | FLAGS |
|---|---|---|---|---|
| 300009e008 | 1 | FIFO/3000902e7 | | read write |
| 300009e040 | 1 | UFS/3000117dc68 | 535 | write appen |
| 300009e078 | 1 | SPEC/3000e8d698 | 3216 | write appen |
| 300009e0b0 | 1 | UFS/30001d8c98 | | read write |
| 300009eb0 | 1 | UFS/3000bf45a0 | | read write |
| 300009e120 | 1 | /dev/30009229a8 | | read write |
| 300009e158 | 1 | UFS/3000f4c3c8 | | read |
| 300009e1c8 | 1 | UFS/300076a6c0 | 106 | read write |
| 300009e238 | 1 | /dev/30009229a8 | | write write |
| 300009e270 | 1 | SPEC/30008ecf18 | | read |
| 300009e2a8 | 1 | UFS/3000e5f0e0 | | read |
| 300009e3b4 | 1 | UFS/3000f1fd90 | | read |
| 300009e350 | 1 | FIFO/300090f2c0 | | read write |
```

The Address column is the kernel memory address of the file structure. RCNT is the reference count field (f_count). TYPE is the type of file, and ADDR is the current file pointer, of the vnode. FLAGS are the flags bits set for the file.

You can use sar(1M) for a quick look at how many files are opened systemwide.

```bash
# sar -v 3 3
SunOS devhome 5.7 Generic sun4u      08/01/99
11:38:09  proc-sz  ov  inode-sz      ov  file-sz  ov  lock-sz
11:38:12  100/5930  0  37181/37181  0  603/603  0  0/0
11:38:15  100/5930  0  37181/37181  0  603/603  0  0/0
11:38:18  101/5930  0  37181/37181  0  607/607  0  0/0
```

This example shows 603 opened files. The format of the sar output is a holdover from the early days of static tables, which is why it is displayed as 603/603. Originally, the value on the left represented the current number of occupied table slots, and the value on the right represented the maximum number of slots. Since file structure allocation is completely dynamic in nature, both values will always be the same.

For a specific process, you can use the pfiles(1) command to create a list of all the files opened.

```text
585: /space1/framemaker,v5.5.3/bin/sunxm.85:sparc/maker -xrm iconX:0 -xrm
Current limit: 64 file descriptors
0: S_IFCHR mode:0666 dev:22:ino:143523 uid:0 gid:3 rdev:13,2
  O_RDONLY|LARGEFILE
1: S_IFCHR mode:0666 dev:22:ino:143523 uid:0 gid:3 rdev:13,2
  O_WRONLY|APPEND|LARGEFILE
2: S_IFCHR mode:0666 dev:22:ino:143523 uid:0 gid:3 rdev:13,2
  O_WRONLY|APPEND|LARGEFILE
3: S_IFIFO mode:0666 dev:22:ino:413262568 uid:0 gid:0 size:0
  O_RDWR|NONBLOCK|FD_CLOEXEC
4: S_IFDOOR mode:0644 dev:32:176,0 ino:4127633624 uid:0 gid:0 size:0
  O_RDONLY|LARGEFILE|FD_CLOEXEC
5: S_IFREG mode:0644 dev:32:9 ino:1643 uid:19821 gid:10 size:29784
  O_RDWR|FD_CLOEXEC
6: S_IFREG mode:0644 dev:32:8 ino:566 uid:19821 gid:10 size:2696
7: S_IFREG mode:0644 dev:32:9 ino:612 uid:1921 gid:10 size:0
  O_RDWR|FD_CLOEXEC
8: S_IFREG mode:0644 dev:32:8 ino:666 uid:1921 gid:10 size:0
  O_RDWR|FD_CLOEXEC
9: S_IFCHR mode:0000 dev:32:24 ino:360 uid:0 gid:0 rdev:41,104
  O_RDWR|FD_CLOEXEC
10: S_IFREG mode:0644 dev:32:9 ino:38607 uid:1921 gid:10 size:65083
  O_RDONLY
11: S_IFREG mode:0644 dev:32:8 ino:667 uid:1921 gid:10 size:4096
  O_RDWR
```

In the preceding example, the pfiles command executed on PID 585. The PID and process name are dumped, followed by a listing of the process's opened files. For each file, we see a listing of the file descriptor (the number to the left of the colon), the file type, mode, the device from which the file was created, the inode number, file UID and gid, and the file size.

## Application Interfaces (APIs)

Different APIs perform I/O in Solaris. These include standard I/O—the generic buffered I/O mechanism—and low-level system calls. The traditional C interfaces are known as Standard I/O, abbreviated as stdio. The buffered I/O interfaces were added to Unix V6 by Bell Laboratories in 1976; they appear as a standard I/O mechanism in nearly all runtime environments. The stdio library exists as a layer above the lower-level system calls.

Of several different types of I/O, the most basic are the read and write system calls. The more advanced (and recent) are POSIX I/O through pread and write system calls and scatter/gather I/O through the read and write interfaces via ao_read(3) and ao_write(3) interfaces, which are part of the libaio library. Both sets of asynchronous I/O interfaces provide similar functionality; they differ in how they are used in application code.

Figure 11.2 shows the general relationships among the various file-related APIs and the underlying kernel subsystems.

![](img/a8637b95bf21add85c9948ac951c6_524.png)
**Figure 11.2 Kernel File I/O Interface Relationships

### 11.2.1 Standard I/O (stdio)

The standard I/O functions allow a file to be opened as a “stream” of bytes, known as a file stream. This approach allows a C program to access the file by reading and writing characters and arbitrary length strings, while the underlying libraries deal with the system calls necessary to implement the real I/O operations. This design has the advantage that it is completely portable, even across different operating systems, and the programmer does not need to consider any underlying machine-dependent characteristics, such as alignment with the file system block.

For example, a C program can read a file one at a time, and rather than reading from disk in 1-byte I/Os, the standard I/O library will buffer the I/O so that the file system and I/O subsystem can read in large efficient sizes. Standard I/O file buffering comes at the cost of additional processing overhead for each I/O.

The basic handle for a standard I/O file stream is the FILE handle, which is acquired by a call to open. Once a file handle is established, a suite of standard I/O routines is available to perform I/O on the handle.

The traditional Unix definition for a file handle defines the FILE structure in `<stdio.h>`, which is also true for Solaris versions up to including Solaris 2.6. Beginning with Solaris 7, the FILE structure is defined in stdio.h, a form of the standard I/O header. There are now different definitions for the FILE structure for 32-bit and 64-bit implementations.

```c
#ifdef _LP64
struct FILE_TAG {
  long pad[16];
};
#else
struct FILE_TAG { /* needs to be binary-compatible with old versions */
#ifdef STDIO_REVERSE
  unsigned char *ptr; /* next character from/to in buffer */
  size_t _cnt; /* number of available characters in buffer */
#else
  size_t _cnt; /* number of available characters in buffer */
  unsigned char *ptr; /* next character from/to in buffer */
  unsigned char base; /* the buffer */
  unsigned char flag; /* the state of the stream */
  unsigned char file; /* Unix System file descriptor */
  unsigned char orientation:2; /* the orientation of the stream */
  };
#endif /* _LP64 */
```

### Header File <stdio impl.h>

The members of the 32-bit FILE structure are defined as follows:

- cnt — Count of the number of characters in the buffer.
- ptr — Pointer to the current position in the buffer.
- base — Pointer to the buffer (a char).
- flag — Flag field that stores the state of the stream.
- file — The file descriptor itself is stored as an unsigned char.

