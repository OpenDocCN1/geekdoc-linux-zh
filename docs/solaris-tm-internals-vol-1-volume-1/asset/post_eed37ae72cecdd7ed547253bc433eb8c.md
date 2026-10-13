
```c
extern struct mod_ops mod_fsops;
static struct modfs modfs = {
        &mod_fsops,
        "vnode_file pseudo file system",
        &vfw
};

static struct modlinkage modlinkage = {
        MODREV_1,
        &modfs,
        NULL
};

int
_init(void)
{
        int     error;

        mutex_init(&vnfslock, NULL, MUTEX_DEFAULT, NULL);
        rw_init(&vnfsnodes_lock, NULL, RW_DEFAULT, NULL);
        error = mod_install(&modlinkage);
        if (error) {
                mutex_destroy(&vnfslock);
                rw_destroy(&vnfsnodes_lock);
        }
        myfs_init_otherstuff();
        return (error);
}

int
_fini(void)
{
        int     error;

        vnfs_vnlist_destroy();
        error = mod_remove(&modlinkage);
        if (error) {
                return (error);
        }
        mutex_destroy(&vnfslock);
        rw_destroy(&vnfsnodes_lock);
        return (0);
}

int
_info(struct modinfo *modinfop)
{
        return (mod_info(&modlinkage, modinfop));
}

static struct vfsw vfw = {
        "myfs",
        myfsinit,
        &myfs_vfsops,
        0
};

static int
myfsinit(struct vfsw *vswp, int fstyp)
{
        vswp->vfsw_vfsops = &myfs_vfsops;
        myfstype = fstyp;
        (void) myfs_init();
        return (0);
}
```

### 13.6 The File System Flush Daemon

The fsflush process writes modified pages to disk at regular intervals. The fsflush process scans through physical memory looking for dirty pages. When it finds one, it initiates a write (or putpage) operation on that page.

The fsflush process is launched by default every 5 seconds and looks for pages that have been modified (the modified bit is set in the page structure) more than 30 seconds ago. If a page has been modified, then a page-out is scheduled for that page, but without the free flag so the page remains in memory. The fsflush daemon flushes both data pages and inodes by default. Table 13-15 describes the parameters that affect the behavior of fsflush.

**Table 13-15 Parameters That Affect fsflush**

| Parameter | Description | Min | Solaris 2.7 Default |
| --- | --- | ---: | ---: |
| `tune_t_fsflushr` | The number of seconds between fsflush scans. | 1 | 5 |
| `autoup` | Pages older than autoup in seconds are written to disk. | 1 | 30 |
| `doiflush` | By default, fsflush flushes both inode and data pages. Set to 0 to suppress inode updates. | 0 | 1 |
| `dopageflush` | Set to 0 to suppress page flushes. | 0 | 1 |

## THE UNIX FILE SYSTEM

The Unix File System (UFS) is the general-purpose, disk-based file system that is shipped with Solaris. It has been the standard disk-based file system since early versions of SunOS 4.x. Over the life of Solaris, UFS has undergone extensive changes to keep pace with the required application performance, security, and reliability constraints.

### 14.1 UFS Development History

The original version of UFS is derived from the Berkeley Fast File System (FFS) work from BSD Unix, architected by Kirk McKusick and Bill Joy in the late eighties. The Berkeley FFS was the second major file system available for Unix and was a leap forward from the original System V file system. The System V file system was lightweight and simple but had significant shortcomings: poor performance, unreliability, and lack of functionality.

During the development of SunOS 2.0, a file-system-independent interface was introduced to provide support for concurrent, different file systems within an operating system instance. This interface, known today as the vnode/vfs interface, is the mechanism all file systems use to interface with the file-related system calls. (The vnode/vfs architecture is discussed further in “The vnode” on page 543.) At that time, UFS was modified so that it could be used within the vnode/vfs framework. Since then, UFS has been the focus of much of the file system development effort in Solaris.

A second major overhaul for UFS was at the time of SunOS 4.0, when the virtual memory system was redeveloped to use the vnode as the core of virtual memory operations. The new VM system implemented the concept of virtual file caching—a departure from the traditional physical file cache (known as the “buffer cache” in previous versions of Unix). The old buffer cache was layered under the file systems and cached the physical blocks from the file system to the storage device. The new model is layered above the file systems and allows the VM system to act as a cache for files rather than blocks. The VM system caches page-sized pieces of files, where the file and a particular offset are cached as pages of memory. From this point forward, the buffer cache was used only for file system metadata, and the VM system implements file system caching. The new VM system affected the file systems in many ways and required significant changes to the vnode interface. At that point, UFS was substantially modified to provide support for the new vnode and VM interfaces.

The third major change to UFS was in Solaris 2.4 in 1994, which saw the introduction of file system metadata logging to provide better reliability and faster reboot times after a system crash or outage. The first versions of logging were introduced in the unbundled Online: DiskSuite 3.0, the precursor to Solstice DiskSuite (SDS). Solaris 7 saw the integration of logging into the base Solaris UFS.

Table 14-1 summarizes the major UFS development milestones.

**Table 14-1** *Unix File System Evolution*

| Year | SunOS Version | Annotations |
| --- | --- | --- |
| 1984 | SunOS 1.0 | FFS from 4.2 BSD. |
| 1985 | SunOS 2.0 | UFS rearchitected to support vnodes/vfs. |
| 1988 | SunOS 4.0 | UFS integrated with new VM virtual file cache. |
| 1991 | SunOS 4.1 | I/O clustering added to allow extent-like performance. |
| 1992 | SunOS 4.1 | 1TB file system and ability to grow UFS file systems with Online: DiskSuite 1.0. |
| 1992 | Solaris 2.0 | 1TB file system support included in base Solaris. |
| 1994 | Solaris 2.4 | Metadata logging option with Online: DiskSuite 3.0. |
| 1995 | Solaris 2.6 | Large file support allows 1TB files. Direct I/O uncached access added. |
| 1998 | Solaris 7 | Metadata logging integrated into base Solaris UFS. |

### 14.2 UFS On-Disk Format

The on-disk format of the UFS file system has largely remained unchanged with the introduction of new features, maintaining forward compatibility across all releases. This allows Solaris to be upgraded without the need to back up and restore file systems.

#### 14.2.1 UFS Inodes

Information about which data blocks relate to each file are stored in a special file index node: the inode. The inode contains all of the information about the file, except for the file name, which is stored in the directory. Inode information includes:

- File type (regular, special, fifo, link, etc.)
- Owner of file (uid)
- Group of file (gid)
- File size
- Attributes (read, execute, modify)
- Timestamps (last modified, etc.)
- Number of references to the file (links)
- Arrays of disk block addresses that contain the file’s data

#### 14.2.2 UFS Directories

The file-name information and hierarchy information that constitute the directory structure of UFS are stored in directories. Each directory stores a list of file names and the inode number for each file; this information allows the directory structure to relate file names to real disk files.

The directory itself is stored in a file as a series of chunks, which are groups of the directory entries. Each directory entry in the chunk contains the following information (see Figure 14-1):

- Inode number
- Size of the file-name entry
- Length of the directory entry
- File-name string (null-terminated)

Earlier file systems like the System V file system had a fixed directory record length, which meant that a lot of space would be wasted if provision was made for long file names. In the UFS, each directory entry can be of variable length, thus
