You *must* check `/var/log/messages` for errors after a background *fsck*. The preliminary *fsck* assessment can make an error, and perhaps a full single-user mode's *fsck* on a partition really is required. If you find such a message, schedule downtime within a few hours to correct the problem. While inconvenient, having the system down for a scheduled period is better than the unscheduled downtime caused by a power outage and the resulting single-user mode's *fsck* `-y`.

# Forcing Read-Write Mounts on Dirty Disks

If you really want to force FreeBSD to mount a dirty disk read-write without using a background *fsck*, you can. You won't like the results. At all. But, as it's described in *mount*(8), some reader will think it's a good idea unless they know why. Use the `-w` (read-write) and `-f` (force) flags to *mount*(8).

Mounting a dirty partition read-write corrupts data. Note the absence of words like *might* and *could* from that sentence. Also note I didn't use *recoverable*. Mounting a dirty filesystem may panic your computer. It might destroy all remaining data on the partition or even shred the underlying filesystem. Forcing a read-write mount of a dirty filesystem is seriously bad juju. Don't do it.

# Background fsck, fsck -y, Foreground fsck, Oy Vey!

All these different *fsck*(8) problems and situations can occur, but when does FreeBSD use each command? FreeBSD uses the following conditions to decide when and how to *fsck*(8) on a filesystem:

+   * If the filesystem is clean, it is mounted without *fsck*(8).
+   * If a journaled filesystem is dirty at boot, FreeBSD recovers the data from the journal and continues the boot. A journaled filesystem rarely needs *fsck*(8).
+   * If a filesystem without soft updates is dirty at boot, FreeBSD runs *fsck*(8) on it. If the filesystem damage is severe, FreeBSD stops