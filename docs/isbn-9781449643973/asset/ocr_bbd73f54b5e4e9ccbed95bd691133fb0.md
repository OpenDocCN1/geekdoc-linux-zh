# Laboratory #2

Lab #2: Configure Basic Security Controls on a Fedora Linux Server

# Learning Objectives and Outcomes

Upon completing this lab, students will be able to:

+   * Configure the bootloader with set timeout to 0 and password credential to mitigate tampering with the GRUB loader and the boot sequence of the server
+   * Enable SELinux on a Fedora Linux Server and set it to “permissive” mode
+   * Create a student user account and add it to a user group for managing permissions and applying access controls across the system
+   * Configure user groups with limited sudo access (with password credentials) to log and properly monitor access across the system
+   * Create iptables set to “on” for runlevels 3 & 5 to enable an internal, host-based IP stateful firewall
+   * Set restrictions and permissions for user access to files and system log files

# Required Setup and Tools

This lab does not require the use of the Mock IT Infrastructure - Cisco core backbone network. In addition, the Instructor VM workstation and Student VM workstations should be physically disconnected from the internal network and be isolated on the classroom dedicated layer 2 switch. This will allow for a shared DHCP server to be used to allocate the IP addresses for the instructor and student workstations.

The following are required for this equipment-based lab:

+   A) A classroom workstation (with at least 2 Gig RAM) capable of supporting the removable hard drive with the VM server farm connected to the classroom layer 2 switch.
+   B) An instructor workstation (with at least 4 Gig RAM recommended) that shall act as the Instructor’s demo lab workstation. The instructor will display the Instructor workstation on the LCD projector to demo the loading and configuring of the Instructor VM workstation using VMware Player.
+   C) Students Lab workstations will use their own VM server farm and VM student workstation. VMware Player will be used to run the Student VM and the Target VM.