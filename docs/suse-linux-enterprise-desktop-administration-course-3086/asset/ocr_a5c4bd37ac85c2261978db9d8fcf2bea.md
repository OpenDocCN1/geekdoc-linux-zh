+   - **/proc/dma**—View the DMA (Direct Memory Access) channels used on your Linux system.
+   - **/proc/bus/pci/devices**—View the PCI (Peripheral Component Interconnect) information on your Linux system.
+   - **/proc/scsi/scsi**—View a summary of the SCSI (Small Computer System Interface) information on your Linux system.

# Hardware Information (Command-Line Utilities)

You can use the following utilities from the command-line to view information about the hardware on your Linux system:

+   - **hwinfo**—Generates and displays a list of specific information on the devices installed on your Linux system. If you want to scroll up and down the list, enter `hwinfo | less`.
+   
+     For a summary listing, enter `hwinfo --short`. Enter `hwinfo --log filename` to write the information to a log file.
+   - **hdparm**—With various options, lets you view information about your hard drive and manage certain hard drive parameters.
+   
+     For example, the option `-i` displays hard drive identification information available at boot time. The option `-I` requests information directly from the hard drive.
+   
+     For a summary list of available options, enter `hdparm` or `hdparm -h`.
+   - **fdisk**—Used primarily for managing the partition table on a Linux system. You can also use options such as `-l` (list partition tables), or `-s` (size of partition) to view hard drive information.
+   - **lspci**—Displays information on all PCI buses in your Linux system and all devices connected to them.
+   
+     The options `-v` and `-vv` generate verbose reports. The option `-b` gives you a bus-centric view of all the IRQ numbers and addresses as seen by the cards (instead of the kernel) on the PCI bus.
+   - **siga** *(System Information Gathering)*—Collects information on your system and outputs it in HTML or ASCII format.

# System and Process Information (Command-Line Utilities)

Several command-line tools, including the following, can be used to view system information:

+   - uptime
+   - netstat
+   - uname

Additional utilities are covered in “View and Prioritize Processes.”

**uptime**  You can use the uptime command to display the current time, the length of time the system has been running, the number of users on the system, and the average number of jobs in the run queue over the last 1, 5, and 15 minutes.