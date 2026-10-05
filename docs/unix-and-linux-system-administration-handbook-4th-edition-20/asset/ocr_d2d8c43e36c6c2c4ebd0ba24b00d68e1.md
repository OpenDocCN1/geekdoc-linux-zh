# Volume snapshots

```
$ sudo mkfs /dev/DEMO/web1
$ sudo mkdir /mnt/web1
$ sudo mount /dev/DEMO/web1 /mnt/web1
```

# Volume snapshots

You can create copy-on-write duplicates of LVM2 logical volume, whether or not it contains a filesystem. This feature is handy for creating a quiescent image of a filesystem to be backed up on tape, unlike ZFS snapshots, LVM2 snapshots are unfortunately not very useful as a general method of version control.

The problem is that logical volumes are of fixed size. When you create one, storage space is allocated for it up front from the volume group. A copy-on-write initially consumes no space, but as blocks are modified, the volume manager finds space to store both the old and new versions. This space for modified blocks must be set aside when you create the snapshot, and like any LVM volume, the allocated storage is of fixed size.

Note that it does not matter whether you modify the original volume or the snapshot (which by default is writable). Either way, the cost of duplicating the blocks is charged to the snapshot. Snapshots' allocations can be paid away by activity on the source volume when the snapshots themselves are idle.

If you do not allocate much space for a snapshot as is consumed by the volume of which it is, you can potentially run out of space in the snapshot. More catastrophic than it sounds because the volume manager has no way to maintain a coherent image of the snapshot; additional storage space is required to keep the snapshot the same. The result of running out of space is that LVM stops maintaining the snapshot, and the snapshot becomes irrevocably corrupt.

So

![](bbox=[0.943, 0.443, 0.993, 0.55])