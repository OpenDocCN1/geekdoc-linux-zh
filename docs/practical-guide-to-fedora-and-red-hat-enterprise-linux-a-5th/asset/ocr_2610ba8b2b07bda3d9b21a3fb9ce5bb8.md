![](bbox=[0.0, 0.09, 0.9, 0.36])

however: When you run out of space on a filesystem on an LV, you can grow (expand) the LV and its filesystem into empty or new disk space, or you can move the filesystem to a larger LV. LVM's disk space manipulation is transparent to users and does not interrupt service.

LVM also eases the burden of storage migration. When you outgrow the PVs or need to upgrade them, LVM can move data to new PVs without interrupting users. To read more about LVM, refer to the resources listing under “More Information” on page 48.

# THE INSTALLATION PROCESS

The following steps outline the process of installing Fedora/RHEL from an install DVD using Anaconda. Installation from other media follows similar steps. See Chapter 3 for the specifics of how to perform the installation.

+   Insert the install DVD in the computer and turn on or reset the computer.

+   After going through computer-specific hardware diagnostics, the system displays the install DVD Welcome menu (Figure 3-4, page 56).

+   You can make a selection from the menu, press TAB, and modify the boot parameters, or wait for a minute without entering anything; the computer brings up the installer from the DVD.

+   As part of the installation process, Fedora/RHEL creates RAM disks (page 1102) that it uses in place of the hard disk used for a normal boot operation. The installer copies tools required for the installation from the install DVD to the RAM disks. The use of RAM disks allows the installation process to run through the specification and design phases without writing to the hard disk and enables you to opt out of the installation at