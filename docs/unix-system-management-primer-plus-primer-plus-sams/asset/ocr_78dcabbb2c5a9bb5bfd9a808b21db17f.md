# UNIX SYSTEM MANAGEMENT PRIMER PLUS

# FIGURE 10.11
The DiskUtil GUI

metatool can graphically show the configuration of your metadevices.

![](bbox=[0.318, 0.038, 0.934, 0.435])

# Data Redundancy Using Split Mirrors

In data warehousing environments and on systems with long backup windows, it would be very convenient to work with physically separate copies of data instead of the real thing. That way, I/O-intensive processes such as backups and complex database queries don't interfere with the normal operations of the system and cause slowdowns or temporary outages.

Split mirrors help make this reality and, thus, contribute to high availability in Unix systems. A split mirror is a RAID-1 mirror in which one of the submirrors can be split off from the main device to become a completely separate device. As a submirror, this new device carries an exact copy of the original mirror's data at the time of the split. Backups, data-housing queries, and any other I/O-intensive tasks can now be performed on this separate device without interfering with production tasks on the main mirror.

# Use Three-Way Mirrors for Split Mirror Configurations

By using a three-way mirror in split mirror configurations, the mirror will still have the minimum two disks required for redundancy after one disk is split off.

The benefits of a split mirror become even more apparent on a SAN (storage area network), where any server on the SAN can potentially have access to any disk device on the SAN. The split device can be accessed separately by an entirely different server to which the original mirror is mounted, providing instant data duplication.