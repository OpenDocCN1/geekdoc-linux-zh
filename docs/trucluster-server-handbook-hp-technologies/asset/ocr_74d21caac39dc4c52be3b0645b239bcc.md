# 8. Import the disk group.

+   If the disk group is not the rootdg (Note: the "-f" switch may also be necessary if not every disk in the disk group is available):

```
# voldg -o shared -c import mydg
```

+   If the disk group was the rootdg on the original system, you will need to rename the disk group because the cluster already has a rootdg.

Before you can import the root disk group, you must determine the disk group identifier (DGID) of the standalone system's rootdg.

```
# voldisk list dsk10 | grep group
group: name=rootdg id=999905375.1022.delemn
```

Import the disk group with a new disk group name. We'll use "mydg."

```
# voldg -o shared -n mydg -c import id=999905375.1022.delemn
```

# 9. Recover the volumes for the disk group in the background.

```
# volrecover -ab -g mydg
```

# 14.6.1.2 From Tru64 UNIX Prior to Version 5.0

# 1. Save the LSM configuration.

While saving the LSM configuration is always a good idea, it is particularly important if you are moving a disk group from a system running Digital UNIX version 3.2 through 4.0E, or Tru64 UNIX version 4.0F through 4.0G, because you may need to move it back. Once a disk group is imported into LSM on a system running Tru64 UNIX version 5.0 or newer, the metadata is converted to the new format and is no longer compatible with the older format. It is possible to restore the metadata to the older, pre-V5 format provided you have the older format backed up and you did not make subsequent metadata changes (e.g., detaching or moving data plexes).

```
# volsave -d /MyLSMbackupDirectory
```