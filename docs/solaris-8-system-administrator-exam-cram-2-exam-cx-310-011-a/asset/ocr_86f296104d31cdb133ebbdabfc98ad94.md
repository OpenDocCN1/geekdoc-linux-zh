CD-ROM drive, insert the Device Configuration Assistant floppy disk into the A: drive. If you’re installing over the network, set up an install server and possibly a boot server.

+   10. Reboot the system.

# During the Upgrade

If the current layout of the system disks does not provide enough space for the upgrade, SunInstall uses the auto-layout feature to reallocate disk space as required. If the auto-layout fails or you want to use a different layout, you must manually specify the disk layout.

If the system configuration information was not preconfigured, you need to supply the correct information when prompted.

# After the Upgrade

Merging the existing system configuration with the Solaris 8 operating system might not be completely successful, and you may need to do some manual cleanup. Check the /a/var/sadm/system/data/upgrade_clean file to determine any configuration problems that need to be reviewed and possibly modified before the system can be rebooted.

After resolving any cleanup issues, reboot the system.

# Preconfiguring System Configuration
Information

You can preconfigure the system configuration information required for installation in two ways:

+   ➤ **Name service method**—This method adds the system information to an available name service (NIS or NIS+). During installation, the information is retrieved from the name service and used to configure the system. This is the recommended method for SPARC installations.
+   
+   ➤ **Sysidcfg file method**—This method creates a file named sysidcfg that contains the configuration information. The file must conform to a defined format (keywords and syntax). The file must be available on a local drive, and the local floppy disk drive on the remote drive must be accessible via the network.