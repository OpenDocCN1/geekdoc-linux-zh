
ZFS supports several different types of VDEV, each differentiated by the degree and style of redundancy they offer. The common mirrored disk, where each disk copies what’s on another disk, is one type of VDEV. Piles of disks with no redundancy is another type of VDEV. And ZFS includes three different varieties of sophisticated parity-based redundancy, called RAID-Z.

Using multiple VDEVs in a pool creates systems similar to advanced RAID arrays. A RAID-Z2 array looks an awful lot like RAID-6, but a ZFS pool with two RAID-Z2 VDEVs resembles RAID-60. Mirrored VDEVs work like RAID-1, but multiple mirrors in a pool behave like RAID-10. In both of these cases, ZFS stripes the data across the VDEV with no redundancy. The individual VDEVs provide the redundancy.

Choose your VDEV type carefully.

## Striped VDEVs

A VDEV composed of a single disk is called a stripe and has no redundancy. Losing the disk means losing your data. While a pool can contain multiple striped VDEVs, each disk is its own VDEV. Much like RAID-0, losing one disk means losing the whole pool.

## Mirror VDEVs

A mirror VDEV stores a complete copy of all the VDEV’s data on every disk. You can lose all but one of the drives in the VDEV and still access your data. A mirror can contain any number of disks.

ZFS can read data from all of the mirrored disks simultaneously, so reading data is fast. When you write data, though, ZFS must write that data to all of the disks simultaneously. The write isn’t complete until the slowest disk finishes. Write performance suffers.

## RAID-Z

RAID-Z spreads data and parity information across all of the disks, much like conventional RAID. If a disk in a RAID-Z dies or starts giving corrupt data, RAID-Z uses the parity information to recalculate the missing data. A RAID-Z VDEV must contain at least three disks and can withstand the loss of any single disk. RAID-Z is sometimes called *RAID-Z1*.

You can't add or remove disks in a RAID-Z. If you create a five-disk RAID-Z, it will remain a five-disk RAID-Z forever. Don't go thinking you can add an additional disk to a RAID-Z for more storage. You can't.

If you're using disks over 2TB, there's a nontrivial chance of a second drive failing as you repair the first drive. For large disks, you should probably consider RAID-Z2.

### RAID-Z2

RAID-Z2 stripes parity and data across every disk in the VDEV, much like RAID-Z1, but doubles the amount of parity information. This means a RAID-Z2 can withstand the loss of up to two disks. You can't add or remove disks from a RAID-Z2. It is slightly slower than RAID-Z.

A RAID-Z2 must have four or more disks.

### RAID-Z3

Triple parity is for the most important data or those sysadmins with a whole bunch of disks and no time to fancy about. You can lose up to three disks in your RAID-Z3 without losing data. As with any other RAID-Z, you can't add or remove disks from a RAID-Z3.

A RAID-Z3 must have five or more disks.

### Log and Cache VDEVs

Pools can improve performance with special-purpose VDEVs. Only adjust or implement these if performance problems demand them; don't add them proactively. Most people don't need them, so I won't go into details, but you should know they exist in case you get unlucky.

The *Separate Intent Log* (SLOG or ZIL) is ZFS's filesystem journal. Pending writes get dumped to the SLOG and then arranged more properly in the primary pool. Every pool dedicates a chunk of disk space for a SLOG, but you can use a separate device for the SLOG instead. You need faster writes? Install a really fast drive and dedicate it to the SLOG. The pool will dump all its initial writes to the fast disk device and then migrate those writes to the slower media as time permits. A dedicated fast SLOG will also smooth out bursty I/O.

The *Level 2 Adaptive Replacement Cache (L2ARC)* is like the SLOG but for reads. ZFS keeps the most recently accessed and the most frequently accessed data in memory. By adding a really fast device as an L2ARC, you expand the amount of data ZFS can provide from cache instead of calling from slow disk. An L2ARC is slower than memory but faster than the slow disk.

### RAID-Z and Pools

You can add VDEVs to a pool. You can’t add disks to a RAID-Z VDEV. Think about your storage needs and your hardware before creating your pools.

Suppose you have a server that can hold 20 hard drives, but you have only 12 drives. You create a single RAID-Z2 VDEV out of those 12 drives, thinking that you’ll add more drives to the pool later if you need them. You haven’t even finished installing the server, and already you’ve failed.

You can add multiple identical VDEVs to a pool. If you create a pool with a 12-disk VDEV, and the host can hold only another 8 disks, there’s no way to create a second identical VDEV. A 12-disk RAID-Z2 isn’t identical to an 8-disk RAID-Z2. You can force ZFS to accept the different VDEVs, but performance will suffer. Adding a VDEV to a pool is irreversible.

Plan ahead. Look at your physical gear. Decide how you will expand your storage. This 20-drive server would be fine with two 10-disk RAID-Z2 VDEVs, or one 12-disk pool and a separate 8-disk pool. Don’t sabotage yourself.

Once you know what sort of VDEV you want to use, you can create a pool.

### Managing Pools

Now that you understand the different VDEV types and have indulged in planning your storage, let's create some different types of zpools. Start by setting your disk block size.

### ZFS and Disk Block Size

Chapter 10 covered how modern disks have two different sector sizes, 512 bytes and 4KB. While a filesystem can safely assume a disk has 4KB sectors, if your filesystem assumes the disk has 512-byte sectors and the disk really has 4KB sectors, your performance will plunge. ZFS, of course, assumes that disks have 512-byte sectors. If your disk really has 512-byte sectors, you're good. If you're not sure what size the physical sectors are, though, err on the side of caution and tell ZFS to use 4KB sectors. Control ZFS's disk sector assumptions with the *ashift* property. An ashift of 9 tells ZFS to use 512-byte sectors, while an ashift of 12 indicates 4KB sectors. Control ashift with the sysctl vfs.zfs.min_auto_ashift.

```
sysctl vfs.zfs.min_auto_ashift=12
```

Make this permanent by setting it in `/etc/sysctl.conf`.

You *must* set ashift before creating a pool. Setting it after pool creation has no effect.

If you're not sure what size sectors your disks have, use an ashift of 12. That's what the FreeBSD installer does. You'll lose a small amount of performance, but using an ashift of 9 on 4KB disks will drain system performance.

Now create your pools.

### Creating and Viewing Pools

Create a pool with the zpool create command.

```
zpool create poolname vdevtype disks...
```

If the command succeeds, you get no output back.

Here, I create a pool named *db*, using a mirror VDEV and two GPT-labeled partitions:

```
zpool create db mirror gpt/zfs3 gpt/zfs4
```

The structure we assign gets reflected in the pool status.

```
zpool status db
--snip--
config:

NAME           STATE    READ WRITE CKSUM
db             ONLINE    0    0     0
  mirror-0     ONLINE    0    0     0
    gpt/zfs3   ONLINE    0    0     0
    gpt/zfs4   ONLINE    0    0     0
--snip--
```

The pool *db* contains a single VDEV, named *mirror-0*. It includes two partitions with GPT labels, /dev/gpt/zfs3 and /dev/gpt/zfs4. All of those partitions are online.

If you don’t include a VDEV name, zpool(8) creates a striped pool with no redundancy. Here, I create a striped pool called *scratch*:

```
zpool create scratch gpt/zfs3 gpt/zfs4
```

The pool status shows each VDEV, named after the underlying disk.

```
--snip--
NAME       STATE    READ WRITE CKSUM
scratch    ONLINE    0    0     0
  gpt/zfs3 ONLINE    0    0     0
  gpt/zfs4 ONLINE    0    0     0
--snip--
```

Creating any type of RAID-Z looks much like creating a mirror. Just use the correct VDEV type.

```
zpool create db raidz gpt/zfs3 gpt/zfs4 gpt/zfs5
```

The pool status closely resembles that of a mirror, but with more disks in the VDEV.
