Use SMIT to configure boot-time NFS mounts on AIX systems. Do not modify the **/etc/filesystems** file by hand since it can be overwritten during volume group imports or exports.

When you add entries to **fstab/vfstab**, be sure to create the appropriate mount point directories with **mkdir**. You can make your changes take effect immediately (without rebooting) by running **mount -a -F nfs** on Solaris or HP-UX; use **-t** instead of **-F** on Linux, and for version 4 use **mount -a -t nfs4**. On AIX, you can mount NFS filesystems with **mount -v nfs -a**.

The flags field of **/etc/fstab** specifies options for NFS mounts; these options are the same ones you would specify on the **mount** command line.

# Restricting exports to privileged ports

NFS clients are free to use any TCP or UDP source port they like when connecting to an NFS server. However, some servers may insist that requests come from a privileged port (a port numbered lower than 1,024). Others allow this behavior to be set as an option. In the world of PCs and desktop Linux boxes, the use of privileged ports provides little actual security.

Most NFS clients adopt the traditional (and still recommended) approach of defaulting to a privileged port to avert the potential for conflict. Under Linux, you can accept mounts from unprivileged ports with the insecure export option.

# 18.5  Identity mapping for NFS version 4

Unlike earlier versions of NFS, which identify users with raw UID and GID values, version 4 uses strings of the form **user@NFS-domain** and **group@NFS-domain**. On both NFS servers and clients, an identity mapping daemon translates between the string identifiers and the local UNIX UID and GID values. Mapped values are used to translate file attribute information, but they are not used for access control, which is handled separately.

All systems participating in an NFSv4 network should have the same NFS domain. In most cases, it’s reasonable to use your DNS domain as the NFS domain. For example, atrust.com is a straightforward choice of NFS domain for the server hap.atrust.com. Clients in subdomains (e.g., booklab.atrust.com) may or may not want to use the shorter site-wide name (e.g., atrust.com) to facilitate NFS communication.

Unfortunately for administrators, there is no standard implementation of NFSv4 UID mapping, so the details of administration differ slightly among systems. Table 18.10 on the next page names the mapping daemon on each of our example systems and notes the location of its configuration file.

Other than having their NFS domains set, identity mapping services require little assistance from administrators. The daemons are started at boot time from the same scripts that manage NFS. After making configuration changes, you’ll need

![](bbox=[0.194, 0.109, 0.24, 0.145])