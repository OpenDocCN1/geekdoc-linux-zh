**Table 8.2 Fields of the Partition Table**

| Field | Description |
|---|---|
| Partition Name | A single hexadecimal character used as a name for the partition (0 through f). |
| Tag | The intended use of the partition (obsolete; see Table 8.3). |
| Flags | 1 if the partition is not mountable; 10 if the partition is read-only (obsolete). |
| First Sector | The number of the first sector in the partition. |
| Sector Count | The number of sectors in the partition. |
| Last Sector | The number of the last sector assigned to the partition. |
| Mount Directory | The directory where the partition (actually file system) was last mounted. |

When you define partitions, you can assign them a hexadecimal tag that identifies the partition’s intended use. These partition tags can be used during system maintenance to quickly identify and select partitions. The tags, listed in Table 8.3, are stored in the tag field of the partition table.

**Table 8.3 Partition Tags**

| Partition Type | Tag Value |
|---|---:|
| unassigned | 0 |
| boot | 1 |
| root | 2 |
| swap | 3 |
| usr | 4 |
| backup | 5 |
| stand | 6 |
| var | 7 |
| home | 8 |
| altsctr | 9 |
| cache | a |

You can create the partition table by using the **format** command or the **fmthard**(1M) command. To display it, use the **format** command or the **prtvtoc**(1M) command.

After the partition table has been populated with the appropriate information (the disk partitions have been defined), you can create file systems