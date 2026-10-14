# NOTE:

If the mounting member fails, the NFS mount disappears and another member will not automatically become the new NFS client/CFS server unless automount(8) (V5.0A-V5.1A) or autofs(8) (V5.1-V5.1B) is configured.

```
# mount -t nfs
/usr/patches@delenn on /patches type nfs (v3, ro, nosuid,udp, hard, intr)
```

```
# cfsmgr /patches
Domain or filesystem name = /patches
Server Name = molari
Server Status : OK
```

```
# ls -l /patches
T64V51AB01AS0001-20020116.tar.gz
T64V51AB02AS0002-20020513.tar.gz
```

# 20.4.1.1 AutoFS

Note that the failure of a client member that has mounted a remote file system and is providing access (through CFS) to the remote file system to all other cluster members causes all members to lose access to the remote file system. AutoFS became available in Tru64 UNIX version 5.1 as a higher availability option to the automount command. HP recommends using AutoFS as an "automount" mechanism whereby remote file systems are automatically mounted upon reference. More importantly, if AutoFS is configured in a cluster, it will be configured (using CAA) such that automatic failover of the mounted file system can be arranged.

```
# caa_stat -t autofs
Name          Type        Target    State    Host
---------------------------------------------------
autofs        application ONLINE    ONLINE    molari
```

Note that this is based on client side activities (NFS mounting is done only on the client). For more information on AutoFS, see the Tru64 UNIX Network Administration Guide: Services (the Network Administration Guide was split into two books in V5.1A) in the documentation set.

An interesting alternative to autofs exists. It involves creating a CDSL (which will be cluster-wide) and using the CDSL as the NFS mount point. The advantage to this is that there will be a