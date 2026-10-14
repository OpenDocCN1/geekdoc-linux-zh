
```
# disklabel -r disk5 | grep -v '  part'
8 partitions:
#        size       offset     fstype  fsize  bsize  cpg  # ~Cyl values
 a:     1293637          0       unused     0      0    # 0 - 385*
 b:     3906059    1293637       unused     0      0    # 385* - 1557*
 c:    17773524    5230330       unused     0      0    # 0 - 5289*
 d:     3389144    5234331       unused     0      0    # 1557* - 2566*
 e:     4180140    8623475       unused     0      0    # 2566* - 3810*
 f:     6499090   12803615       unused     0      0    # 3810* - 5289*
 g:     5959156    5234331       unused     0      0    # 1557* - 3810*
 h:     6580037   11193447       LSMsimp     0      0    # 3331* - 5289*
```

Partition “a” looks large enough, so we will use it.

- 2. Backup the data in the domain — just in case.

- 3. Define the disk within LSM.

```
# voldisksetup -i disk5a
```

- 4. Add the disk to the rootdg.

```
# vxdg adddisk clu_rootdg=disk5a
```

- 5. Migrate!

```
# volligrate cluster_root clu_root
volassist -Uclu_root make cluster_rootvol 1048576 clu_root init=active nlog=0
addvol /dev/vol/vol cluster_rootvol cluster_root
rmvol /dev/dsk/dsk1a cluster_root
rmvol: Removing volume '/dev/disk/dsk1a' from domain 'cluster_root'
rmvol: Removed volume '/dev/disk/dsk1a' from domain 'cluster_root'
```

- 6. Verify that the migration succeeded.
  - Check the cluster_root domain.

```
# showdomain cluster_root

                                Id              Date Created  LogPgs  Version  Domain Name
3acde49b.0004e69c  Fri Apr  6 11:45:31 2001     512       4      cluster_root

Vol     512-Blks             Free  % Used  Cmode  Rblks  Wblks  Vol Name
  2L    1048576          644608     39%     on    65536  65536  /dev/vol/rootdg/clust
                                                                 er_rootvol
```

The cluster_root domain is now using the LSM volume, "cluster_rootvol" device special file located in the /dev/vol/rootdg directory.

- Check LSM.

```
# volprint -aht cluster_rootvol
Disk group: rootdg

V NAME        USETYPE  KSTATE  STATE   LENGTH  READPOL  PREFPLEX
PL NAME       VOLUME   KSTATE  STATE   LENGTH  LAYOUT   NCOL/WID MODE
SD NAME       PLEX     DISK    DISKOFFS LENGTH  [COL/OFF DEVICE MODE
v  cluster_rootvol cluroot  ENABLED ACTIVE 1048576 SELECT  -  -
pl cluster_rootvol-01 cluster_rootvol ENABLED ACTIVE 1048576 CONCAT -  RW
sd clu_root-01 cluster_rootvol-01 cluster_root 0 1048576 0  dak5a  ENA
```

# NOTE:

If for some reason you want to reverse your migration decision, you can use the volumigrate command. In the following example, we will move the cluster_root domain back to the original partition.

```
# volumigrate cluster_root dskla
addvol /dev/disk/dskla cluster_root
rmvol /dev/vol/rootdg/cluster_rootvol cluster_root
rmvol: Removing volume '/dev/vol/rootdg/cluster_rootvol' from domain 'cluster_root'
rmvol: Removed volume '/dev/vol/rootdg/cluster_rootvol' from domain 'cluster_root'
voledit -g rootdg -rf rm cluster_rootvol
```

```
# voldg rmdisk clu_root
```

```
# voldisk rm dak5a
```

The cluster_root domain is back to its original device.

## 14.7.1.1 Migrate and Mirror the Cluster-Common File Systems

One of the main reasons for the volmigrate command is to provide an online process to migrate the cluster_root domain as we illustrated earlier in this section. Why is this important? To avoid having to shutdown the entire cluster.

Adding support for cluster_root (and swap) in V5.1A allows for lower cost cluster configurations by utilizing LSM to mirror the cluster-common domains across buses for a NSPOF failure solution.

So, we thought, if you have a cluster without a multiple-bus, dual-redundant hardware RAID controller, you might like to see an example of mirroring your cluster-common devices using LSM.

Here are the steps you will need to take:

- 1. Locate a disk (or disks) large enough to migrate cluster_root, cluster_usr, and cluster_var domains.
  - Ideally, you will want the disk(s) to be on a shared bus other than the bus where the cluster-common domains are currently located. Additionally, choose the disk(s) at least the same size as the current cluster-common disk(s) so that you can reuse the original cluster-common disk(s) as the mirror.
  - Our cluster-common domains are on the same disk, so we will be using another disk of the same size for the remainder of this example.

- 2. Save the disk label in case you want to go back to the original (non-LSM) configuration.

```
# disklabel -r dsk1 > /dsk1_noLSM.lbl
```

- 3. Add the disk(s) to LSM that you will be using as your destination disks.
  - In this case, we will be using dsk6. We are going to use the entire disk and let LSM create the volumes it needs instead of splitting the disk into separate partitions for each domain.

```
# voldisksetup -i dsk6
```

- 4. Add the disk(s) to the root disk group.

```
# voldg adddisk dsk6
```

- 5. Migrate the cluster-common domains (this may take a while – be patient).

```
# volmigrate cluster_root dsk6
volassist -Uclu root make cluster_rootvol 1048576 dsk6 init=active nlog=0
addvol /dev/vol/rdg/cluster_rootvol cluster_root
rmvol /dev/disk/dsk1b cluster_root
rmvol: Removing volume '/dev/disk/dsk1b' from domain 'cluster_root'
rmvol: Removed volume '/dev/disk/dsk1b' from domain 'cluster_root'
```
