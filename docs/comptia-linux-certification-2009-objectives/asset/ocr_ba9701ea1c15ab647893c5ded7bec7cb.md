# TOPIC E

# Manage Logical Volumes Using the Logical Volume Manager

You added new storage devices to store huge amounts of data on the Linux system. Now, you want to manage the storage area when the system runs out of space. In this topic, you will manage disk space with the help of the logical volume manager.

Consider a scenario where you are downloading source files from a website, to install new software. While downloading, an error is displayed stating that there is insufficient memory in your home directory. You want to increase the storage space, without disrupting the download. To manage the current situation, you decide to move the memory allocated to the swap filesystem to the home directory. Learning about LVM will enable you to accomplish this task.

# LVM

**Definition:**
*Logical Volume Manager (LVM)* is a software tool that is used to manage disk storage on a computer system. LVM creates an abstraction layer over the storage area on the system so that details about where data is stored are hidden. It hides the storage details by completely separating the hardware storage from the software management, so that any changes made to the hardware do not affect the software during runtime. The volume manager organizes hard disks into volume groups and the partitions in the storage area are referred to as the *Logical Volumes (LV).*

**Example:**

![](bbox=[0.25, 0.57, 0.78, 0.7])

*Figure 15-7: Logical volumes on a hard disk.*