```
*****  Checking daemons on members  *****
*****
*****  Checking member molari-ics0 daemons
        aliasd is RUNNING
        aliasd_niff is RUNNING
        /sbin/klroadsrv is RUNNING
        /usr/sbin/evmd is RUNNING
        /usr/sbin/nifd is RUNNING
        /usr/sbin/portmap is RUNNING
        /usr/sbin/caad is RUNNING
        /usr/sbin/clu_wal1 is RUNNING
        /usr/sbin/xntpd is RUNNING
        /usr/sbin/gated is RUNNING
        /usr/sbin/clu_mibs is RUNNING
        /usr/sbin/rdginit is RUNNING
        /usr/sbin/snmpd is RUNNING
        /usr/sbin/syslogd is RUNNING
        /usr/sbin/binlogd is RUNNING
        /usr/sbin/mountd is RUNNING
        /usr/sbin/nfsd is RUNNING
        /usr/sbin/smnsd is RUNNING
        /usr/sbin/clu_wal1 is RUNNING
        /usr/sbin/xntpd is RUNNING
        /usr/sbin/gated is RUNNING
        /usr/sbin/clu_mibs is RUNNING
        /usr/sbin/rdginit is RUNNING
        /usr/sbin/snmpd is RUNNING
        /usr/sbin/syslogd is RUNNING
        /usr/sbin/binlogd is RUNNING
        /usr/sbin/mountd is RUNNING
        /usr/sbin/nfsd is RUNNING
        /usr/sbin/smnsd is RUNNING
*****
*****  Checking the synchronization between members  *****
*****
molari-ics0: delay:0.000976 offset:0.000488  Sun Apr 21 00:59:10 2002

check_cds1_config : Checking installed CDSLs
check_cds1_config : Successfully verified CDSL configuration
```

# 10.5.2  Check the Connection Manager Subsystem

Let’s now check the Connection Manager subsystem. The clu_get_info(8) command provides detailed information about the cluster and all the cluster members. This command is also executed from the clu_check_config command.