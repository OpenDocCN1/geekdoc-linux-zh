# Using the Format Utility to Modify Partitions

If you need to change the size of slices on a particular disk, you can either re-create the disk slices as outlined in the previous section or use the modify option of the format utility.

The modify option allows the root to create slices by specifying the size of each slice without having to keep track of starting cylinder boundaries. It will also keep track of any excess disk space in the temporary free hog slice.

> NOTE
If you try to modify mounted partitions, you receive an error that states Cannot modify disk partitions while it has mounted partitions.

# STEP BY STEP

# 6.3 Modifying a Disk Slice

To modify a disk slice, follow these steps:

+   1. Make a backup of your data. This process will destroy the data on this disk.
2. As root, enter the partition menu of the format utility as described in the 6.2 Step by Step.
3. After printing the existing partition scheme, type modify and press Enter.

When typing modify, you’ll see the following output on a disk that does not have mounted partitions:

```
Select partitioning base:
    0. Current partition table (original)
    1. All Free Hog
Choose base (enter number) [0]?
```

4. Press Enter to select the default selection. The following is displayed:

| Part | Tag | Flag | Cylinders | Size | Blocks |
|------|-----|------|-----------|------|--------|
| 0 | usr | wm | 0 - 194 | 100.26MB | (195/0/0) 205335 |
| 1 | unassigned | wu | 195 - 1167 | 500.28MB | (973/0/0) 1024569 |
| 2 | backup | wm | 0 - 3983 | 2.00GB | (3984/0/0) 4195152 |
| 3 | unassigned | wm | 0 | 0 | (0/0/0) 0 |
| 4 | unassigned | wm | 0 | 0 | (0/0/0) 0 |