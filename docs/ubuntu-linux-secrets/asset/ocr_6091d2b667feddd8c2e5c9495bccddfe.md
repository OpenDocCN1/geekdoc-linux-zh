# Table 3-2: (continued)

| Location | Description |
|---|---|
| /home | User directories for storing personal files and individual application setting files |
| /tmp | Temporary files used by applications and the Linux system |
| /usr | A common location for multi-user application files |
| /var | The variable directory, commonly used for log files and spool files |
| /opt | Optional package installation directory for third-party applications |
| /usr/local | A common alternative location for optional multi-user package installations |

If you create just one partition for Ubuntu, you must mount it at the root mount point (/). If you have additional partitions available, you can mount them in other locations within the virtual filesystem.

If you’re using the manual partition method, don’t forget to allocate a partition for the swap area, even if you already have lots of physical memory installed on your system. The standard rule of thumb is to create as large of a swap area as you have physical memory. Thus, if you have 2 GB of physical memory, create a 2 GB partition and assign it as the swap area.

> Secret
> One problem with Linux is that if the root mount point hard drive becomes full, the system will be unable to boot. To prevent this from happening, many Linux administrators create a separate partition for the /home mount point, where user files are normally stored.

This keeps user files separate from the operating system files. With this technique, a user who tries to store many large files won’t take up all of the disk space and crash the system. Even if the installation is just for a single-user personal workstation, this technique can prevent you from accidentally using up all the disk space and crashing your system.

Once you’ve created the partition settings (either manually or via the Ubuntu guided method) you’re ready to move on to the next step in the installation process.

# Create a Login ID

Up next in the installation process is selecting a Login ID, shown in Figure 3-10.