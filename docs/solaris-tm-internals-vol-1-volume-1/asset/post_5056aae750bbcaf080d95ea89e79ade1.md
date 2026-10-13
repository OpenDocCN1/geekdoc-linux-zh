
The changes are noteworthy. Table 13-13 summarizes the important changes to the DNLC.

**Table 13-13.** *Solaris DNLC Changes*

| Year | OS Rev | Comment |
|---|---|---|
| 1984 | BSD 4.2 | 14-character name maximum |
| 1990 | SunOS 2.0 | 31-character name maximum |
| 1994 | SunOS 5.4 | Performance (new locking/search algorithm) |
| 1998 | SunOS 5.7 | Variable name length |

### 13.5.5.1 DNLC Operation

Each time we open a file, we call the `open()` system call with a path name. That path name must be translated to a vnode by the process of reading the directory and finding the corresponding name that matches the requested name. No place in the vnode stores the name of the file; so, to prevent us from having to reread the directory every time we translate the path name, we cache pathname-to-vnode mappings in the directory name lookup cache. The cache is managed as an LRU cache, so that most frequently used directory entries are kept in the cache. The early-style DNLC in Solaris uses a fixed name length in the cache entries. Hence, if a file name is opened with a name larger than can fit, it will not be entered into the DNLC. The old-style (pre-SunOS 5.4) DNLC is shown in Figure 13.6.

![](img/220ae4af07df2fe8e5be69d27f885d1b_611_0.png)

The number of entries in the DNLC is controlled by the `ncsize` parameter, which is initialized to `4 * (max_nprocs + maxusers) + 320` at system boot.

Most of the DNLC work is done with two functions: `dnlc_enter()` and `dnlc_lookup()`. When a file system wants to look up the name of a file, it first checks the DNLC with the `dnlc_lookup()` function, which queries the DNLC for an entry that matches the specified file name and directory vnode. If no entry is found, `dnlc_lookup()` fails and the file system reads the directory from disk. When the file name is found, it is entered into the DNLC with the `dnlc_enter()` function. The DNLC stores entries on a hashed list (`nc_hash[]`) by file name and directory vnode pointer. Once the correct `nc_hash` chain is identified, the chain is searched linearly until the correct entry is found.

The original BSD DNLC had 8 `nc_hash` entries, which was increased to 64 in SunOS 4.x. Solaris 2.0 sized the `nc_hash` list at boot, attempting to make the average length of each chain no more than 4 entries. It used the total DNLC size, `ncsize`, divided by the average length to establish the number of `nc_hash` entries. Solaris 2.3 had the average length of the chain dropped to 2 in an attempt to increase DNLC performance; however, other problems, related to the LRU list locking and described below, adversely affected performance.

Each entry in the DNLC is also linked to an LRU list, in order of last use. When a new entry is added into the DNLC, the algorithm replaces the oldest entry from the LRU list with the new file name and directory vnode. Each time a lookup is done, the DNLC also takes the entry from the LRU and places it at the end of the list so that it won't be reused immediately. The DNLC uses the LRU list to attempt to keep most-used references in the cache. Although the DNLC lists had been made short, the LRU list still caused contention because it required that a single lock be held around the entire chain.

The old DNLC structure is shown below. Note that the name field is statically sized at 31 characters.

```c
#define NC_NAMELEN       31      /* maximum name segment length we bother with */

struct ncache {
        struct ncache *hash_next;        /* hash chain, MUST BE FIRST */
        struct ncache *hash_prev;
        struct ncache *lru_next;          /* LRU chain */
        struct ncache *lru_prev;
        struct vnode *vp;                /* vnode the name refers to */
        struct vnode *dp;                /* vnode of parent of name */
        char namlen;                     /* length of name */
        char name[NC_NAMELEN];           /* segment name */
        struct cred *cred;               /* credentials */
        int hash;                        /* hash signature */
};
```

Header File `<sys/dnlc.h>`

### 13.5.5.2 The New Solaris DNLC Algorithm

In Solaris 2.4, replacement of the SVR4 DNLC algorithm yielded a significant improvement in scalability. The Solaris 2.4 DNLC algorithm removed LRU list lock contention by eliminating the LRU list completely. In addition, the list now takes into account the number of references to a vnode and whether the vnode has any pages in the page cache. This design allows the DNLC to cache the most relevant vnodes, rather than just the most frequently looked-up vnodes.

```c
struct ncache {
        struct ncache *hash_next;        /* hash chain, MUST BE FIRST */
        struct ncache *hash_prev;
        struct ncache *next_free;         /* freelist chain */
        struct vnode *vp;                /* vnode the name refers to */
        struct vnode *dp;                /* vnode of parent of name */
        struct cred *cred;               /* credentials */
        char *name;                      /* segment name */
        int namlen;                      /* length of name */
        int hash;                        /* hash signature */
};
```

Header File `<sys/dnlc.h>`

The lookup algorithm uses a rotor pointing to a hash chain, which switches chains for each invocation of `dnlc_enter()` that needs a new entry. The algorithm starts at the end of the chain and takes the first entry that has a vnode reference count of 1 or no pages in the page cache. In addition, during lookup, entries are moved to the front of the chain so that each chain is sorted in LRU order. Figure 13.4 illustrates the Solaris 2.4 DNLC.

![](img/220ae4af07df2fe8e5be69d27f885d1b_613_0.png)

The Solaris 7 DNLC was enhanced to use the kernel memory allocator to allocate a variable length string for the name; this change removed the 31-character limit. In the Solaris 7 DNLC structure, shown below, note that the name field has changed from a static structure to a pointer.

### 13.5.5.3 DNLC Support Functions

Table 13-14 lists the DNLC support functions.

**Table 13-14.** *Solaris 7 DNLC Functions from* `sys/dnlc.h`

| Function | Description |
|---|---|
| `dnlc_lookup()` | Locates an ncache entry that matches the supplied name and directory vnode pointer. Returns a pointer to the vnode for that entry or returns NULL. |
| `dnlc_update()` | Enters a new ncache entry into the DNLC for the given name and directory vnode pointer. If an entry already exists for the name and directory pointer but the vnode is different, then the entry is overwritten. Otherwise, the function returns with no action. |
| `dnlc_enter()` | Enters a new ncache entry into the DNLC for the given name and directory vnode pointer. If an entry already exists for the name and directory pointer, the function returns with no action. |
| `dnlc_remove()` | Removes the entry matching the supplied name and directory vnode pointer. |
| `dnlc_purge()` | Called by the vfs framework when an `umountall()` is called. |
| `dnlc_purge_vp()` | Purges all entries matching the vnode supplied. |

## 13.5.6 File System Modules

A file system is implemented as an instance of the vfs and vnode objects in a self-contained, loadable kernel module. The operating system provides the infrastructure for mounting and interfacing with the file system, and each file system implementation can abstract the file system object methods in different ways. The modules are loaded from the file system directory `/kernel/fs` during the first mount operation. File systems provide module initialization functions; a typical file system initialization section declares a module constructor and destructor, as described in “Kernel Module Loading and Linking” on page 116.

## 13.5.7 Mounting and Unmounting

When a file system is first mounted, the file system framework attempts to auto-load the file system from the `/kernel/fs` directory. The autoload procedure calls the initialization routines in the file system; at that point, the file system can register itself in the file system switch table. The file system is required to fill in the `vfs` structure during the initialization function. Once this phase is completed, the file system is available for mount requests and the mount method of the file system is called.

When the mount method is called for the file system, a vfs object for the instance of the mounted file system is created; then, the mount method must fill in the vfs structures. Typically, the root vnode of the file system is either created or opened at this time. The following example shows a simple file system and its initialization functions.
