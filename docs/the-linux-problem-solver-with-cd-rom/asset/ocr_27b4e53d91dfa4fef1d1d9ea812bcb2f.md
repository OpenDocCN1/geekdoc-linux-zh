# PROBLEM 18

Symptom: Stale NFS file handle errors. I/O errors. Empty directories.

Problem: Lingering processes, a moved directory, or a stale file handle.

Fix: When you move a directory or change the source of a mount point, there's always a risk that a user will be using a file or directory underneath that mount point when you make the change. Fix it by trial and error. First make sure the Automounter is not running for this mount point. Then try to unmount the directory at the mount point by hand. If umount complains that the directory is busy, you probably need to kill some process (most likely a user process) that's accessing it. Usually it's pretty simple to hunt these down with a process listing, but sometimes you have to use lsof.

Often the Automounter refuses to start backing up because the automount point itself is hung up on something. You can also try to umount that (for example, in our /home example, you'd try umount /home). In rare cases, rebooting is the only fix.

Relevant man pages: autofs (5), automount (8), autofs (8)

# NFS Mount Options

There are a few (sometimes) useful options to an NFS mount. You can invoke them with the -o option, placing a comma between multiple options:

```
# mount -o bg,soft foo.example.com:/scratch /mnt
```

rsize=n, wsize=n Set the read and write buffer sizes to n bytes. Before Linux kernel version 2.2, the default NFS buffer size was 1024 bytes. However, this small size significantly slowed throughput, so version 2.2 raised the defaults—you shouldn't have to worry too much if you're running that kernel or higher. You can usually take the limits up to 8192 bytes.

intr For hard mounts, allows interruption of processes hung on an NFS access.

soft Gives an I/O error to any program hung on an access due to a server that's not responding. Useful when some really nonessential server has a habit of crashing.

bg If there's a timeout on the first mount attempt, keep trying in the background.

Relevant man pages: nfs (5), mount (8)