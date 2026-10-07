# Linux Web Server Toolkit

Changed system type of partition 2 to 82 (Linux swap)
Command (m for help):

Now use the p command again to see what the partition you created looks like. You've been changing the partitions only in the system memory. You'll decide to write these changes to the hard disk (making them real) or discard your efforts in a minute.

Command (m for help): p

Disk /dev/hda: 64 heads, 63 sectors, 786 cylinders
Units = cylinders of 4032 * 512 bytes

| Device | Boot | Begin | Start | End | Blocks Id | System |
|---|---|---|---|---|---|---||
| /dev/hda1 >=32M | | 1 | 1 | 152 | 306400+6 | |
| /dev/hda2 | | 153 | 153 | 169 | 34272 82 | Linux swap |

Command (m for help):

Now use the main Linux partition using the n command again. Make this partition number 3, also a primary partition.

Command (m for help): n
Command action
 e extended
 p primary partition (1-4)
P
Partition number (1-4): 3
First cylinder (170-786): 170

For the starting cylinder, again enter the first number given. For the ending point, give the last cylinder listed, making the main Linux partition fill all the remaining space on the hard disk.

Last cylinder or +size +sizeM or +sizeK ([170]-786): 786

Command (m for help):

Use the t command with partition 3 to change the partition type to 83, for a Linux filesystem.

Command (m for help): t
Partition number (1-4): 3
Hex code (type L to list codes): 836

Command (m for help):