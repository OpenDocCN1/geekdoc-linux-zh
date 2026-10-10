# Listing 11-6

# Minimal BusyBox Root File System

```
$ tree
|-- bin
|   |-- busybox
|   |-- cat -> busybox
|   |-- dmesg -> busybox
|   |-- echo -> busybox
|   |-- hostname -> busybox
|   |-- ls -> busybox
|   |-- ps -> busybox
|   |-- pwd -> busybox
|   `-- sh -> busybox
|-- console
|-- etc
`-- proc
4 directories, 10 files
```

This BusyBox-based root file system occupies little more than the size needed for busybox itself. In this configuration, using static linking and supporting nearly 100 utilities, the BusyBox executable came in at less than 1MB:

```
$ ls -1 /bin/busybox
-rwxr-xr-x 1 root root 824724 Dec 3 2005 /bin/busybox
```

Now let's see how this system behaves. Listing 11-7 captures the console output on power-up on this BusyBox-based embedded system.

# Listing 11-7

# BusyBox Default Startup

```
...
Looking up port of RPC 100003/2 on 192.168.1.9
Looking up port of RPC 100005/1 on 192.168.1.9
VFS: Mounted root (nfs filesystem).
Freeing init memory: 96k
Bummer, could not run '/etc/init.d/rcS': No such file or directory

Please press Enter to activate this console.

BusyBox v1.01 (2005.12.03-19:09+0000) Built-in shell (ash)
Enter 'help' for a list of built-in commands.

-sh: can't access tty; job control turned off
/ #
```