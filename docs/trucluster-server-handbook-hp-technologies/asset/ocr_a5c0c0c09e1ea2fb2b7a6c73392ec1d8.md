27. Take note of the major and minor numbers of the new cluster_root device.

```
# file /dev/disk/dsk2la
/dev/disk/dsk2la:    block special (19/467)
```

28. Boot the member boot disk interactively specifying the major and minor numbers (above) for the newly restored cluster_root.

```
>>> boot -flags "1a"
Enter: <kernel_name> [option_1 ... option_n]
or: ls [name]['help'] or: 'quit' to return to console
Press Return to boot 'vmunix'
```

```
# vmunix cfs:cluster_root_dev1_maj=19 cfs:cluster_root_dev1_min=467
```

# NOTE:

In cluster_root_dev#_maj and cluster_root_dev#_min, the "#" can range from 1 to 3, meaning that you can have from 1 to 3 AdvFS volumes in cluster_root.

29. Boot each cluster member one at a time.

# 22.2.1.3 Emergency Repair Disk

As mentioned in the previous section, to restore cluster_root you must have a bootable non-clustered operating system disk at the same operating system version and patch level as the current cluster. Our recommendation is that when you install a patch kit on your cluster, you always copy the patch kit tar(1) file to a file system on the Emergency Repair (ER) disk; that way you'll have it if you need it. What is the Emergency Repair disk you ask? It's the disk that you originally used to build the operating system and from which you ran clu_create(8). We recommend keeping this disk and the operating system file systems intact after installation.

# 22.2.1.4 Replacing a Member Disk

If you need to replace only a member disk and you have a vdum p of the "a" partition, you can restore that disk or restore the data to a new disk. In the procedure that follows, you can skip any steps that "correct" for the fact that we are restoring to a different disk already known to the cluster (those steps will be marked with a "†"). Please see section 7.4.4 for more on adding disks to a system. Our original configuration had molari's (member1) member boot disk as dsk2 and its