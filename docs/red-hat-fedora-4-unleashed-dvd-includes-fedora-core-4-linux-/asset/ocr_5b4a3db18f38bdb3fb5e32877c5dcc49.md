To observe the existing attributes of a file, use `# lsattr filename`

The `chattr` utility is part of the *e2fsprogs* package.

A file’s attributes include its access permissions. The traditional Unix systems of permissions is controlled with `chmod`. Posix Access Control Lists extend this functionality.

ACL supports permissions for users and groups beyond the traditional owner/group/world scheme. They enable finer-grained control of permissions for files.

To learn more about Access Control Lists, visit the Posix ACLs for Linux website: http://acl.bestbits.at/.

How big are these blocks? The default size is 1,024 bytes, but the size can be made smaller or larger when the file system is first created. The optimum size is determined by the application of the particular machine. If you typically use very large files, a larger block size can speed up disk I/O operations at the expense of slower I/O for smaller files; the reverse is also true. For an individual system, it might require monitoring over time and benchmarking before an optimal value is determined. For most users, the defaults have been found satisfactory.

# ## File System Partitions

File system partitions are ways to organize blocks of data on the physical drive media and are parts of the overall file system on your computer. No single universal partition format exists. In addition to the commonly used DOS partition format (used by Linux as well), Fedora Core also provides support for the following partition types:

+   - Acorn
+   - Alpha OS (compiled into the kernel)
+   - Amiga
+   - Atari
+   - Macintosh (compiled into the kernel)
+   - BSD (compiled into the kernel)
+   - Minix (compiled into the kernel)
+   - SunOS/Solaris (compiled into the kernel)
+   - Unixware slices (compiled into the kernel)
+   - SGI (compiled into the kernel)
+   - Windows Logical Disk Manager
+   - DEC Ultrix (now owned by Hewlett Packard)