# RAID Tools

The RAID support available with Red Hat Linux 6.0 is not the support found in the stock kernel. Red Hat has upgraded the RAID software drivers and the RAID tools to a more recent set than is currently found in the original kernel source.

> **Note**
> 
> To see the complete set of patches applied to the original Linux source tree, examine the source RPM for the kernel. To install this SRPM, look for `kernel-2.2.5-15.src.rpm` either on the Red Hat FTP site or on the SRPM CD-ROM that comes with the Red Hat distribution. Once you have installed this RPM, you can examine all of the kernel patches applied by looking in the `/usr/src/redhat/SOURCES` directory.

Red Hat Linux comes with version 0.90 of the RAID tools. These commands differ from their predecessors significantly and include features required to support the extra functionality provided by the updated RAID drivers supplied with the kernel sources. The RAID command set resides in the `/sbin` directory and consists of tools in Table 9.1.

TABLE 9.1 The RAID Commands and Their Functions

| Command | Function |
|---|---|
| mkraid | Initializes RAID device arrays |
| raidstart | Configures RAID devices in the kernel and activates them |
| raidhotadd | Adds spare devices to a running RAID array |
| raidhotremove | Removes devices from a running RAID array |
| raidstop | Unconfigures a RAID device array |

The first command to consider is the `mkraid` command. The `mkraid` command is used to initialize RAID devices and is applicable to all RAID levels supported by the Linux software RAID drivers. The `mkraid` command is similar in function to the `mkfs` command used to create a filesystem in that it is the first step in preparing the RAID array to receive data. In normal usage, the only time that this command is used is during the creation of a RAID array because like the `mkfs` command, this command is destructive to the data on the RAID array. It reads from a configuration file, either one that you specify with the `-c` command-line option or the default `/etc/raidtab`, to determine the specifics of each RAID device. The options for the `mkraid` command are described in the manual page and in Table 9.2.