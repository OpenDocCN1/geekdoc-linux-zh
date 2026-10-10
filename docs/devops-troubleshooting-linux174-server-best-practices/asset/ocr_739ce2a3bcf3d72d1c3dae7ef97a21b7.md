| Device: |    |    |    |    |     |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |
| sda | 9.82 | 417.96 | 27.53 | 30227262 | 1990625 |
| sda1 | 6.55 | 219.10 | 7.12 | 15845129 | 515216 |
| sda2 | 0.04 | 0.74 | 3.31 | 53506 | 239328 |
| sda3 | 3.24 | 198.12 | 17.09 | 14328323 | 1236001 |

*Columns: tps, Blk_read/s, Blk_wrt/s, Blk_read, Blk_wrt*

The first bit of outputs gives CPU information similar to what you would see in top. Below it are I/O stats on all of the disk devices on the system as well as their individual partitions. Here is what each of the columns represents:

+   - `tps`  
+     This lists the transfers per second to the device. “Transfers” is another way to say I/O requests sent to the device.
+   - `Blk_read/s`  
+     This is the number of blocks read from the device per second.
+   - `Blk_wrt/s`  
+     This is the number of blocks written to the device per second.
+   - `Blk_read`  
+     In this column is the total number of blocks read from the device.
+   - `Blk_wrt`  
+     In this column is the total number of blocks written to the device.

When you have a system under heavy I/O load, the first step is to look at each of the partitions and identify which partition is getting the heaviest I/O load. Say, for instance, that you have a database server and the database itself is stored on /dev/sda3. If you see that the bulk of the I/O is coming from there, you have a good clue that the database is likely consuming the I/O.

Once you figure that out, the next step is to identify whether the I/O is mostly from reads or writes. Let’s say you suspect that a backup job is causing the increase in I/O. Since the backup job is mostly concerned with reading files from the file system and writing them over the network to the backup server, you could possibly rule that out if you see that the bulk of the I/O is due to writes, not reads.