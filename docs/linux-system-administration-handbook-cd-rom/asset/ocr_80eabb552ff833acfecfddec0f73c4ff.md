# D.3 Problems Using Very Large Hard Disks

After these values are entered in the “fdisk” expert mode, return to the normal main menu of “fdisk” with “r.” Now using the “p” command should show all partitions with the warnings shown in the first listing above.

Command (m for help): p Disk /dev/sda: 255 heads, 63 sectors, 522 cylinders Units = cylinders of 16065 * 512 bytes

| Device | Begin | Start | End | Blocks | Id | System |
|---|---|---|---|---|---||}{
| /dev/sda | | 1 | 96 | 771088* | 6 | DOS 16-bit>32M |
| /dev/sda2 * | 97 | 97 | 249 | 128292* | 82 | Linux swap |
| /dev/sda3 | 250 | 250 | 313 | 514080 | a5 | BSD/386 |
| /dev/sda4 | 314 | 314 | 522 | 1678792* | 5 | Extended |
| /dev/sda5 | 314 | 314 | 345 | 257008* | 83 | Linux native |
| /dev/sda6 | 346 | 346 | 353 | 64228* | 83 | Linux native |
| /dev/sda7 | 354 | 354 | 438 | 682731 | 6 | DOS 16-bit>32M |
| /dev/sda8 | 439 | 439 | 522 | 674698* | 6 | DOS 16-bit>32M |

If the error messages have not disappeared, you have not found the right values. Try with new values until the error messages do not appear.
When you find the correct values, make a note of them in your system documentation. You must enter these values each time you need to run “fdisk.” They are not saved.
After the correct values are entered in expert mode, you can continue working normally with “fdisk” to create the partitions that you need to install on Linux.
If you want to use LILO to boot Linux from the hard disk, you must list the correct partitions in the file /etc/fstab/ These partitions are shown from the main menu of “fdisk” once you have corrected the information in expert mode. Change the partition display of “fdisk” to sectors with the “u” command. The sector values shown correspond to the block values of the LBA mode.

Command (m for help): u Changing display/entry units to sectors

Display the revised partition table:

Command (m for help): p

/dev/sda: 255 heads, 63 sectors, 522 cylinders
Units = sectors of 1 * 512 bytes

| Device | Begin | Start | End | Blocks | Id | System |
|---|---|---|---|---|---||}{
| /dev/sda | | 63 | 63 | 1542239 | 771088* | 6 | DOS 16-bit>32M |
| /dev/sda2 * | 1542240 | 1542240 | 1282972* | 82 | Linux swap |
| /dev/sda3 | 4000185 | 4000185 | 5028344 | 514080 | a5 | BSD/386 |
| /dev/sda4 | 5028345 | 5028345 | 8385929 | 1678792* | 5 | Extended |