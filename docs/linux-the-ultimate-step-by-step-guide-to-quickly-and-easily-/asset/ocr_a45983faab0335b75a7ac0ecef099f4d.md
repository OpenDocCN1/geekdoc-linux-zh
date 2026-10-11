| Term | Description |
| :--- | :--- |
| **Used** | Total kilobytes of space used (by files). |
| **Avail** | Total kilobytes available for use. |
| **Capacity** | Percentage of total space used by files. |
| **Mounted on** | What the file system is mounted on. |

You can use the `-h` (human readable) option to display the output in a format that shows the size in easier-to-understand notation.

# The du Command

The `du` (disk usage) command enables you to specify directories to show disk space usage on a particular directory. This command is helpful if you want to determine how much space a particular directory is using. The following command will display the number of blocks used by each directory. A single block may take either 512 Bytes or 1 Kilo Byte depending on your system.

```
$du /etc
10	/etc/cron.d
126	/etc/default
6	/etc/dfs
...
$
```

The `-h` option makes the output easier to comprehend –

```
$du -h /etc
5k	/etc/cron.d
63k	/etc/default
3k	/etc/dfs
...
$
```

# Mounting the File System

A file system must be mounted in order to be usable by the system. To see what is currently mounted (available for use) on your system, use this command –

```
$ mount
/dev/vzf5 on / type reiserfs (rw,usrquota,grpquota)
proc on /proc type proc (rw,nodiratime)
devpts on /dev/pts type devpts (rw)
$
```