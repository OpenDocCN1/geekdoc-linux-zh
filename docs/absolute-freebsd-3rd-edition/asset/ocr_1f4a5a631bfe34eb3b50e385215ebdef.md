Unavailable drives might not be dead. They might be disconnected. If you wiggle a drive tray and suddenly get a green light, the disk is fine but the connection is faulty. You should address that hardware problem, yes, but in the meantime, you can reactivate the drive. You can also reactivate deliberately removed drives. Use the `zpool online` command with the pool name and the GUID of the missing disk as arguments. If the disk in my example pool were merely disconnected, I could reactivate it like so:

```
# zpool online db 14398195156659397932
```

ZFS resilers the drive and resumes normal function.

If you want to remove a drive, you can tell ZFS to take it offline with `zpool offline`. Give the pool and disk names as arguments.

```
# zpool offline db gpt/zfs6
```

Bringing disks offline, physically moving them, bringing them back online, and allowing the pools to resilver will let you migrate large storage arrays from one SAS cage to another without downtime.

# Replacing Drives

If the drive isn’t merely loose but flat-out busted, you’ll need to replace it with a new drive. ZFS lets you replace drives in several ways, but the most common is using `zpool replace`. Use the pool name, the failed provider, and the new provider as arguments. Here, I replace the db pool’s `/dev/gpt/zfs3` disk with `/dev/gpt/zfs6`:

```
# zpool replace db gpt/zfs3 gpt/zfs6
```

The pool will resilver itself and resume normal operation.

In a large storage array, you can also use successive `zpool replace` operations to empty a disk shelf. Only do this if your organization’s operation requirements don’t allow you to offline and online disks.

# Boot Environments