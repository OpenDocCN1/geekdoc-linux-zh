+   ■ **512MB of physical RAM**  This is necessary for the proper operation of the Oracle Database Server; however, this is a minimum requirement. For optimal operation, you really should have significantly more RAM than this.

+   ■ **1GB of swap space**  The amount of swap space is typically set to two times the amount of physical RAM. For systems where RAM is greater than 2GB, the amount of swap space can be more in the range of one to two times the amount of RAM. The more RAM you have, the less likely it is you will use the swap space.

+   ■ **/tmp must have at least 400MB of space**  If the /tmp partition is created as a separate partition, it must be at least 400MB in size. If the /tmp directory is part of the / (root) filesystem, there must be at least 400MB in addition to the space you will use for other usage.

+   ■ **Oracle file space**  You must allocate at least 1.5GB of space for the most basic Oracle install. This amount varies depending on the components you have chosen to install.

+   ■ **Oracle data files**  In order to install the basic sample database, you must have at least 1.2GB of space. This space can be either on a filesystem, an NFS partition, or on an Oracle ASM (Automatic Storage Management) disk group. In an Oracle 10g RAC environment, this storage must be shared between all of the nodes in the cluster.

These requirements should be considered when creating your Linux installation. It is quite painful to have to rebuild partitions in order to fit the Oracle installation, and the time required could make your installation take much longer.

# Configuring the Filesystems

The Linux filesystem layout can consist of as little as three partitions, or as many as you want. The minimal requirements for a Linux configuration consist of the following two partitions:

+   ■ **/, the root partition**  This is the initial partition. All other partitions are mounted on subdirectories of the root partition.

+   ■ **swap, the swap partition**  The swap partition is not mounted as a regular filesystem, but is required by the Linux partition in order to function. The swap partition (or partitions) must be configured according to the minimum requirements listed earlier.