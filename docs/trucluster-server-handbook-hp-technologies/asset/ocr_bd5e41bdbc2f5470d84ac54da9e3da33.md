```
# cnxread -l dsk2

The CNX Partition info for /dev/rdisk/dsk2h. This is a member boot disk.
Cluster Root Filesystem (AdvFS) Segment Information

Magic #: 0x42534, Sequence #: 116

      maj,min
      ----
Devices: [ 1]: 40, 5

CLBN Segment Information

Magic #: 0x4185, Sequence #: 22, Version 3.1

      maj,min
      ----
Devices: [ 1]: 19,128   dsk5h (simp)
        [ 2]: 19,142   dsk6g (simp)
        [ 3]: 19,126   dsk5g (simp)
```

In our cluster, dsk5g and dsk6g are the two plexes in a mirrored volume that are used for cluster_root. The first device listed (dsk5h) is the private region disk in the rootdg. We are not exactly sure why it shows up because it is not in the cluster_root volume, but it does appear that any device in the rootdg will show up in the output.

```
# volprint -g rootdg
TY NAME          ASSOC        KSTATE   LENGTH   PLOFFS   STATE   TUTIL0  PUTIL0
dg rootdg        rootdg       -        -        -        -       -       -
dm clu_mroot     dsk5g        -        8686058  -        -       -       -
dm clu_root      dsk6g        -        8686058  -        -       -       -
dm dsk5h         dsk5h        -        8686058  -        -       -       -
v  cluster_rootvol cluroot  ENABLED 1048576  -        ACTIVE  -       -
pl cluster_rootvol-01 cluster_rootvol ENABLED 1048576  -   ACTIVE  -       -
sd clu_mroot-01 cluster_rootvol-01 ENABLED 1048576 0   -       -       -
pl cluster_rootvol-02 cluster_rootvol ENABLED 1048576  -   ACTIVE  -       -
sd clu_root-01 cluster_rootvol-02 ENABLED 1048576 0   -       -       -
```