Make it so:

```
```sh
# sysconfigtab -t /mnt/etc/sysconfigtab -a -f /tmp/bd_mod.stanza.vx
# sysconfigtab -t /mnt/etc/sysconfigtab -m -f /tmp/bd_mod.stanza clauses
```
```

+   6. Restore the “n” partition (cnx).

```
```sh
# /usr/sbin/clu_bdmgr -h dsk10
```
```

+   7. Unmount the member’s boot_partition.

```
```sh
# umount /mat
```
```

+   8. Adjust the bootdef_dev console variable on molari’s console to reflect the change.

```
```text
>>> set bootdef_dev DKB202
```
```

The device DKB202 is the appropriate console device name that corresponds to dsk10 in UNIX.

+   9. Boot molari.

```
```text
>>> boot
```
```

# 22.1.5  Restoring a Critical Data File System

Just as losing a file system critical to the operating system can be a problem for your cluster, so can losing a critical data file system. Restoring a data or non-OS file system is really no different in a cluster than in a standalone Tru64 UNIX system. For example, if your backups are made with vdump, you can restore them quite easily with this vrestore command:

```
```sh
# vrestore -xf /dev/tape/tape0 -D /data
```
```

If restoring to a new disk, you will, of course, have to disklabel it and create a new file system (either AdvFS or UFS) before restoring and either rename the device special file or adjust any references to the device name (like in /etc/fdmns) to point to the new device. The point here is that it isn’t special because it’s a cluster.