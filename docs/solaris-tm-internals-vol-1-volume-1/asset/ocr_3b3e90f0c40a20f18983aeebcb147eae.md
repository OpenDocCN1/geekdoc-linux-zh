# Table 7-4  `prtmem` Rows (Continued)

| Row | Description |
|---|---|
| Kernel Memory | Memory used for the kernel executable, data structures, and kernel allocations, internal to the operating system. |
| Application | Anonymous memory used by processes, typically heap, stack, and copy-on-write pages. |
| Executable & libs | Executable and shared library pages that are mapped into process address space. |
| File Cache | File cache that is not on the free list. |
| Free, file cache | File system cache that has been placed on the free list. This file cache memory still contains valid cache but will be consumed from the free list when memory is needed. |
| Free, free | Memory that is free and not associated with any files. |

# 7.4.2.2 File System Cache Memory: `memps -m`

Memtool provides a list showing where the pool of filesystem cache memory has been allocated, sorted by vnode. The list summarizes the size of each vnode in the file system cache and, if possible, gives the real file name. If the real file name cannot be determined, then the device and inode number are printed for that vnode.

We can display the list of vnodes in file system cache with the memps -m command. Table 7-5 describes the columns.

```
```text
# memps -m

SunOS devhome 5.7 SunOS_Development sun4u    02/08/100

00:23:12
   Size E/F Filename
10232k E  /export/usr/local/netscape/netscape
 5648k E  /export/ws/dist/share/framemaker_v5.5.3/bin/sparc/maker5X.e
 2944k E  /home/cmr/.netscape/history.dat
 2888k E  /ws/ongos/tools/SUNWspc/SC5.x/contrib/XEmacs20.3-b91/bin/sparc-sun-
 2000k E  /export/ws/dist/share/acroread,v3.01/Reader/sparc/solaris/bin/libX...
 1648k E  /usr/dt/lib/libXm.so.4
 1400k E  /usr/dt/lib/libXm.so.3
 1392k E  /export/openswin/server/lib/libserverops.so.5
  928k E  /export/ws/dist/share/acroread,v3.01/Reader/sparc/solaris/lib/libread
  824k E  /export/ws/dist/share/acroread,v3.01/Reader/sparc/solaris/bin/acrorea
     .
     .
     .
```
```