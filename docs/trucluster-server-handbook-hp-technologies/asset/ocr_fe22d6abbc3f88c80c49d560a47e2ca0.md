# 12.3.2.3 What hwmgr Command Options Have Focus?

The easiest way to determine whether a command option can be focused clusterwide or redirected to another member is to ask hwmgr with the "-help" option. For example, say we want to scan for new hardware but want to ensure that we perform the scan clusterwide.

```
# hwmgr -help scan
Usage: hwmgr -scan component [ -id <hardware-component-ID> ]
    [ -category <hardware-category> ]
    [ -recurs ]
    [ -instance <member-instance-number> ]
    [ -member <cluster-member-name> ]
    [ -cluster ]
Usage: hwmgr -scan [name] -entry <hardware-name>
    [ -member <cluster-member-name> ]
    [ -cluster (scan cluster-wide) ]
Usage: hwmgr -scan scsi
    [ -bus <scsi-bus> ]
    [ -target <scsi-target> ]
    [ -lun <scsi-lun> ]
    [ -member <cluster-member-name> ]
```

According to the help output, the "hwmgr -scan component" command provides a member or a cluster option, whereas the "hwmgr -scan scsi" command only provides a member option. Table 12-3 shows the various hwmgr commands and whether or not they can be directed to the cluster or an alternate member.

> NOTE:
> We have written a script to run the "hwmgr scan scsi" command on every member. The clu_scan_scsi script is available at the TruCluster Server Handbook website (see Appendix B for the URL).

# 12.3.3 The dsfmgr(8) Command Revisited

When using the dsfmgr command in cluster, there are a few things to keep in mind:

+   - When adding a device class, specify a "c" as the entry_type to indicate that the device will have a clusterwide scope.

```
# dsfmgr -a class guitar c 755
```

See the last line of the following output for the results of the previous command.