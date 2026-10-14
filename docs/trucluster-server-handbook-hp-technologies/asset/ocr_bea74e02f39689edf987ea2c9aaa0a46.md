# NOTE:

An rc.config.site file is supported but Tru64 UNIX doesn't ship this file by default and the system administrator would have to create and maintain it.

Let's also take a quick peek at rc.config.common to see the sorts of variables defined there.

```
...
NUM_NFSIOD="7"
export NUM_NFSIOD
NFS_CONFIGURED="1"
export NFS_CONFIGURED
NFSSERVING="1"
export NFSSERVING
...
NIS_DOMAIN="BRAVO"
export NIS_DOMAIN
NIS_ARGS="-s -S OSD, fathom.abc.net, reverse.abc.net"
export NIS_ARGS
NIS_SERVERARGS="**"
export NIS_SERVERARGS
SECURITY="BASE"
export SECURITY
...
```

Things like security settings, NIS setup, NFS, etc. are common to the cluster, and it makes sense that they would be in a cluster-common variable definition file. The important point here is that there are two files to keep in mind when setting and checking variable definitions.

For more on rc.config, check back to Chapters 6 and 12.

# 21.6 Clusterwide cron

One area of cluster confusion involves the cron(8) daemon. The crontab files for each member (found in /var/spool/cron/crontabs) are member-specific — /var/spool/cron is a CDS L.

```
# fin /var/spool/cron
/var/spool/cron -> ../cluster/members/(memb)/spool/cron
```

Not only are the crontab files member-specific, but the cron daemon is also not cluster-aware.