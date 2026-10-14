
```
# volplex -v cluster_usarvol dis cluster_usarvol-03
# voledit -rf rm cluster_usarvol-03
```

```
# volplex -v cluster_varvol dis cluster_varvol-03
# voledit -rf rm cluster_varvol-03
```

Add in the new log plexes from a different disk with the root disk group.

```
# volassist addlog cluster_usarvol dsk5h
# volassist addlog cluster_varvol dsk5h
```

8. Verify that everything completed successfully.

```
# volprint cluster_rootvol cluster_usarvol cluster_varvol
Disk group: rootdg

TY NAME            ASSOC        KSTATE   LENGTH   PLOFFS   STATE   TUTIL0  PUTIL0
v  cluster_rootvol  cluroot      ENABLED  1048576  -        ACTIVE  -       -
pl cluster_rootvol-01 cluster_rootvol ENABLED 1048576 - ACTIVE - -
ad dsk6-01        cluster_rootvol-01 ENABLED 1048576 0 - - -
pl cluster_rootvol-02 cluster_rootvol ENABLED 1048576 - ACTIVE - -
ad dsk7-01        cluster_rootvol-02 ENABLED 1048576 0 - - -

v  cluster_usarvol  fagen       ENABLED  8389344  -        ACTIVE  -       -
pl cluster_usarvol-01 cluster_usarvol ENABLED 8389344 - ACTIVE - -
ad dsk6-02        cluster_usarvol-01 ENABLED 8389344 0 - - -
pl cluster_usarvol-02 cluster_usarvol ENABLED 8389344 - ACTIVE - -
ad dsk7-02        cluster_usarvol-02 ENABLED 8389344 0 - - -
pl cluster_usarvol-03 cluster_usarvol ENABLED LOGONLY - ACTIVE - -
ad dsk5h-01       cluster_usarvol-03 ENABLED 195 LOG - - -

v  cluster_varvol   fagen       ENABLED  8323280  -        ACTIVE  -       -
pl cluster_varvol-01 cluster_varvol ENABLED 8323280 - ACTIVE - -
ad dsk7-03        cluster_varvol-01 ENABLED 8323280 0 - - -
pl cluster_varvol-02 cluster_varvol ENABLED 8323280 - ACTIVE - -
ad dsk6-04        cluster_varvol-02 ENABLED 8323280 0 - - -
pl cluster_varvol-03 cluster_varvol ENABLED LOGONLY - ACTIVE - -
ad dsk5h-02       cluster_varvol-03 ENABLED 195 LOG - - -
```

## 14.7.2 Encapsulate Using the volencap(8) Command

When you use the volencap command to encapsulate an AdvFS domain, disk, or disk partition, the data that exists on the device is left unchanged. This is a good thing because if you decide to remove LSM you will not have to recreate or restore your data.

The volencap command expects as input a partition, disk, or domain:

- If you choose to have an individual disk partition encapsulated, a nopriv disk and an LSM volume are created from the disk partition.
- If you choose to have an entire disk encapsulated, a nopriv disk and an LSM volume are created for each partition on the disk that is not marked unused.
- If you choose to have an AdvFS domain encapsulated, all AdvFS volumes in the domain become LSM volumes.

The volencap command creates files in the /etc/vol/reconfig.d directory that are used by the volreconfig(8) command to create the LSM volumes, plexes, and subdisks from the devices that were input to the volencap command.

### 14.7.2.1 Encapsulating an AdvFS Domain

Any domain except for the cluster_root domain can be encapsulated. To place the cluster_root domain under LSM control, you must use the volmigrate command (see section 14.7.1 earlier in this chapter).

As long as the domain is not in use, encapsulation does not require a reboot. If you can, unmount the file systems in the domain you want to encapsulate so that you can avoid having to reboot the cluster.

To encapsulate a domain, do the following:

```
# volencap tcrhb

Setting up encapsulation for tcrhb.
For AdvFS domain tcrhb:
  - Creating nopriv disk dsk6c.

The following disks are queued up for encapsulation or use by LSM:
dsk6c

Please consult the Cluster Administration Guide for steps
that you will need to follow to complete the encapsulation.
```

You can see which devices are scheduled for encapsulation by issuing the volencap command with the "-s" switch:

```
# volencap -s

The following disks are queued up for encapsulation or use by LSM:
dsk6c
```

In order for the encapsulation process to complete, we need to run the volreconfig command.

# NOTE:

If you decide not to finish the encapsulation process, you cancel the encapsulation for one device by using the volencap command with the "-k <diskname|partition>" switch or cancel all queued encapsulation requests with the "-k -a" switch:

```
# volencap -k dsk6c
```

-OR-

```
# volencap -k -a
```

The volreconfig command completes the encapsulation process provided that the devices that are queued for encapsulation are not in use.

```
# volreconfig
Encapsulating dsk6c.
The following disks were encapsulated successfully:
    dsk6c
```

You can verify that the encapsulation succeeded by using the volprint command.

```
# volprint | grep dsk6
dm dsk6c-AdvFS fsg6c      -      17773524 -      -      -
v  vol-dsk6c   fsg6en    ENABLED 17773524 -      ACTIVE -      -
pl vol-dsk6c-01 vol-dsk6c ENABLED 17773524 -      ACTIVE -      -
sd dsk6c-01   vol-dsk6c-01 ENABLED 17773524 0      -      -      -
```

You can also verify that the domain volume links were updated with the fln function (or you can use an "ls -l" command).

```
# fln /etc/fdmns/tcrhb
rootdg,vol-dsk6c -> /dev/vol/rootdg/vol-dsk6c
```

### 14.7.2.1.1 Encapsulating cluster_usr or cluster_var

The major difference between encapsulating any other domain and the cluster_usr or cluster_var domains is simply that /usr and /var cannot be unmounted. In other words, in
