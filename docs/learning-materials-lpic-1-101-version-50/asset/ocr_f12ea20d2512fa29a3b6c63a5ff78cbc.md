```
drwxrwxr-x 1 carol carol 988 jul 13 17:30 Images
```

**NOTE**    Yes, subvolumes can *also* be accessed like any other directory.

We can check that the subvolume is active, with the command:

```
```bash
# btrfs subvolume show /mnt/disk/BKP/
    Name:                   BKP
    UUID:                   e90alafe-69fa-da4f-9764-3384f66fa32e
    Parent UUID:            -
    Received UUID:          -
    Creation time:          2019-07-13 17:35:40 +0300
    Subvolume ID:           260
    Generation:            23
    Gen at creation:       22
    Parent ID:              5
    Top level ID:           5
    Flags:                  -
    Snapshot(s):
```
```

You can mount the subvolume on /mnt/BKP by passing the -t btrfs -o subvol=NAME parameter to the mount command:

```
# mount -t btrfs -o subvol=BKP /dev/sdb1 /mnt/bkp
```

**NOTE** The -t parameter specifies the filesystem type to be mounted.

# Working with Snapshots

Snapshots are just like subvolumes, but pre-populated with the contents from the volume from which the snapshot was taken.

When created, a snapshot and the original volume have exactly the same content. But from that point in time, they will diverge. Changes made to the original volume (like files added, renamed or deleted) will not be reflected on the snapshot, and vice-versa.

Keep in mind that a snapshot *does not* duplicate the files, and initially takes almost no disk space. It simply duplicates the filesystem tree, while pointing to the original data.

The command to create a snapshot is the same used to create a subvolume, just add the snapshot parameter after btrfs subvolume. The command below will create a snapshot of the Btrfs