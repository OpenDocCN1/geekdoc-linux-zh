# Selecting the Installation Class

The Red Hat Linux installation procedure provides three default installation classes or configurations:

+   - GNOME Workstation
- KDE Workstation
- Server

The workstation classes are a quick way to get a Red Hat Linux system up and running. Both workstation classes install the most commonly used packages. In addition, the GNOME Workstation class installs the GNOME desktop manager, and the KDE Workstation class installs the KDE desktop manager.

The workstation classes are particularly useful for building a dual-boot system, because they disturb no non-Linux partitions as long as sufficient unallocated disk space is available. They do, however, delete all existing Linux (ext2) partitions. They establish three standard partitions:

+   - 64MB swap partition
- 16MB boot partition (/boot)
- A root partition (/) that uses the remaining free disk space

Both workstation classes require about 600MB of free disk space. In contrast to the workstation classes, the Server installation class deletes all existing partitions, including DOS/Windows partitions. The Server installation class requires about 1.6GB of disk space. By default, a Server installation lacks the following components, which are included in one or the other of the work-station installations:

+   - Author/Publishing
- DOS/Windows connectivity
- GNOME or KDE
- Graphics manipulation
- Multimedia support
- X Window system