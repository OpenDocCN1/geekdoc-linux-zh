```
define dumptype always-full {
    global
    comment "Full dump of this filesystem always"
    compress none
    priority high
    dumpcycle 0
}
```

This example amanda.conf file was trimmed down from a larger example I copied from the /etc/amanda/DailySet1 directory. The example amanda.conf file provides additional information on the available configuration options. Also, the online man page for Amanda should be helpful (type man amanda to read it). You can find more instructions in the /usr/share/doc/amanda-server* directory. Generally, you have to do the following:

+   * Modify the org name for reports.
+   * Change the device names set for tapedev and rawtapedev to match your tape device.
+   * Select a tape type entry that is appropriate for your tape drive.
+   * Change the name of the directory specified in the holding disk section to match the directory you created earlier.

# ### Creating a disklist File

You also must create a disklist file in the /etc/amanda/normal directory. This simply contains a list of the systems and disk partitions to back up. The qualifier always-full is included on each entry to tell Amanda what type of backup to perform. It means to use full, rather than incremental, backups.

```
# sample Amanda2 disklist file
#
# File format is:
#
#       hostname diskdev dumptype [spindle [interface]]
#
# where the dump types are defined by you in amanda.conf.

dexter sda5 always-full
dexter sda6 always-full
dexter sda7 always-full
dexter sda8 always-full

daffy sda5 always-full
daffy sda6 always-full
daffy sda7 always-full
daffy sdb1 always-full
daffy sdb2 always-full
```