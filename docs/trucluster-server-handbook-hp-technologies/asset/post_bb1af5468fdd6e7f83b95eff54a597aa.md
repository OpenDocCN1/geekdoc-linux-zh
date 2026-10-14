
2. Deport the disk group from LSM on the standalone system.

```
# volume -g mydg stopall
```

```
# voldg deport mydg
```

3. Disconnect the storage from the standalone system.

4. Connect the storage to the cluster.

5. Scan the SCSI bus on each cluster member.

```
[sheridan]
# hwmgr -scan scsi -bus 3
```

```
[sheridan]
# hwmgr -scan scsi -bus 3 -member molari
```

6. Create the device special files (if necessary).

```
# devmgr -K
```

7. Determine the new device names.

```
# hwmgr -show scsi -bus 3
```

8. Rebuild the LSM volume device nodes.

```
# voldctl enable
```

9. Import the disk group.

- If the disk group is from a V3.2 through V4.0G standalone system and not the rootdg:

```
# voldg -o shared -o convert_old -fc import mydg
lsm:voldg: WARNING: Volume myvol: Temporarily renumbered due to conflict
```

If the disk group is from a V3.2 through V4.0G standalone system and is the rootdg, you will need to rename the disk group because the cluster already has a rootdg. Before you can import a disk group you will be renaming, you must determine the disk group identifier (DGID) of the standalone system's rootdg.

```
# voldisk list dsk10 | grep group
group: name=rootdg id=999905375.1022.delenn
```

Import the disk group with a new disk group name. We'll use "mydg."

```
# voldg -o shared -o convert_old -n mydg -fc import id=999905375.1022.delenn
```

10. Start the volume.

```
# volprint -Aht myvol
Disk group: mydg
V NAME USERTYPE KSTATE STATE LENGTH READPOL PREFLEX
PL NAME VOLUME KSTATE STATE LENGTH LAYOUT NCOL/WID MODE
SD NAME PLEX DISK DISKOFFS LENGTH [COL/]OFF DEVICE MODE
v myvol fsgn DISABLED CLEAN 2097152 SELECT -
p1 myvol-01 myvol DISABLED CLEAN 2097152 CONCAT - RW
sd mydg_01-01 myvol-01 mydg_01 0 2097152 0 dsk10 ENA
```

```
# volume -g mydg startall
```

For additional information, see the Logical Storage Manager manual or the volume(8), voldisk(8), voldg(8), volrecover(8), and volsave(8) reference pages.

## 14.6.2 Importing a Disk Group from a Cluster to a Standalone System

### 14.6.2.1 From TruCluster Server to a V5.0+ Standalone System

The procedure for going from a cluster to a standalone system running Tru64 UNIX version 5.0 or newer is almost the same procedure as described in section 14.6.1.1 the only difference occurs at Step 8. Use the following command:

```
# voldg -o private -c import mydg
```

## 14.6.2.2 From TruCluster Server to a V3.2 through V4.0G Standalone System

### CAUTION:

This procedure will not work if the disk group did not originate on a system that had a vols ave performed prior to moving the data to the TruCluster Server environment. This procedure is really a recovery procedure and not to be used to move disk groups back and forth between the pre-V5.0 operating system environments.

If you are moving the disk group back to a standalone system running Digital UNIX version 3.2 through 4.0E, or Tru64 UNIX version 4.0F through 4.0G, you need to restore the metadata from a backup. Replace Steps 5–10 in section 14.6.1.2 with the following procedure:

- 5. Scan the SCSI bus on each cluster member.

```
# scu scan edt
```

- 6. Restore the LSM configuration.

```
# volrestore -i -g mydg -d /MyLSMbackupDirectory
```

- 7. Initialize the volumes in the disk group to a CLEAN state (repeat as necessary).

```
# volume -g mydg init clean myCoolVolume myMultiPlex
```

- 8. Start all of the volumes in the disk group.

```
# volume -g mydg startall
```

For additional information, see the Logical Storage Manager Guide or the volume(8), voldg(8), and volrestore(8) reference pages.

## 14.6.3 Importing a Disk Group from a Cluster to a Cluster

### 14.6.3.1 From TruCluster Server to TruCluster Server

The procedure for going from a cluster to a cluster running TruCluster Server version 5.0A or newer is almost the same procedure as described in 14.6.1.1; the only difference is at Step 8. Use the following command:

```
# voldg -C import mydg
```

### 14.6.3.2 From TruCluster Version 1.5 or 1.6 to TruCluster Server

Importing a disk group from a cluster running TruCluster version 1.5 or 1.6 should be done using the clu_migrate_* scripts included in the TCRMIGRATE subset that ships with TruCluster Server version 5.0A (or newer). We will discuss migrating from V1.5 or V1.6 as well as those clu_migrate_* scripts in chapter 26.

## 14.7 To Migrate or Encapsulate? That is the Question

In this section, we will discuss when you may want or need to migrate versus when you may want or need to encapsulate.

- When you migrate an AdvFS domain to an LSM volume, you are actually moving your data from the storage currently associated with the domain to an LSM volume composed of different underlying storage. To migrate an AdvFS domain to LSM, use the volmigrate command. Conversely, to migrate from LSM to an AdvFS domain, use the volumigrate command.
  
- Prior to TruCluster Server version 5.1A, the volmigrate and volumigrate commands did not exist, so migrating an AdvFS domain would have to be done manually using one of two methods: either backing up and restoring the data from each file system in the domain to an LSM volume, or using the addvol(8) command to add an LSM volume to the AdvFS domain and then removing the non-LSM volume with the rmvol(8) command. But even these methods were not supported for the cluster_root file system.
  
- Notice that we mention only AdvFS domains with regard to migration because the volmigrate command only supports AdvFS domains.
  
- You can migrate a domain while the cluster is up and running – no reboot is required!

- When you encapsulate a disk, a disk partition, or an AdvFS domain, the underlying storage becomes LSM volumes. Unlike migration, encapsulation does not require additional storage because the current storage is simply brought under LSM control. To encapsulate a disk, a disk partition, or an AdvFS domain, use the volencap command.
  
- If you encapsulate a disk, a disk partition, or an AdvFS domain that is currently in use, encapsulation will not be completed until a reboot is performed. If, however, the device(s) are dormant, the encapsulation can be completed without a reboot.
