Be sure to review your partition table after each change to ensure that the changes you made are what you intended.

It is customary to create your primary and swap partitions before creating an extended partition. However, you can create a primary partition after creating an extended partition as long as there is free space available and you have not reached the four-partition limit.

# Step 3: Create an Extended Partition

Next, you should create an extended partition. Use the following:

```
Command (m for help): n
Command action
  e extended
  p primary partition (1-4)
e
First cylinder (476-788): 476
Last cylinder or +size or +sizeM or +sizeK (476-788): 788
```

When your partition table is displayed again, you'll see the following:

```
Command (m for help): p
Disk /dev/hda: 255 heads, 63 sectors, 788 cylinders
Units = cylinders of 16065 * 512 bytes
```

| Device | Boot | Begin | Start | End | Blocks | Id | System |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/hda1 | * | 1 | 1 | 459 | 3686759 | 83 | Linux native |
| /dev/hda2 | | 460 | 460 | 475 | 128488 | 82 | Linux swap |
| /dev/hda3 | | 476 | 476 | 788 | 2513751 | 5 | Extended |

Next, you will need to create logical drives in your extended partition. When you issue the n command, you will have a new choice:

```
Command (m for help): n
Command action
  l logical (4 or over)
  p primary partition (1-4)
```

```
Command (m for help):
```

You can elect to divide your extended partition into one or more logical drives by using the 1 command and then specifying the appropriate size. The starting and ending cylinders for each logical drive must be completely contained within the starting and ending cylinders of the extended partition.