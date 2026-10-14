
Now mount the second fileset partitioned.

```
# mount -o server_only tcrhb#lola /lola
Cannot mount fileset server_only when existing domain is not.
tcrhb#lola on /lola: Function not implemented
```

The second fileset is prevented from being mounted at all. Unmount the file system so that we can mount it "-o server_only" next.

```
# umount /fafrak
```

## 13.4.2.3.2 The First Fileset is Mounted "-o server_only"

This time we will mount the first fileset partitioned.

```
# mount -o server_only tcrhb#fafrak /fafrak
```

The subsequent mounts will not fail but will also be partitioned. For example:

```
# mount tcrhb#lola /lola
WARNING: Domain is already specified server_only so this mount will be.
```

```
# mount | grep server_only
tcrhb#fafrak on /fafrak type advfs (rw, server_only)
tcrhb#lola on /lola type advfs (rw, server_only)
```

Alternatively, you could use the output of cfs command piped into the grep command – the advantage being that you can also see which member is the server of the partitioned file system.

```
# cfs | grep @
molari      @ /fafrak      tcrhb#fafrak          AdvFS
molari      @ /lola        tcrhb#lola            AdvFS
```

## 13.4.2.4 Mounting a File System Beneath a Partitioned File System’s Mount Point

What happens when you attempt to mount a file system underneath a partitioned file system’s mount point? You get an error – really, no kidding. Don’t believe us? Okay, how about if we prove it?

```
[sheridan]
# mount -o server_only tcrhb#fafrak /fafrak
```

```
[sheridan]
# mount extra#kits /fafrak/kits
extra#kits on /fafrak/kits: Permission denied
```

## 13.4.2.5 Attempting a Mount Update

You cannot mount update a file system to make it "-o server_only". For example:

```
[sheridan]
# umount /fafrak
```

```
[sheridan]
# mount tcrhb#fafrak /fafrak
```

```
[sheridan]
# mount -u -o server_only /fafrak
Cannot update existing mount to be server-only.
```

If you want to change a mounted file system from a cluster-wide mount to a partitioned mount, then you must unmount the file system and mount the file system "-o server_only".

You can, however, mount update a file system from read-only mode to read-write mode. Let's remount the tcrhb#fafrak file system "-o server_only, ro", so that we can attempt to update the mount to be read-write.

```
[sheridan]
# umount /fafrak
```

```
[sheridan]
# mount -o server_only,ro tcrhb#fafrak /fafrak
```

```
[sheridan]
# mount | grep fafrak

tcrhb#fafrak on /fafrak type advfs (ro, server_only)
```

```
[sheridan]
# mount -u /fafrak
WARNING: Domain is already specified server_only so this mount will be.
```

```
[sheridan]
# mount | grep fafrak
tcrhb#fafrak on /fafrak type advfs (rw, server_only)
```

## 13.5 Quotas

Tru64 UNIX provides quota support on three levels:

- User
- Group
- Fileset (AdvFS-only)

The TruCluster Server has always supported fileset quotas, but user and group quota support was not added until V5.1A.

In order to keep quota support from adversely affecting the cluster file system's performance, a compromise was made in quota enforcement. The compromise is that it is possible for a user or group to exceed its quota by up to the quota_excess_blocks attribute in the cfs subsystem. By default, this value is set to 1 MB per member – so on an eight-node cluster any user or group may exceed its quota by up to 8 MB. The quota_excess_blocks attribute can be reconfigured while the system is running (notice the "R" in the "op" field in the following example).

```
# sysconfig -Q cfs quota_excess_blocks
cfs:
quota_excess_blocks - type=ULONG op=CRQ min_val=0 max_val=18446744073709551615
```

The attribute value is expressed in kilobytes as you can see in the next example.

```
# sysconfig -q cfs quota_excess_blocks
cfs:
quota_excess_blocks = 1024
```

If you want to increase the value to 2 MB, for example, you can use the following command:

```
# sysconfig -r cfs quota_excess_blocks=2048
quota_excess_blocks: reconfigured
```
