
# LAB 27

## Determine and Configure Hardware Settings: Filesystems and Storage

**Lab Objective:**

Learn about gathering information on and configuring storage devices and special filesystems.

**Lab Purpose:**

In this lab, you will learn about how to differentiate between various types of mass storage devices, and about `sysfs`, `udev`, and `dbus`.

**Lab Tool:**

Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

**Lab Walkthrough:**

### Task 1

Open the Terminal and run `ls /sys/block`

This will give you a list of block devices on your system. At a minimum, you should have a device such as `sda` or `xvda`. These are your standard disk devices, like hard disks and USB drives. You may also have an optical drive, such as `sr0`, and possibly one or more loopback devices.

To get more information on these devices, run `lsblk`

This will list all of those devices as well as their sizes, types, and mount points. Your hard drive(s) should be labeled as “disk”, partitions as “part”, loopback devices as “loop”, and optical or other read-only devices as “rom”.
