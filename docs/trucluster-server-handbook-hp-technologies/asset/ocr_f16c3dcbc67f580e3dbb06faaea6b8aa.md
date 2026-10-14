may seem, it is reasonable. But it serves to emphasize that CDSLs can potentially be a problem in an exported file system.

```
# file /etc/rc.config
/etc/rc.config: symbolic link to ../cluster/members/{memb}/etc/rc.config
```

```
# grep "HOSTNAME=" /cluster/members/member?/etc/rc.config
/cluster/members/member0/etc/rc.config:HOSTNAME="molari.dec.com"
/cluster/members/member1/etc/rc.config:HOSTNAME="molari.dec.com"
/cluster/members/member2/etc/rc.config:HOSTNAME="sheridan.dec.com"
```

From a client system, mount the cluster's /etc directory.

```
# mount babylon5:/etc /mnt
```

```
# grep "HOSTNAME=" /mnt/rc.config
HOSTNAME="delenn.dec.com"
```

# 20.4.2.2 Excluding Members from NFS Server Responsibilities

If desired, some members may be excluded from the duties of NFS serving using the "sysman" with the "-focus" option (see the TruCluster Server Cluster Administration Guide for more information). By focusing the configuration utility (sysman or nfsconfig) on a particular member, it will override the cluster-wide configuration. So you can configure the cluster as an NFS server but then exclude certain members if you prefer. The following output shows that the NFS serving variables are normally reflected in the /etc/rc.config.common file, but if the member is reconfigured as a member-specific NFS server, the variables appear in the member-specific /etc/rc.config file.

```
# grep -i nfs /etc/rc.config /etc/rc.config.common
/etc/rc.config.common:NUM_NFSIOD="7"
/etc/rc.config.common:export NUM_NFSIOD
/etc/rc.config.common:NFS_CONFIGURED="1"
/etc/rc.config.common:export NFS_CONFIGURED
/etc/rc.config.common:NFSSERVING="1"
/etc/rc.config.common:export NFSSERVING
/etc/rc.config.common:NFSLOCKING="1"
/etc/rc.config.common:export NFSLOCKING
/etc/rc.config.common:PCNFSD="0"
/etc/rc.config.common:export PCNFSD
```