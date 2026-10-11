
## Almost all YaST installation dialogs use the same format:

- The left side displays an overview of the installation status.
- From the lower left side, you can select a help button to get information about the current installation step.
- The right side displays the current installation step.
- The lower right side provides buttons for navigating to the previous or next installation steps, or for aborting the installation.

![](img/63e88022bf135307e3eac051ad238b5b_27_0.png)

If the installation program does not detect your mouse, you can use the Tab key to navigate through the dialog elements, the arrow keys to scroll in lists and Enter to select buttons. You can change the mouse settings later in the installation process.

From the language dialog, select the language of your choice, and then select **Next** to continue to the next step, the **License Agreement**.

You have to select **Yes, I agree to the License Agreement** to get to the next step by selecting **Next**.

## Select the Installation Mode

If there is no operating system installed on your computer, the installation mode dialog offers only **New Installation**. (Update and Other cannot be selected in this case.)

If YaST detects another SUSE Linux installation, you are offered more options, some of which are only available after selecting **Other**, like in the following:

![](img/63e88022bf135307e3eac051ad238b5b_28_0.png)

- **New Installation.** Performs a normal new installation of SLES 10. This is the default option.
- **Update.** Updates a previously installed SLES 9 installation.
- **Other.** Offers two more options:
  - **Repair Installed System.** Repairs a previously installed SLES 10 installation.
  - **Boot Installed System.** Boots a previously installed Linux installation.
- **Abort Installation.** Terminates the installation process.

For a normal installation, select **New Installation** and then select **Next** to proceed to the next step.

## Set the Clock and Time Zone

YaST selects the time zone of the installed system according to your language selection. Change the time zone if you are located in a different one.

![](img/63e88022bf135307e3eac051ad238b5b_29_0.png)

If your hardware clock is set to UTC (Universal Time Coordinated) the system time is set according to your time zone and automatically adjusted to daylight saving time. If your hardware clock is set to local time, select Local Time instead of UTC in the drop-down menu.

## Understand and Change the Installation Settings

YaST analyzes the system and creates an installation proposal. The proposed settings are displayed on two tabs, as in the following figure; **Overview** shows the main categories:

![](img/63e88022bf135307e3eac051ad238b5b_30_0.png)

The proposal displays installation settings that are necessary for a base installation. You can change these settings by selecting the following headings:

- **Keyboard layout.** Changes the keyboard layout. YaST selects the keyboard layout according to your language settings. Change the keyboard settings if you prefer a different layout.
- **Partitioning.** Changes the hard drive partitioning. If the automatically generated partitioning scheme does not fit your needs, you can change it by selecting this headline.
- **Software.** Changes the software selection. You can select or deselect software.

The Experts tab shows the above options, plus the following:

- **System.** Restarts the hardware detection process and displays a list of all available hardware components. You can change the PCI-ID setup, select single components and view details, or save the list to a file.
- **Add-on Products.** Choose this option to include any add-on products.
- **Booting.** Select this if you want to change any boot loader settings or use Lilo (Linux Loader) instead of GRUB (Grand Unified Bootloader) as boot loader.
- **Time zone.** Opens the Clock and Time Zone dialog described earlier.
- **Default Runlevel.** Changes the runlevel. If a graphical environment is installed, the default is runlevel 5, otherwise it is 3.

Of the settings described above, partitioning and software will be discussed in more detail.

## Verify Partitioning

In most cases, YaST proposes a reasonable partitioning scheme that you can accept without change. However, you might need to change the partitioning manually if

- You want to optimize the partitioning scheme for a special purpose server (such as a file server).
- You want to configure LVM (Logical Volume Manager).
- You have more than one hard drive and want to configure RAID (Redundant Array of Independent Disks).
- You want to delete existing operating systems so you have more space available for your SLES 10 installation.

To partition the hard drive manually, you need to know the following:

- The Basics of Hard Drive Partitioning
- The Basic Linux Partitioning Scheme
- Change YaST’s Partitioning Proposal
- Use the YaST Expert Partitioner

### The Basics of Hard Drive Partitioning

Partitions divide the available space of a hard drive into smaller portions. This lets you install more than one operating system on a hard drive or use different areas for programs and data.

Every hard disk (on an Intel platform) has a partition table with space for four entries. An entry in the partition table can correspond to a primary partition or an extended partition. However, only one extended partition entry is allowed.

A *primary partition* consists of a continuous range of cylinders (physical disk areas) assigned to a particular file system. If you use only primary partitions, you are limited to four partitions per hard disk (because the partition table can only hold four primary partitions).

This is why extended partitions are used. *Extended partitions* are also continuous ranges of disk cylinders, but can be subdivided into logical partitions. *Logical partitions* do not require entries in the main partition table. In other words, an extended partition is a container for logical partitions.

If you need more than four partitions, create an extended partition instead of a fourth primary partition. This extended partition should include the entire remaining free cylinder range. Then create multiple logical partitions within the extended partition. The maximum number of partitions is 15 on SCSI disks and 63 on (E)IDE disks.

It does not matter which type of partitions you use on Linux systems; primary and logical partitions both work well.

### The Basic Linux Partitioning Scheme

The optimal partitioning scheme for a server depends on the purpose of the server.

A SLES 10 installation needs at least two partitions:

- **Swap partition.** This partition is used by Linux to move unused data from the main memory to the hard drive, thus freeing main memory which then can be used by other processes.
- **Root partition.** This is the partition that holds the top (/) of the file system hierarchy, the so-called root directory.

No matter what partition scheme you choose, you always need at least one swap partition and a root partition.

The following guidelines help you determine what you can install depending on the space available on your hard disk for your file system:

- **800 MB.** This allows for a minimal installation with no graphical interface. With this configuration, you can only use console applications.
- **1300 MB.** This allows for an installation with a minimum graphical interface. This includes the X Window system and a few graphical applications.
- **2 GB.** This holds the default installation proposed by YaST. This configuration includes a modern desktop environment (such as KDE or GNOME), and provides enough space for several additional applications.
- **4 GB.** This allows for a full installation, including all software packages shipped with SLES 10.

You can put certain directories on separate partitions. If you do this, your root partition can be smaller than outlined above. Any space for data needs to be added to the above.

> As today’s computers are equipped with hard disks with capacities of 100 GB and more, there is still plenty of space for data. Considering the difficulties involved with changing partitions in an installed system and the size of current hard disks, you should therefore allocate much more space than the above minimum when deciding on the hard disk layout.
