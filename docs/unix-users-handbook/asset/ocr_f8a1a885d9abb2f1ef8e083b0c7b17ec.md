+   - Loopback File System (LOFS) allows you to have the same file system in multiple places using alternate path names.
- VxFS is an extent-based Journal File System that supports fast file system recovery and on-line features such as backup on HP-UX.
- High Performance File System (HFS) is HP's version of the UNIX File System. This is used in most of the examples.
- TMPFS is a memory-based file system.
- CacheFS is a file system present in cache.

File system types is an area of high customization on UNIX variants. You will find some of the file systems listed on some UNIX variants and others on other UNIX variants. Although UNIX and its associated commands are very similar, going from one UNIX variant to another, file system types are generally peculiar to a specific UNIX variant. A good place to start when determining what file system types are included with your UNIX variant is to view the file system types listed in the manual page for mount.

![](bbox=[0.04, 0.56, 0.12, 0.64])

The manual page for mount on the Caldera Linux system we are using lists many file system types. With the Linux mount command, you would use the -t vfstype option to specify one of the file system types to mount:

+   - minix
- ext
- ext2
- xiafs
- hpfs