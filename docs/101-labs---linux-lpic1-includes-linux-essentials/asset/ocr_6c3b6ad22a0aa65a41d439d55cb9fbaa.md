# **LAB 32**

# # Design Hard Disk Layout

**Lab Objective:**
Learn how to design a disk partitioning scheme.

**Lab Purpose:**
In this lab, you will learn about disk partitioning, partition types, and how to set up partitioning using tools such as *fdisk*.

**WARNING:** In this lab, you will begin partitioning your main disk with *fdisk*. As long as you do not use the write command, these changes will stay in memory only and your data will be safe. As an extra precaution, you may wish to run *fdisk* on a secondary drive, or create another VM just for this purpose.

**Lab Tool:**
Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**
A single Linux machine, or virtual machine

# ## Lab Walkthrough:

**Task 1:**
Open the Terminal and run *sudo fdisk /dev/sda*—substitute your hard disk for */dev/sda*, if *sda* is not the right device.

Enter p to see the current partition layout. If you selected your main disk, you should see at least one partition, along with its size, type, and whether it is a boot partition. For example, in the output below:

```
/dev/sda1 * 2048 41940991 41938944 20G 83 Linux
```

The disk contains a single 20GB partition, of type 83—a Linux filesystem (enter i to list all of the types).