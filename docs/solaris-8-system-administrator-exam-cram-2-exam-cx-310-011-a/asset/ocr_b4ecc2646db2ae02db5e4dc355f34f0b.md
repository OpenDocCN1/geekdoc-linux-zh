view and modify the partition table of the selected disk, but also to create new partition tables.

![](bbox=[0.151, 0.158, 0.255, 0.228])

Basic understanding and general use of the **format** Partition submenu is a test objective. Be familiar with the Partition submenu commands and their intended use.

Table 8.5 describes the subcommands available on the Partition submenu.

| Subcommand | Description |
|---|---|
| **0** through **7** | Modifies the tag, flags, starting cylinder, and size associated with partitions 0 through 7. |
| **select** | Selects a partition table. |
| **modify** | Modifies a partition table. Starts with the current partition table or all disk space in an unassigned partition. (A large unassigned partition is referred to as “free hog.”) |
| **name** | Assigns a name to the current partition table. |
| **print** | Displays the current partition table. |
| **label** | Writes the current partition table and label to disk. |
| **!cmd** | Executes **cmd** using the user’s shell, and then returns to the **format** command. |
| **quit** | Returns to the **format** menu. |

The following example uses the Partition submenu to name the partition table, select a partition table, and display the current selected table:

```
format> partition

PARTITION MENU:
      0       - change '0' partition
      1       - change '1' partition
      2       - change '2' partition
      3       - change '3' partition
      4       - change '4' partition
      5       - change '5' partition
      6       - change '6' partition
      7       - change '7' partition
select - select a predefined table
modify - modify a predefined partition table
name   - name the current table
print  - display the current table
label  - write partition map and label to the disk
!<cmd> - execute <cmd>, then return
quit   - quit
```