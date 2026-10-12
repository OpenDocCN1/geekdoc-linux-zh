| Partition | Description |
| :--- | :--- |
| / | The root partition is for those core system files necessary to bring a system to single-user mode. Once established, the partition’s contents shouldn’t vary at all and definitely shouldn’t need to grow. The intent is to isolate this file system from other file systems, to prevent interference with core operations. |
| /usr | This partition is used for system software such as user tools, compilers, X, and so forth. Because you may one day need to find a bigger home for your system software, you put this in a separate partition. |
| /var | The /var partition is used to hold files that change a lot—this usually includes spool directories (mail, print, etc.) and log files. What makes this partition worrisome is that external events can make its contents grow beyond allocated space. Log files from a web server, for instance, can grow quickly and beyond your control. To keep these files from spilling over into the rest of your system, it’s wise to keep this partition separate. (A type of attack via the network can be mounted by artificially generating so much activity on your server that the disk fills up with system logs and the system behaves unreliably.) |
| /tmp | Similar to /var, files in /tmp can unexpectedly consume substantial space. This can occur when users leave files unattended or application programs create large temporary files. Either way, maintaining this partition is a good safety mechanism. |
| /home | If you need to store home directories on your disk, especially for users whose disk consumption needs to be restricted, you’ll definitely want to have this separate partition. |
| swap | The swap partition is necessary to hold virtual memory. Although it isn’t required, swap is often a good idea in case you do exhaust all your physical RAM. In general, you’ll want this partition to be the same size as your RAM. |

# Table 7-5 Partition Descriptions and Configuration

The last partition would be an “extended” partition, unseen by the user but able to contain additional partitions.

The next question: Which partition number? (You can see the limit of four primary partitions as part of the question.) You start with one, picking the default starting cylinder, and then specify that you want 25MB allocated to it.

To create the second partition for swap, type the following:

```
Command (m for help): n
Command action
     e   extended
     p   primary partition (1-4)
**p**
Partition number (1-4): **2**
First cylinder (68-665, default 68): **68**
Last cylinder or +size or +sizeM or +sizeK (52-665, default 665): **+16M**
Command (m for help):
```