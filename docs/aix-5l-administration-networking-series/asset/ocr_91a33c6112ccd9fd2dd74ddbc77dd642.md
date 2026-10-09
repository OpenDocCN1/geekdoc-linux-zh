+   • **Installation disks** Normally *hdisk0* and possibly *hdisk1*. (Specify all of the disks in rootvg, even the mirrored drives!) It is important to know he actual location code of the disk you found using the `lsdev -C -l hdisk*` command. Note that *hdisk0* on the old system may be *hdisk2* after booting from the install disk.

+   • **File system sizing** There is an option to resize logical volumes for an exact fit if overallocated.

+   • **Trusted computing base** Turn on high-level system security. TCB cannot be removed without reinstallation of AIX, and TCB can be installed on the system only at initial system installation time. TCB performs a checksum on critical system files to ensure they have not been hacked.

9. Turn the key (if present) to the normal position.

10. After the installation is complete, the system will reboot and the SMIT Installation Assistant screen will be displayed. The SMIT Installation Assistant will help you finish the system configuration. This will include setting the date and time, setting the root password, setting up the network interface, and so on. The Installation Assistant will be displayed at each system boot until you have selected Tasks Completed—Exit To AIX Login to signal that your configuration changes have been completed.

![](bbox=[0.24, 0.65, 0.86, 0.92])