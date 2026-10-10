
and UUID associated to it. To do this, use the `-f` parameter, followed by the device name:

```
$ lsblk -f /dev/sda1
NAME FSTYPE LABEL UUID                       FSAVAIL FUSE% MOUNTPOINT
sda1 ext4      6e2c12e3-472d-4bac-a257-c49ac07f3761  64,9G 33% /
```

Here is the meaning of each column:

- **NAME**
  - Name of the device containing the filesystem.
- **FSTYPE**
  - Filesystem type.
- **LABEL**
  - Filesystem label.
- **UUID**
  - Universally Unique Identifier (UUID) assigned to the filesystem.
- **FSAVAIL**
  - How much space is available in the filesystem.
- **FUSE%**
  - Usage percentage of the filesystem.
- **MOUNTPOINT**
  - Where the filesystem is mounted.

In `/etc/fstab` a device can be specified by its UUID with the `UUID=` option, followed by the UUID, or with `LABEL=`, followed by the label. So, instead of:

```
/dev/sda1  /  ext4  noatime,errors
```

You would use:

```
UUID=6e2c12e3-472d-4bac-a257-c49ac07f3761  /  ext4  noatime,errors
```

Or, if you have a disk labeled home disk:

```
LABEL=homdisk /home ext4 defaults
```

The same syntax can be used with the mount command. Instead of the device name, pass the UUID or label. For example, to mount an external NTFS disk with the UUID 56C11DCC5D2E1334 on `/mnt/external`, the command would be:

```
$ mount -t ntfs UUID=56C11DCC5D2E1334 /mnt/external
```

## Mounting Disks with Systemd

Systemd is the init process, the first process to run on many Linux distributions. It is responsible for spawning other processes, starting services and bootstrapping the system. Among many other tasks, systemd can also be used to manage the mounting (and automounting) of filesystems.

To use this feature of systemd, you need to create a configuration file called a *mount unit*. Each volume to be mounted gets its own mount unit and they need to be placed in `/etc/systemd/system/`.

Mount units are simple text files with the .mount extension. The basic format is shown below:

```ini
[Unit]
Description=

[Mount]
What=
Where=
Type=
Options=

[Install]
WantedBy=
```

**Description=**
Short description of the mount unit, something like Mounts the backup disk.

**What=**
What should be mounted. The volume must be specified as `/dev/disk/by-uuid/VOL_UUID` where VOL_UUID is the UUID of the volume.

**Where=**
Should be the full path to where the volume should be mounted.

**Type=**
The filesystem type.

**Options=**
Mount options that you may wish to pass, these are the same used with the **mount** command or in */etc/fstab*.

**WantedBy=**
Used for dependency management. In this case, we will use **multi-user.target**, which means that whenever the system boots into a multi-user environment (a normal boot) the unit will be mounted.

Our previous example of the external disk could be written as:

```ini
[Unit]
Description=External data disk

[Mount]
What=/dev/disk/by-uuid/56C11DCC5D2E1334
Where=/mnt/external
Type=ntfs
Options=defaults

[Install]
WantedBy=multi-user.target
```

But we are not done yet. To work correctly, the mount unit **must** have the same name as the mount point. In this case, the mount point is `/mnt/external`, so the file should be named **mnt-external.mount**.

After that, you need to restart the systemd daemon with the **systemctl** command, and start the unit:

```sh
# systemctl daemon-reload
# systemctl start mnt-external.mount
```

Now the contents of the external disk should be available on `/mnt/external`. You can check the status of the mounting with the command `systemctl status mnt-external.mount`, like below:

```
# systemctl status mnt-external.mount
- mnt-external.mount - External data disk
  Loaded: loaded (/etc/systemd/system/mnt-external.mount; disabled; vendor preset: enabled)
  Active: active (mounted) since Mon 2019-08-19 22:27:02 -03; 14s ago
  Where: /mnt/external
  What: /dev/sdb1
  Tasks: 0 (limit: 4915)
  Memory: 128.0K
  CGroup: /system.slice/mnt-external.mount

Aug 19 22:27:02 pop-os systemd[1]: Mounting External data disk...
Aug 19 22:27:02 pop-os systemd[1]: Mounted External data disk.
```

The `systemctl start mnt-external.mount` command will only enable the unit for the current session. If you want to enable it on every boot, replace `start` with `enable`:

```
# systemctl enable mnt-external.mount
```

### Automounting a Mount Unit

Mount units can be automounted whenever the mount point is accessed. To do this, you need an `.automount` file, alongside the `.mount` file describing the unit. The basic format is:

```
[Unit]
Description=

[Automount]
Where=

[Install]
WantedBy=multi-user.target
```

Like before, `Description=` is a short description of the file, and `Where=` is the mountpoint. For example, an `.automount` file for our previous example would be:

```
[Unit]
Description=Automount for the external data disk

[Automount]
Where=/mnt/external

[Install]
WantedBy=multi-user.target
```

Save the file with the same name as the mount point (in this case, mnt-external.automount), reload systemd and start the unit:

```
# systemctl daemon-reload
# systemctl start mnt-external.automount
```

Now whenever the /mnt/external directory is accessed, the disk will be mounted. Like before, to enable the automount on every boot you would use:

```
# systemctl enable mnt-external.automount
```

## Guided Exercises

1. Using mount, how can you mount an ext4 filesystem on /dev/sdc1 to /mnt/external as read-only, using the noatime and async options?

2. When unmounting a filesystem at /dev/sdd2, you get the target is busy error message. How can you find out which files on the filesystem are open, and what processes opened them?

3. Consider the following entry in /etc/fstab: /dev/sdb1 /data ext4 noatime,noauto,async. Will this filesystem be mounted if the command mount -a is issued? Why?

4. How can you find out the UUID of a filesystem under /dev/sdb1?

5. How can you use mount to remount as read-only an exFAT filesystem with the UUID 6e2c12e3-472d-4bac-a257-c49ac07f3761, mounted at /mnt/data?

6. How can you get a list of all ext3 and ntfs filesystems currently mounted on a system?

## Explorational Exercises

1. Consider the following entry in `/etc/fstab`: `/dev/sdc1  /backup  ext4  noatime,nouser,async.` Can a user mount this filesystem with the command `mount /backup`? Why?

2. Consider a remote filesystem mounted at `/mnt/server`, which has become unreachable due to a loss of network connectivity. How could you force it to be unmounted, or mounted as read-only if this is not possible?

3. Write an `/etc/fstab` entry that would mount a btrfs volume with the label `Backup` on `/mnt/backup`, with default options and without allowing the execution of binaries from it.

4. Consider the following systemd mount unit:

```ini
[Unit]
Description=External data disk

[Mount]
What=/dev/disk/by-uuid/56C11DCC5D2E1334
Where=/mnt/external
Type=ntfs
Options=defaults

[Install]
WantedBy=multi-user.target
```

- What would be an equivalent `/etc/fstab` entry for this filesystem?

5. What should be the file name for the unit above, so it can be used by systemd? Where should it be placed?

## Summary

In this lesson, you learned how to mount and unmount filesystems, manually or automatically. Some of the commands and concepts explained were:

- **mount** (mounts a device to a location)
- **umount** (unmounts a device)
- **lsof** (lists the processes accessing a filesystem)
- `/mnt` and `/media` directories
- `/etc/fstab`
- **lsblk** (lists the type and UUID of a filesystem)
- How to mount a filesystem using its UUID or label.
- How to mount a filesystem using systemd mount units.
- How to automount a filesystem using systemd mount units.

## Answers to Guided Exercises

1. Using mount, how can you mount an ext4 filesystem on /dev/sdc1 to /mnt/external as read-only, using the noatime and async options?

```
# mount -t ext4 -o noatime,async,ro /dev/sdc1 /mnt/external
```

2. When unmounting a filesystem at /dev/sdd2, you get the target is busy error message. How can you find out which files on the filesystem are open, and what processes opened them?

Use lsof followed by the device name:

```
$ lsof /dev/sdd2
```

3. Consider the following entry in /etc/fstab: /dev/sdb1 /data ext4 noatime,noauto,async. Will this filesystem be mounted if the command mount -a is issued? Why?

It will not be mounted. The key is the noauto parameter, which means this entry be ignored by mount -a.

4. How can you find out the UUID of a filesystem under /dev/sdb1?

Use lsblk -f, followed by the filesystem name:

```
$ lsblk -f /dev/sdb1
```

5. How can you use mount to remount as read-only an exFAT filesystem with the UUID 6e2c12e3-472d-4bac-a257-c49ac07f3761, mounted at /mnt/data?

Since the filesystem is mounted, you do not need to worry about the filesystem type or the ID, just use the remount option with the ro (read-only) parameter and the mount point:

```
# mount -o remount,ro /mnt/data
```

6. How can you get a list of all ext3 and ntfs filesystems currently mounted on a system?

Use mount -t, followed by a comma-separated list of filesystems:
