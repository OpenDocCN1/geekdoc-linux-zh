| Mount Type | Description |
| :--- | :--- |
| /etc/fstab | A line of code is added to the /etc/fstab file that is referenced by the netfs service. NFS shares are mounted when the initialization script runs from the /etc/init.d/netfs file. The syntax of the line that is added is: {server *IP address or host* name} {<u>exported filesystem</u>} {<u>mount point</u>} nfs ({<u>mount options</u>} 0, 0 |
| autofs | It is an automount utility that is used to mount and unmount filesystems automatically without the need for system resources. It compresses kernel modules that implement the filesystems and a user space daemon to control other functions. It uses the /etc/auto.master file as the main configuration file. |

![](bbox=[0.05, 0.44, 0.15, 0.51])

# The rsync Utility

**Definition:**

The *rsync* utility is a utility that is used to synchronize files among systems. It compares two files and sends only the differences in the compressed form, instead of sending the entire file. The *rsync* daemon is managed using the rsyncd.conf file stored in the /etc directory. The *rsync* utility uses the rsync algorithm to determine differences between files.

**Example:**

![](bbox=[0.23, 0.63, 0.9, 0.69])

The syntax of the *rsync* utility is rsync {source file or folder} {destination file or folder}.

# Syntax