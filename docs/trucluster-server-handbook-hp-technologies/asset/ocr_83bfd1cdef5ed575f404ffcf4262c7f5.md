daemons (Table 14-5), as well as commands to aid in moving data to and from LSM (Table 14-6).

# 14.6 Importing a Disk Group

Importing a disk group where a cluster is involved differs from dealing with standalone systems.

There are a few scenarios to consider when importing disk groups in a cluster:

+   - Importing a disk group from a standalone system to a cluster.
+   - Importing a disk group from a cluster to a standalone system.
+   - Importing a disk group from a cluster to a cluster.

| Command | Location | Man | Type | Description |
|---|---|---|---|---|
| lsmbstartup | /sbin | 8 | sh | Script that starts LSM during system startup. |
| lsmsetup | /usr/sbin | 8 | symlink | A symbolic link to the volsetup command. |
| vold | /sbin | 8 | binary | LSM volume configuration daemon. |
| voldctl | /sbin | 8 | binary | Controls the LSM volume configuration daemon (vold). |
| volinstall | /usr/sbin | 8 | sh | Sets up LSM after LSM installation. Creates LSM device special files, etc. |
| voliod | /sbin | 8 | binary | Starts, stops, and reports on LSM kernel I/O daemons. |
| volrecover | /sbin | 8 | binary | Performs volume recovery operations |
| volrestore | /usr/sbin | 8 | sh | Restores a complete or partial LSM configuration from information saved by the volsave command. |
| volrootmir | /usr/sbin | 8 | sh | Creates mirror of areas necessary for booting on a new disk. NOT SUPPORTED IN A CLUSTER! |
| volsave | /usr/sbin | 8 | sh | Saves a LSM configuration. |
| volsetup | /usr/sbin | 8 | sh | Initializes LSM by creating the rootdg disk group. |
| voltrace | /usr/sbin | 8 | binary | Trace operations on volumes. |
| volunroot | /usr/sbin | 8 | sh | Removes root and swap from LSM on a standalone system. NOT SUPPORTED IN A CLUSTER! |
| volwatch | /usr/sbin | 8 | sh | Monitors LSM for failure events and performs hot sparing. |

Table 14-5: LSM Administrative Commands and Daemons