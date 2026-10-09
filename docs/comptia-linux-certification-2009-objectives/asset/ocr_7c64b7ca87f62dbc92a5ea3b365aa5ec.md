| Cause | Solution |
|---|---|
| If the services do not start correctly, then they may not have been configured properly. | Configure the services properly. |

# Procedure Reference: Use the Linux Rescue Environment

To use the Linux rescue environment:

+   1. Modify the BIOS settings to boot from the recovery disc.
2. Insert the first Red Hat installation CD into the CD-ROM drive and boot the system.
3. At the boot prompt, enter `linux rescue` to enter the rescue mode.
4. If necessary, specify settings necessary to access the installation files.
    a. Specify the language and keyboard settings.
    b. On the **Setup Networking** page, select **Yes**.
    c. On the **Network Configuration** page, specify the networking parameters or **eth0** and then select **OK**.
5. A message is displayed, stating that the root partition will be mounted in the `/mnt/sysimage` directory. Select **Continue** to mount the filesystem with read and write permissions.
6. Select **OK** to continue with the boot process.
7. The root directory is now mounted on the ramdisk. Enter `chroot /mnt/sysimage` to change the root directory to the one mounted in the `/mnt/sysimage` directory.
8. Troubleshoot to find the cause of system failure and make the necessary changes to recover the system. For example, if the system failed to boot due to inaccuracies in the LILO configuration file, modify the file and then reinstall LILO.
9. Enter `exit` to exit the chroot environment.
10. Enter `sync` so that the changes you made are reflected in the filesystem on the hard disk.
11. Enter `exit` to exit from the rescue mode. The system will now reboot.