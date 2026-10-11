# ## Building The Initial KickStart File

To build the initial KickStart file, do the following:

+   1. Log in to the newly installed machine as root.
+   2. Place the Red Hat CD-ROM in the drive, if it is not already there.

> > **TIP:** Use the df command to see whether the CD-ROM is already mounted.

+   3. Type "mount /mnt/cdrom" to add the CD-ROM to your file system.
+   4. Type "cd /mnt/cdrom/RedHat/RPMS" to change to the directory with the RPM packages.
+   5. Type "rpm -ihv mkkick" and press the Tab key to finish the rest of the file name, and then press Enter to install the KickStart file builder.
+   6. Type "mkkickstart_flags > /path/ks.cfg" to create the KickStart install script. The available flags are shown in Table 10.2.

**Related solutions:**  | **Found on page:**
Setting Up A DHCP Server | 213
Setting Up NFS Exports | 505

Table 10.2 Flags used when running mkkickstart.

| Flag | Purpose | Values |
| :--- | :--- | :--- |
| **--dhcp** | Uses DHCP to configure networking for this machine at boot time. | None |
| **--nfs** | Installs over an NFS mount. | *host:path* |
| **--nonet** | Does not clone the networking configuration. Using this flag is a good idea for machines you are preparing for different networking environments, or that have different networking hardware. | None |
| **--nox** | Does not clone the X configuration. Using this flag is a good idea for machines that will not have a GUI or those that have different video hardware. | None |
| **--version** | Displays the version of **mkkickstart** you have. | None |