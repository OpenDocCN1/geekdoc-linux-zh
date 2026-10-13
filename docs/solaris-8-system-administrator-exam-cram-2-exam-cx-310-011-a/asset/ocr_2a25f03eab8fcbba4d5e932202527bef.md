# hot relocation

The process Volume Manager uses to reconstruct a failed subdisk on a spare disk or free space within a disk group and then substitute the rebuilt subdisk for the failed subdisk.

# hot spare

A disk slice that DiskSuite automatically substitutes for a slice that has failed.

# hot spare pool

A collection of hot spares managed by DiskSuite.

# indirect map

A type of AutoFS configuration file that identifies partial pathnames to mount points and associated NFS resources. The partial pathnames are relative to the directory identified in the /etc/auto-master file.

# initialization file templates

Login and shell startup initialization files for each user account are copied from templates under the /etc/skel directory when the home directory for the user account is created.

# initialization files

Several initialization files are associated with each user account home directory. These files are used to specify commands to be executed when the associated event occurs. Depending on the login shell being used, there might be a login initialization file, a shell startup file, or a logout file. Commands in the login initialization file are executed when

the user logs in. All three common shells provide a login initialization file. Commands in the shell startup file are executed whenever the logged-in user starts a shell. Both csh and ksh provide this capability. The ENV parameter is used to define the ksh shell startup initialization file. Only csh provides a file for automatic execution of commands when a user logs out.

# install client

A system that will be installed over the network. Basic information about install clients needs to be available through a name service (NIS/NIS+) or in the files under the /etc directory on the install server or boot server.

# install server

A network server that provides the distribution files necessary for installing the Solaris operating system on an install client during an over-the-network installation. The files can be provided directly from the Solaris distribution CD mounted in a local CD-ROM drive or from the local hard disk.

# installation

The four installation methods are SunInstall, Web Start, JumpStart, and Custom JumpStart. All four methods can use a local CD-ROM or over-the-network installation resources to obtain the distribution files. The installation process is divided into three phases: system configuration, system installation, and post-installation.