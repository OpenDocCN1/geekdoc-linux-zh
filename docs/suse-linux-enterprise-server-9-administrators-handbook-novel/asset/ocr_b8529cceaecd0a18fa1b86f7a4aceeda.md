As a system matures and the user community's use of a machine increases, it is not uncommon for a system to run low on resources. The following section examines how you can add devices to a system to solve some of these issues.

# Adding and Removing Hardware

The acquisition stage of a new server should include preliminary growth estimates. Capacity planning is an ongoing process and can usually monitor long-term resource consumption. Eventually, either through aging or through the creation of unexpected projects, servers become resource bound.

When possible, a new server will be purchased, with significantly larger capacity, and the functionality transferred to the new machine. In many cases, however, budget or, more typically, time constraints make this impossible.

The most common resource problem is disk space. As users become accustomed to a system or service, they tend to use it more. They copy their local workstation files to the server for proper backups and disaster recovery purposes. In some cases, an individual or department significantly increases its website with new and improved features. Either way, as system manager, you will be required to increase the system's capacity.

The following section examines how additional disk space can be added to a system and targeted to a specific solution. It is understood that additional disk space will have backup and disaster recovery implications. These topics will be covered in Chapter 10, “Data Backup and Disaster Recovery.”

# Preparations

The most common hardware added to a system is disk space. Other devices you might want to add to your system usually come with vendor-specific instructions for SLES and will not be covered here. Many are peripherals such as scanners, webcams, and audio gear that are not typically incorporated into servers.

For the purpose of this section, we will discuss the concept of a disk as a single physical unit of storage. We will ignore the underlying complexities of how the unit of storage is generated. The “disk” could be simply a single IDE spindle of fixed capacity, or it could be a partition of a larger RAID array managed at the firmware level. In the current discussion, we will treat these as identical in terms of how they are presented to the operating system.