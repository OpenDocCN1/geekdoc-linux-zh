```
```text
#
# Directories and files
#
# Kernel, system map, etc.
/boot                              Binlib

# watch config files, but exclude, what changes at boot time,
#... /etc/mtab
/etc/vm*                           ConfFiles

# Binaries
/bin                               Binlib
/sbin                              Binlib

# Libraries
/lib                               Binlib

# Complete /usr and /opt
/usr                               Binlib
/opt                               Binlib
```
```

In this example, you can clearly see where a number of command-line parameters have been predefined. Also, the Binlib macro has been created to identify the file attributes we would like AIDE to track. A list of the attributes AIDE is capable of tracking is shown in Table 12.3.

**TABLE 12.3**  
Tracking AIDE Attributes

| ATTRIBUTE | DESCRIPTION |
|---|---|
| P | Permissions |
| I | Inode |
| N | Number of links |
| U | User |
| G | Group |
| S | Size |
| B | Block count |
| M | Modify time (mtime) |
| A | Access timestamp |
| C | Creation time (Ctime) |