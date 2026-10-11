The Experts tab shows the above options, plus the following:

+   - **System.** Restarts the hardware detection process and displays a list of all available hardware components. You can change the PCI-ID setup, select single components and view details, or save the list to a file.

+   - **Add-on Products.** Choose this option to include any add-on products.

+   - **Booting.** Select this if you want to change any boot loader settings or use Lilo (Linux Loader) instead of GRUB (Grand Unified Bootloader) as boot loader.

+   - **Time zone.** Opens the Clock and Time Zone dialog described earlier.

+   - **Default Runlevel.** Changes the runlevel. If a graphical environment is installed, the default is runlevel 5, otherwise it is 3.

Of the settings described above, partitioning and software will be discussed in more detail.

# Verify Partitioning

In most cases, YaST proposes a reasonable partitioning scheme that you can accept without change. However, you might need to change the partitioning manually if

+   - You want to optimize the partitioning scheme for a special purpose server (such as a file server).

+   - You want to configure LVM (Logical Volume Manager).

+   - You have more than one hard drive and want to configure RAID (Redundant Array of Independent Disks).