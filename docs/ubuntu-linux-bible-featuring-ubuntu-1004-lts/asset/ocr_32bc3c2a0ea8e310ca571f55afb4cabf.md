# Chapter 3: Installing Ubuntu on Special-Purpose Systems

If you select the "Configure network manually" option, the installer displays four additional network configuration screens that respectively prompt you for the server's IP address, the netmask for that IP address of your network gateway, and the name server(s) on your network. (If you want to enter multiple names, separate them by a space, not comma.) Once these screens are displayed, the system's network interface is configured, and you are returned to the installer.

Another problem you may encounter when installing Ubuntu Linux is in contacting and verifying all of the default Ubuntu repositories, which are sites on the Internet that provide new and updated software packages for different Ubuntu releases. If problems occur when contacting the Ubuntu repositories, a dialog about this failure may display during the installation process, and certain repositories may be disabled temporarily.

If you see a message along these lines, you should not be concerned. This is usually a transient, network connectivity or load problem. If you reboot, you will need to uncomment any repositories that were identified in this dialog (Most of these problems occur when contacting the security repositories.) To uncomment them, use your favorite text editor via a command such as vi /etc/apt/sources list. Remove the mask at the beginning of each of the lines associated with the specified repositories, save the modified file, and execute the command sudo apt-get update to verify that the new repositories can be contacted successfully. See Chapter 19 for more information about the Ubuntu repositories and software management utilities.

# Manually Specifying Your Partition Layout

Manually specifying the layout of the partitions on your system can be useful, but it is also timeconsuming and requires some understanding of the Linux filesystem. Manually partitioning your system enables you to put specific directories from the Linux filesystem on their own partitions, which can improve performance, minimize the size of backups for your system (backups are usually done on a per-filesystem or per-directory basis), and simplify future upgrades and system reconfiguration.

# Note

If you are installing Ubuntu for the first time or are relatively unfamiliar with Linux, I'd suggest letting the Ubuntu installer automatically partition your disk for you. Automatic partitioning will get you up and running much more quickly, and doesn't require that you understand the content and use of various directories in your Linux system. As you become more familiar with Ubuntu and Linux, you can always subsequently back up your user account to another machine, and then reinstall Ubuntu using manual partitioning.