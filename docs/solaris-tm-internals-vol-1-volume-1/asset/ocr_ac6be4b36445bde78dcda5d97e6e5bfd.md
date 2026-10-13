# The Solaris File I/O System

![](bbox=[0.119, 0.095, 0.869, 0.855])

read()  fwrite()  aioread()  write()  fread()  aiowrite()  mmap()

/dev/rdsk/\n/dev/rdsk/...

Stdio Libraries

Async IO Library

read / write

aio

Stack

Heap

Binary (Data)\nBinary (Text)

Application\nMemory\n(HEAP)

Special\nFile Sys.\n(specfs)

Regular File Systems\n(ufs, vxfs, pcfs etc)

Directory Structures

File System Blocks

seg_drv

NFS Server

Directory Name\nLookup Cache

Meta Data (Inode)\nCache

Old Buffer Cache\n(BUFHWM)

File Segment\ndriver (seg_map)

direct\nI/O

VNODE Segment\ndriver (seg_vn)

Paged VNODE VM Core\n(File System Cache & Page Cache)

Block I/O Interface

Volume Manager Layer - Disk Suite, VxVM

SCSI/Device Driver Framework

Data\nDisks

Swap Disk