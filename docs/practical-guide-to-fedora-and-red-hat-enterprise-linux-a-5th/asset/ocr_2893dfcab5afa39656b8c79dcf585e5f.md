![](bbox=[0.4, 0.11, 0.8, 0.36])

# **Figure 3-7**	The Disk Partitioning screen

creates a default layout in the space it has recovered from the installed operating system.

+   * Use free space—Installs Fedora/RHEL in the *free space* (page 30) on the disk. This choice does not work if there is not enough free space.
+   * Create custom layout—Does not alter hard disk partitions. This choice causes Anaconda to run Disk Druid (page 71) so you can preserve those partitions you want to keep and overwrite other partitions. It is a good choice for installing Fedora/RHEL over an existing system where you want to keep */home*, for example, but want a clean installation and not an upgrade.

**Default layout**	The default layout the first four choices create includes two logical volumes (swap and root [//]) and one standard partition (**boot**). With this setup, most of the space on the disk is assigned to the root partition. For information on the Logical Volume Manager, see page 38.

Put a tick in the check box labeled **Encrypt system** to encrypt the filesystems you are creating. If you are installing on more than one disk, you can select which drive the system boots from. See the tip on page 35.

**Disk Druid**	Anaconda runs Disk Druid only if you put a tick in the check box labeled **Review and modify partitioning layout** or if you select **Create custom layout** from the drop-down list as described earlier. You can use Disk Druid to verify and modify the layout before it is written to the hard disk. For more information refer to “Using Disk Druid to Partition the Disk” on page 71.

**Warning**	Anaconda displays a warning if you are removing or formatting partitions. Click **Yes**, **Format**, or **Write changes** to disk to proceed.