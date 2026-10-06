![](bbox=[0.158, 0.116, 0.342, 0.283])

A significant portion of the RHCE exam requires you to troubleshoot and fix broken system configurations. To do so, you must boot the system in single-user or rescue mode, find the problem, and fix it. This chapter explains single-user and rescue mode operation and gives general procedures for troubleshooting systems.

# System Recovery

F rom time to time, you may attempt to boot a Linux system only to find that the system won't boot. You may see error messages pointing to problems such as:

+   * Missing or corrupt LILO installation
* Kernel panic
* Missing or corrupt kernel
* Damaged file system
* Inability to enter runlevel 2, 3, or 5
* Unknown root password

To fix the system, you must boot it. Unless the system is suffering from a hardware problem, you'll probably be able to boot it either single-user mode or rescue mode. Once you succeed in booting the system, you can study its configuration files and logs to determine the cause of the problem, fix the problem, and reboot the system. The next section explains single-user mode and single-user mode recovery procedures. The following section explains rescue mode and rescue mode recovery procedures.