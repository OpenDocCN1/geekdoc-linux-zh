14. Unmount the member boot partition.

```
# cd /
# umount /mnt
```

15. Create the .bak (backup) database files.

```
# cd /etc
# for i in dec_*db
> do
> cp $i $i.bak
> done
```

16. Reboot to single-user mode using the ER disk as the boot device. The system will now boot with the same hardware configuration that the cluster previously had.

```
>>> boot -fl s DEB100
```

17. Scan the SCSI buses.

```
# hwsmgr -scan scsi
```

18. Mount the root file system as read/write.

```
# mount -u /
```

19. Verify and update the device database.

```
# dsfmgr -v -F
```

20. Display and note the current device layout.

```
# hwsmgr -view devices
```

21. Fix the local file domains, if necessary, by removing and remaking the correct links in the /etc/fdms directory. Examine usr_domain, root1_domain, and cluster_root to see if any changes are necessary based on the output from step 20. If you need to make changes follow this example:

```
# cd /etc/fdms/cluster_root
# rm *
# ln -s /dev/disk/dsk1la
```