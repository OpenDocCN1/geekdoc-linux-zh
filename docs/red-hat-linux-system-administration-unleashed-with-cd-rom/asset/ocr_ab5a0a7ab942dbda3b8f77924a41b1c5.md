Device and application lock files are stored in /var/lock and this is where you look if you need to remove a locked file that is inhibiting a program.

The next directory on our list of important directories is the user mail spool directory, /var/mail. This directory is one of the places to look to diagnose problems with a user's mail.

The final directory that we are concerned with under /var is the /var/yp directory, which is used to store database files for the network information system or NIS daemons.

# The Red Hat Filesystem Layout

Red Hat Linux systems are partially compliant with the Filesystem Hierarchy Standard. The differences between the standard and the Red Hat filesystem layout are minimal. The most visible of the changes is the location of the user mail spool files, which on Red Hat Linux 6.0 systems are located in the /var/spool/mail directory. Another major area of divergence is the location of the manual pages and other systems documentation, which are in /usr/doc and /usr/man, instead of /usr/share/man as specified in the standard. The remainder of this section describes some of the directories of interest to an administrator of Red Hat Linux systems.

# The /etc/sysconfig Directory

The bulk of the system configuration variables used by the initialization scripts in /etc/rc.d are defined in files contained in the /etc/sysconfig directory. Files found in this directory include files named init, mouse, keyboard, soundcard, and network. These define variables related to the configuration of these systems or devices. A major subdirectory on this one is the network-scripts directory, which contains the scripts required to bring up the various configured network interfaces. It contains scripts and more configuration files that actually bring the various interfaces up and down, using many of the configuration variables defined in the /etc/sysconfig directory.

# The /etc/rc.d Directory

Red Hat Linux uses a slightly modified System V style of system initialization scripts. For users of Solaris or HP/UX systems, this structure will seem quite natural. The major difference is that instead of the initialization script directory being located in /etc, it is located one level lower in /etc/rc.d along with the runlevel specific directories.