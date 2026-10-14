7. Restore cluster_root from backup.

```
# vrestore -xf /dev/tape/tap2 -D /mnt
# umount /mnt
```

8. Restore cluster_usr and cluster_var by repeating steps 6 and 7 but for the cluster_usr#usr and cluster_var#var filesets. (Or you could leave cluster_root mounted and mount these filesets at /mnt/usr and /mnt/var respectively and restore them.)

9. Re-mount cluster_root if you unmounted it in step 7.

```
# mount cluster_root#root /mnt
```

10. Copy the restored cluster databases and member-specific databases to /etc on the ER disk so that when you reboot from the ER disk you will have the proper (cluster) view of storage.

```
# cd /mnt/etc
# cp dec_unid_db dec_hwc_db dfsc.dat /etc
# cd /mnt/cluster/members/member1/etc
# cp dfs1.dat /etc
```

11. Create the links in /etc/fdmns for the member boot disk if you don't already have them.

```
# cd /etc/fdmns
# mkdir root1_domain
# cd root1_domain
# ln -s /dev/disk/dsk6a
```

12. Mount the member boot partition.

```
# cd /
# umount /mnt
# mount root1_domain#root /mnt
```

13. Copy the databases from the member boot partition to /etc on the ER disk so that when you reboot from the ER disk you will have the proper (cluster) view of storage.

```
# cd /mnt/etc
# cp dec_devaw_db dec_hw_db dec_hwc_ldb dec_scsi_db /etc
```