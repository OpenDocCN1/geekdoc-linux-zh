| Partition Type | Description |
| :--- | :--- |
| *Primary* | A maximum of four primary partitions are allowed. The swap filesystem and the boot partition are normally created in a primary partition. |
| *Extended* | There can be only one extended partition, which can be further subdivided. This partition type does not contain any data and has a separate partition table. |
| *Logical* | A logical partition is created within an extended partition. There is no restriction on the number of logical partitions, but it is advisable to limit it to 12 logical partitions per disk drive. |

# # The fdisk Utility

**Definition:**
An *fdisk* is a menu-driven utility program that is used for creating, modifying, or deleting partitions on a disk drive. Using `fdisk`, a new partition table can be created, or existing entries in the partition table can be modified. The `fdisk` utility understands the DOS and Linux type partition tables. Depending on the partition table created, the DOS FDISK or the Linux `fdisk` program is invoked. The `fdisk` utility also allows you to specify the size of partitions.

![](bbox=[0.77, 0.35, 0.87, 0.42])

**Example:**

![](bbox=[0.09, 0.51, 0.65, 0.79])

# Syntax

The syntax of the `fdisk` utility is `fdisk [option] [device_name]`.