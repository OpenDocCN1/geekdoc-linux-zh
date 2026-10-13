Although fdisk can be used for numerous purposes, the following are the most common actions:

+   - Creating a primary partition
+   - Creating a logical partition
+   - Setting a partition type
+   - Displaying existing partitions
+   - Deleting an existing partition
+   - Writing changes to disk

# CREATING A PRIMARY PARTITION

To create a primary partition with fdisk, follow these steps:

+   1. Use the n menu option to create a new partition.
+   2. When prompted, enter p to indicate you want to create a primary partition.
+   3. When prompted, enter a number from 1-4 to indicate which primary partition you want to create.
+   4. When prompted, enter the cylinder where the partition should start.
+   5. When prompted, enter the cylinder where the partition should end or enter the size (for instance, +32M for a 32MB partition).

A typical fdisk dialog for creating a primary partition is as follows:

```
Command (m for help): m
Command action
   e   extended
   p   primary partition (1-4)
p
Partition number (1-4): 1
First cylinder (1-810, default 1): 1
Last cylinder or +size or +sizeM or +sizeK (1-810, default 810): +32M

Command (m for help):
```

# CREATING A LOGICAL PARTITION

In order to create a logical partition with fdisk, you first need to create an extended partition to contain one or more logical partitions. To do this, use the following steps:

+   1. Use the n menu option to create a new partition.
+   2. When prompted, enter e to indicate you want to create an extended partition.
+   3. When prompted, enter a number from 1-4 to indicate which extended partition you wish to create.
+   4. When prompted, enter the cylinder where the partition should start.
+   5. When prompted, enter the cylinder where the partition should end or enter the size (for instance, +3200M for a 3200MB partition).