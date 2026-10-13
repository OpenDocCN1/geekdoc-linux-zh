This chapter covers the *Solaris Pseudo File Systems and Swap Space* test objectives. The first section describes the Solaris pseudo file systems and provides information on the more important pseudo file systems. The second section covers managing swap space.

# Solaris Pseudo File Systems

Solaris supports several types of memory-based file systems, referred to as *pseudo file systems*. Because they are memory based, these file systems provide faster access to data stored in them. However, they are not permanent. In addition, any directories or files in pseudo file systems are lost when the file system is unmounted or the system is rebooted/shut down. Table 16.1 describes the pseudo file systems supported by Solaris 8.

**Table 16.1  Solaris 8 Pseudo File Systems**

| Name | Abbreviation | Use |
|---|---|---|
| Cache File System | CacheFS | Local caching for slow (CD-ROM) or remote (NFS) file systems |
| File Descriptors File System | FDFS | Opening file using file descriptors with explicit names |
| First-In First-Out File System | FIFOS | Accessing data (named pipes) |
| Loopback File System | LOFS | Providing alternative paths to existing data |
| Name File System | NAMEFS | Dynamic mounting of file descriptors by STREAMS modules |
| Process File System | PROCFS | Accessing process status and information |
| Special Device File System | SPECFS | Accessing special character or block devices |
| Swap File System | SWAPFS | Accessing system swap space |
| Temporary File System | TMPFS | Providing fast access to temporary files |

Of these nine pseudo file systems, the following five do not require any administration: FDDS, FIFOS, NAMEFS, SPECFS, and SWAPFS. The other four pseudo file systems—CacheFS, LOFS, PROCFS, and TMPFS—are described in the following sections.