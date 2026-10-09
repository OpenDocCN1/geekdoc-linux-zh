The caveat to installing using the **APPLY** option is that additional disk space is required to hold the old version. If you don't have the disk space to spare, you must install the product with **COMMIT**. This option will save on disk space, but it does not provide a simple back-out mechanism. Make a full backup of your root volume group file systems prior to installing with **COMMIT**. In the event of a problem, you can restore the backup.

```
# installp -qa -d /cdrom/usr/sys/inat.images -C -N all

# In the event that you must remove a committed 1pp, you can invoke the deinstall function of the installp command. This -u option will remove product files, associated maintenance, and vital product data (VPD) from the system regardless of the product installation state.

# installp -u  fileset_name   Remove software
```

As with all **installp** command options, it is always a good practice to add the **-p** option to *preview* the results first! As an example:

```
# installp -up fileset_name 1>/tmp/output 2>&1
# view /tmp/output
```

# ## Filesystem Expansion On-the-Fly

To ensure that sufficient filesystem space is available, you can elect to have filesystem size automatically increased during the installation. Unfortunately, this process will sometimes overallocate filesystem space, the result being wasted disk space at the end of the installation. Automatic filesystem expansion can also cause the installation to abort if the requested increment in logical partitions is not available in the volume group. In most cases, you will be better off calculating the space required for the update and allocating the space manually before starting the install process. Remember you cannot easily shrink a filesystem once it is overallocated, but this is usually not a big problem with the large disks being produced today.

```
# installp -qa -d /cdrom/usr/sys/inat.images -X all
# installp -qa -d /cdrom/usr/sys/inat.images all   Auto expansion

# No auto expansion
```

# ## System State

When installing a new product release or maintenance, limit the activity on your system. For some products, this involves shutting down the application being updated and stopping any related subsystems and subservers. If it is controlled by the System