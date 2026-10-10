# FILES

+   /etc/fstab  file system table
+       /etc/mtab  table of mounted file systems
+       /etc/mtab~  lock file
+       /etc/mtab.tmp  temporary file

# SEE ALSO

**mount**(2), **umount**(2), **fstab**(5), **umount**(8), **swapon**(8), **nfs**(5), **mountd**(8), **nfsd**(8), **mke2fs**(8), **tune2fs**(8), **losetup**(8)

# BUGS

It is possible for a corrupted file system to cause a crash.

Some Linux file systems don't support **-o sync** (the ext2fs does support synchronous updates [a la BSD] when mounted with the **sync** option).

The **-o remount** may not be able to change mount parameters (all ext2fs-specific parameters, except **sb**, are changeable with a remount, for example, but you can't change **gid** or **umask** for the *fatfs*).

# HISTORY

A **mount** command appeared in Version 6 AT&T Unix.

# NETSTAT(8)

# NAME

**netstat**  Display network connections, routing tables, interface statistics and masquerade connections.

# SYNOPSIS

```
```
netstat [-v[ea]oc] [--tcp|-t] [--udp|-u] [--raw|-w] [--unix|-u] [-inet|-ip] [--ax25] [--ipx] [--netrom]
netstat [-v[enc]] [-inet] [-ipx] [--netrom] [--ddp] [--ax25]
[-route|-r]
```
```