A second major overhaul for UFS was at the time of SunOS 4.0, when the virtual memory system was redeveloped to use the vnode as the core of virtual memory operations. The new VM system implemented the concept of virtual file caching—a departure from the traditional physical file cache (known as the “buffer cache”) in previous versions of UNIX. The old buffer cache was layered under the file systems and clustering the physical blocks from the file system to the storage device. The new model is layered above the file systems and the VM system paging-sized pieces of files, where the file and a particular offset are cached as pages of memory. From this point, the buffer cache was used only for file system data, and the VM system implements file system caching. The new VM system affected the file systems in many ways and required significant changes to the vnode interface. At that point, UFS was substantially modified to provide support for the vnode and VM interfaces.

The third major change to UFS was in Solaris 2.4 in 1994, which saw the introduction of file system metadata logging to provide better reliability and faster reboots after a system crash or outage. The first versions of logging were introduced in Online: Disk Suite 3.0, the precursor to Solstice Suite (SDS). Solaris 7 saw the integration of logging into the base UFS.

Table 14-1 summarizes the major UFS development milestones.

# Table 14-1 Unix File System Evolution

| Year | SunOS Version | Annotations |
|---|---|--|
| 1984 | SunOS 1.0 | FFS from 4.2 BSD. |
| 1985 | SunOS 2.0 | UFS architected to support vnodes/vfs. |
| 1988 | SunOS 4.0 | UFS integrated with new VM virtual file cache. |
| 1991 | SunOS 4.1 | I/O clustering allowed to add extentlike performance. |
| 1992 | SunOS 4.1 | 1TB file system and ability to grow UFS systems with Online: Disk Suite 1.0. |
| 1992 | Solaris 2.0 | 1TB file system support included in base Solaris. |
| 1994 | Solaris 2.4 | Metadata logging option with Online: DiskSuite 3.0. |
| 1995 | Solaris 2.6 | Large file support allows 1TB files. Direct I/O uncached access added. |
| 1998 | Solaris 7 | Metadata logging integrated into base Solaris UFS. |