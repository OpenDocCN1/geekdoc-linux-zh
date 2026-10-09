
The space used by the snapshot is now available for more junk files.

## Compression

Snapshots aren't the only way ZFS can save space. ZFS uses on-the-fly compression, transparently inspecting the contents of each file and squeezing its size if possible. With ZFS, your programs don't need to compress their log files: the filesystem will do it for you in real time. While FreeBSD enables compression by default at install time, you'll use it more effectively if you understand how it works.

Compression changes system performance, but probably not in the way you think it would. You'll need CPU time to compress and decompress data as it goes to and from the disk. Most disk requests are smaller than usual, however. You essentially exchange processor time for disk I/O. Every server I manage, whether bare metal or virtual, has far, far more processor capacity than disk I/O, so that's a trade I'll gleefully make. The end result is that using ZFS compression most often *increases* performance.

Compression works differently on different datasets. Binary files are already pretty tightly compressed; compressing `/usr/bin` doesn't save much space. Compressing `/var/log`, though, often results in reducing file size by a factor of six or seven. Check the property `compressratio` to see how effectively compression shrinks your data. My hosts write to logs far more often than they write binaries. I'll gleefully accept a sixfold performance increase for the most common task.

ZFS supports many compression algorithms, but the default is *lz4*. The lz4 algorithm is special in that it quickly recognizes incompressible files. When you write a binary to disk, lz4 looks at it and says, “Nope, I can't help you,” and immediately quits trying. This eliminates pointless CPU load. It effectively compresses files that can be compressed, however.

## Pool Integrity and Repair

Every piece of data in a ZFS pool has an associated cryptographic hash stored in its metadata to verify integrity. Every time you access a piece of data, ZFS recomputes the hash of every block in that data. When ZFS discovers corrupt data in a pool with redundancy, it transparently corrects that data and proceeds. If ZFS discovers corrupt data in a pool without redundancy, it gives a warning and refuses to serve the data. If your pool has identified any data errors, they'll show up in `zpool status`.

### Integrity Verification

In addition to the on-the-fly verification, ZFS can explicitly walk the entire filesystem tree and verify every chunk of data in the pool. This is called a *scrub*. Unlike UFS's `fsck(8)`, scrubs happen while the pool is online and in use. If you've previously run a scrub, that will also show up in the pool status.

```
scan: scrub repaired 0 in 8h3m with 0 errors on Fri Jul 21 14:17:29 2017
```

To scrub a pool, run `zpool scrub` and give the pool name.

```
# zpool scrub zroot
```

You can watch the progress of the scrub with `zpool status`.

Scrubbing a pool reduces its performance. If your system is already pushing its limits, scrub pools only during off hours. You can cancel a scrub with the `-s` option.

```
# zpool scrub -s zroot
```

Run another scrub once the load drops.

### Repairing Pools

Disks fail. That's what they're for. The point of redundancy is that you can replace failing or flat-out busted disks with working disks and restore redundancy.

Mirror and RAID-Z virtual devices are specifically designed to reconstruct the data lost when a disk fails. They’re much like RAID in that regard. If one disk in a ZFS mirror dies, you replace the dead disk, and ZFS copies the surviving mirror onto the new disk. If a disk in a RAID-Z VDEV fails, you replace the busted drive, and ZFS rebuilds the data on that disk from parity data.

In ZFS, this reconstruction is called *resilvering*. Like other ZFS integrity operations, resilvering takes place only on live filesystems. Resilvering isn’t quite like rebuilding a RAID disk from parity, as ZFS leverages its knowledge of the filesystem to optimize repopulating the replacement device. Resilvering begins automatically when you replace a failed device. ZFS resilvers at a low priority so that it doesn’t interfere with normal operations.

### Pool Status

The *zpool status* command shows the health of the underlying storage hardware in the *STATE* field. We’ve seen a couple examples of healthy pools, so let’s take a look at an unhealthy pool.

```
# zpool status db
pool: db
 state: DEGRADED
 status: One or more devices could not be opened.  Sufficient replicas exist for
 the pool to continue functioning in a degraded state.
 action: Attach the missing device and online it using 'zpool online'.
 see: http://illumos.org/msg/ZFS-8000-2Q
 scan: none requested
 config:

 NAME STATE READ WRITE CKSUM
 db DEGRADED 0 0 0
 mirror-0 DEGRADED 0 0 0
 gpt/zfs1 ONLINE 0 0 0
 14398195156659397932 UNAVAIL 0 0 0 was
 /dev/gpt/zfs3
 errors: No known data errors
```

The pool state is DEGRADED. If you look further down the output, you’ll see more DEGRADED entries and an UNAVAIL. What exactly does that mean?

Errors in a pool percolate upward. The pool state is a summary of the health of the pool as a whole. The whole pool shows up as DEGRADED because the pool’s virtual device *mirror-0* is DEGRADED. This error comes from an underlying disk being in the UNAVAIL state. We get the ZFS GUID for this disk, and the label used to create the pool.

ZFS pools show an error when an underlying device has an error. When a pool has a state other than ONLINE, dig through the VDEV and disk listings until you find the real problem.

Pools, VDEVs, and disks can have six states:

- **ONLINE** The device is functioning normally.
- **DEGRADED** The pool or VDEV has at least one provider missing, offline, or generating errors more quickly than ZFS tolerates. Redundancy is handling the error, but you need to address this right now.
- **FAULTED** A faulted disk is corrupt or generating errors more quickly than ZFS can tolerate. A faulted VDEV takes the last known good copy of the data. A two-disk mirror with two bad disks faults.
- **UNAVAIL** ZFS can’t open the disk. Maybe it’s been removed, shut off, or that iffy cable finally failed. It’s not there, so ZFS can’t use it.
- **OFFLINE** This device has been deliberately turned off.
- **REMOVED** Some hardware detects when a drive is physically removed while the system is running, letting ZFS set the REMOVED flag. When you plug the drive back in, ZFS tries to reactivate the disk.

Our missing disk is in the UNAVAIL state. For whatever reason, ZFS can’t access `/dev/gpt/zfs3`, but the disk mirror is still serving data because it has a working disk. Here’s where you get to run around to figure out where that disk went. How you manage ZFS depends on what you discover.

## Reattaching and Detaching Drives

Unavailable drives might not be dead. They might be disconnected. If you wiggle a drive tray and suddenly get a green light, the disk is fine but the connection is faulty. You should address that hardware problem, yes, but in the meantime, you can reactivate the drive. You can also reactivate deliberately removed drives. Use the `zpool online` command with the pool name and the GUID of the missing disk as arguments. If the disk in my example pool were merely disconnected, I could reactivate it like so:

```
# zpool online db 14398195156659397932
```

ZFS resilvers the drive and resumes normal function.

If you want to remove a drive, you can tell ZFS to take it offline with `zpool offline`. Give the pool and disk names as arguments.

```
# zpool offline db gpt/zfs6
```

Bringing disks offline, physically moving them, bringing them back online, and allowing the pools to resilver will let you migrate large storage arrays from one SAS cage to another without downtime.

## Replacing Drives

If the drive isn’t merely loose but flat-out busted, you’ll need to replace it with a new drive. ZFS lets you replace drives in several ways, but the most common is using `zpool replace`. Use the pool name, the failed provider, and the new provider as arguments. Here, I replace the db pool’s `/dev/gpt/zfs3` disk with `/dev/gpt/zfs6`:

```
# zpool replace db gpt/zfs3 gpt/zfs6
```

The pool will resilver itself and resume normal operation.

In a large storage array, you can also use successive `zpool replace` operations to empty a disk shelf. Only do this if your organization’s operation requirements don’t allow you to offline and online disks.

## Boot Environments
