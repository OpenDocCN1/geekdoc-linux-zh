where the command argument(s) are usually UUID or TAG, which are the unique identifier or name of a jail.

# Listing:

```
iocage activate ZPOOL
 iocage cap UUID|TAG
 iocage chroot UUID|TAG [command]
 iocage clean [-a|-b|-j]
 iocage clone UUID|TAG [UUID|TAG@snapshot] [property=value]
 iocage console UUID|TAG
 iocage create [-e] [base=[RELEASE|NAME]] [pkglist=file] [property=value]
 iocage deactivate ZPOOL
 iocage defaults
 iocage destroy [-f] UUID|TAG
 iocage df
 iocage exec [-u username | -U username] UUID|TAG|ALL command [arg ...]
 iocage export UUID|TAG
 iocage fetch [release=RELEASE | ftphost=ftp.hostname.org | ftpdir=/dir/ | ftpfiles="base.txz doc.txz lib32.txz src.txz"]
 iocage get property|all UUID|TAG
 iocage help
 iocage import UUID [property=value]
 iocage init-host IP ZPOOL
 iocage inuse UUID|TAG
 iocage limits [UUID|TAG]
 iocage list [-b|-t|-r]
 iocage package UUID|TAG
 iocage promote UUID|TAG
 iocage rboot
 iocage reboot UUID|TAG
 iocage rcshutdown
 iocage record start|stop UUID|TAG
 iocage reset UUID|TAG|ALL
 iocage restart UUID|TAG
 iocage rollback UUID|TAG@snapshotname
 iocage runtime UUID|TAG
 iocage set property=value UUID|TAG
 iocage show property
 iocage snaplist UUID|TAG
 iocage snapremove UUID|TAG@snapshotname|ALL
 iocage snapshot [-r] UUID|TAG [UUID|TAG@snapshotname]
 iocage start UUID|TAG
 iocage stop UUID|TAG|ALL
 iocage uncap UUID|TAG
```