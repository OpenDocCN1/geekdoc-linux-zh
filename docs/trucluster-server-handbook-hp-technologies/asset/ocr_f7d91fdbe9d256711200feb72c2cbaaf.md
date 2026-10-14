```
There may be more optional products than can be presented on a single screen. If this is the case, you can choose products screen by screen or all at once on the last screen. All of the choices you make will be collected for your confirmation before any products are installed.
1) Patches for Tru64 UNIX V5.1A
2) Patches for TruCluster Server V5.1A

Or you may choose one of the following options:
3) ALL of the above
4) CANCEL selections and redisplay menus
5) EXIT without installing any products

Enter your choices or press RETURN to redisplay menus.
Choices (for example, 1 2 4-6): 3
```

```
You are installing patches (to be selected) from the following products:
    Patches for Tru64 UNIX V5.1A
    Patches for TruCluster Server V5.1A
Is this correct? (y/n): y
..
```

For more information on installing patches on Tru64 UNIX, please review the Tru64 UNIX and TruCluster Software Products Patch Kit Installation Instructions guide for the patch kit that you will be installing.

# 10.4 Create the Cluster

Now comes the “fun” part – creating a single-node cluster. To create a cluster, we use the clu_create(8) command. The clu_create command performs the following:

+   - It prompts the System Administrator for configuration information necessary for the creation of a single-node cluster.
+   - It labels disks, creates root (/), /usr, and /var file systems, and the first member’s boot disk, copies data to the newly created file systems, creates CDSLs, and updates system configuration information.
+   - A quorum disk is optionally configured.
+   - The next step is the kernel build of the first cluster member. At this point, the System Administrator will be given the opportunity to modify the kernel configuration file.
+   - The final step is the configuration of boot-related SRM console variables: bootdef_dev, boot_reset, and boot_dev. This allows for the boot of the cluster from the cluster member’s boot_partition.

Now without further ado, let’s build a cluster!