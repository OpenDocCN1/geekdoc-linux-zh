and could in certain setups cause problems with:
1) software that runs at boot time (e.g., old versions of LILO)
2) booting and partitioning software from other OSs
(e.g., DOS FDISK, OS/2 FDISK)

Command (m for help):_

Note from the preceding output that the fdisk command displays a prompt for the user to accept fdisk commands; a list of possible fdisk commands can be seen if the user presses the m key at this prompt, as shown in the following example:

Command (m for help): m
Command action
 a toggle a bootable flag
 b edit bsd disklabel
 c toggle the dos compatibility flag
 d delete a partition
 l list known partition types
 m print this menu
 n add a new partition
 o create a new empty DOS partition table
 p print the partition table
 q quit without saving changes
 s create a new empty Sun disklabel
 t change a partition's system id
 u change display/entry units
 v verify the partition table
 w write table to disk and exit
 x extra functionality (experts only)

Command (m for help):_

To print a list of the partitions currently set on /dev/hdc, you could press the p key at the fdisk prompt:

Command (m for help): p

Disk /dev/hdc: 20.4 GB, 20490559488 bytes
255 heads, 63 sectors/track, 2491 cylinders
Units = cylinders of 16065 * 512 = 8252800 bytes

| Device | Boot | Start | End | Blocks | Id | System |
|---|---|---|---|---|---|---|
| /dev/hdc1 | * | 1 | 510 | 4096543+ | 83 | Linux |
| /dev/hdc2 | | 511 | 561 | 409657+ | 82 | Linux swap |
| /dev/hdc3 | | 562 | 1247 | 5510295 | 83 | Linux |

Command (m for help):_