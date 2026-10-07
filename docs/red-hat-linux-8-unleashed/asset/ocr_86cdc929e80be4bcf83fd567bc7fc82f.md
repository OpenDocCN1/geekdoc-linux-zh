# CHAPTER 10 Managing the Filesystem

+   * Atari
* Macintosh (compiled into the kernel)
* BSD (compiled into the kernel)
* Minix (compiled into the kernel)
* SunOS/Solaris (compiled into the kernel)
* Unixware slices (compiled into the kernel)
* SGI (compiled into the kernel)
* Windows Logical Disk Manager
* DEC Ultrix, now owned by Hewlett Packard

> NOTE
Other modules and support are likely available if you care to search the Internet for them; try searching on the keyword filesystems on http://freshmeat.net/ and http://www.google.com/linux/. As is always the case with Open Source operating systems, and energized soul can write his own filesystem modules.

# Network and Disk Filesystems

We can separate filesystems into two broad categories: those that can be used over a network and local disk filesystems. You are provided with all the applications to work with both types when using Red Hat Linux.

Network filesystems are physically stored somewhere than your local computer but appear as if they are mounted on your local computer.

> NOTE
Mounting is the UNIX method of attaching a filesystem (also referred to as a volume) to the filesystem tree at a mount point. Using the mount command is covered later in this chapter.

Some common network filesystem types are

+   * NFS—The Network File System was developed by Sun and is in common use. It has no built-in security because it was originally designed to run over freely networked friends. Although considered problematic by some, it is easy to implement. It is typically used between UNIX peers. Red Hat supports client and server installations of this filesystem.