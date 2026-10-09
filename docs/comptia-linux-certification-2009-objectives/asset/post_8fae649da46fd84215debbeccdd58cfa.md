
## Bootloader Problems

If a user is unable to boot a system, it may be due to disk errors caused by the bootloader or hardware devices.

RHEL5 does not support LILO.

| Symptom | Cause And Solution |
| :--- | :--- |
| An error message “L” is displayed. | **Cause:** LILO is unable to load the /boot/boot.b file.<br>**Solution:** Use the boot disk to boot the system and reinstall LILO. |
| An error message “LI” is displayed. | **Cause:** LILO is unable to locate the /boot/boot.b file or it could be any disk error.<br>**Solution:** Log in to the rescue mode and reinstall LILO. |
| An error message “LIL” is displayed. | **Cause:** LILO is unable to locate the /boot/map file.<br>**Solution:** Log in to the rescue mode and reinstall LILO. |
| An error message “LILO” is displayed with scrolling zeros and ones. | **Cause:** The hard disk is not supported by BIOS.<br>**Solution:** Update BIOS or change the motherboard or the hard disk. |
| The Kernel Panic message is displayed. | **Cause:** The filesystem is corrupted or inaccessible.<br>**Solution:** Log in to the rescue mode and perform the integrity check on the filesystem. |

## How to Troubleshoot Linux-Based Issues

### Procedure Reference: Analyze the Problem by Gathering Data

To analyze the problem by gathering data:

1. Log in as root in the CLI.
2. Gather data about the issue using appropriate commands and files.
   - Enter `history` to analyze the history of commands run by the user.
   - Enter `grep {keyword} {log file name}` to find the specified keyword in the log file while troubleshooting.
   - Enter `diff {current file} {backed up file}` to view if there are any changes in the file compared with the last backed up state.
   - Enter `find {location of the directory to search} -cmin -{time in minutes}` to find all files that have been modified within a specified timing.
   - Enter `strace {command}` to collect more information when the specified command is run.
   - Enter `tail -f {log file name}` to view the log file as and when it is updated.
   - Configure system logs to log all debug messages.
     1. Enter `vi /etc/syslog.conf` to open the system log configuration file.
     2. Type `{Facility} {Level of severity} {File where the log messages will get stored}` to set the type and level of severity to be logged in the specified file.
     3. Save and exit.
     4. Enter `service syslog restart` to restart the system log service and apply the changes.

## Troubleshooting the Boot Process

| **Cause** | **Solution** |
| :--- | :--- |
| If the bootloader screen does not appear, then GRUB may not be properly configured. | Configure the `/boot/grub/grub.conf` in the rescue mode. |
| If the **grub>** prompt appears, then GRUB may be corrupted. | Install GRUB again in the rescue mode. |
| If the kernel does not load, then the kernel image may be corrupted. | Install a new kernel in the rescue mode. |
| If the kernel does not load, then the parameter passed during the system start up may be wrong. | Specify the correct parameter by editing GRUB in the bootloader screen. |
| If there is a kernel panic, then: | 1. In the rescue mode, configure the bootloader configuration.<br>2. In the rescue mode, define the parameters in the `/etc/inittab` file correctly.<br>3. In the rescue mode, run a filesystem check on the filesystem. |
| *   The bootloader may have been misconfigured. |
| *   The `/etc/inittab` file is misconfigured. |
| *   Or, the root filesystem is misconfigured. |
| If the kernel loads, but `/etc/rc.d` causes an issue, then the `/etc/fstab` file may have an error. | In the rescue mode, fix the `/etc/fstab` file. |
| If the kernel loads, but `/etc/rc.d` causes an issue, then the `fsck` utility may have failed. | In the rescue mode, run the `fsck` command manually. |

| Cause | Solution |
| :--- | :--- |
| If the services do not start correctly, then they may not have been configured properly. | Configure the services properly. |

## Procedure Reference: Use the Linux Rescue Environment

To use the Linux rescue environment:

1. Modify the BIOS settings to boot from the recovery disc.
2. Insert the first Red Hat installation CD into the CD-ROM drive and boot the system.
3. At the boot prompt, enter `linux rescue` to enter the rescue mode.
4. If necessary, specify settings necessary to access the installation files.
   - Specify the language and keyboard settings.
   - On the **Setup Networking** page, select **Yes**.
   - On the **Network Configuration** page, specify the networking parameters for **eth0** and then select **OK**.
5. A message is displayed, stating that the root partition will be mounted in the `/mnt/sysimage` directory. Select **Continue** to mount the filesystem with read and write permissions.
6. Select **OK** to continue with the boot process.
7. The root directory is now mounted on the ramdisk. Enter `chroot /mnt/sysimage` to change the root directory to the one mounted in the `/mnt/sysimage` directory.
8. Troubleshoot to find the cause of system failure and make the necessary changes to recover the system. For example, if the system failed to boot due to inaccuracies in the LILO configuration file, modify the file and then reinstall LILO.
9. Enter `exit` to exit the chroot environment.
10. Enter `sync` so that the changes you made are reflected in the filesystem on the hard disk.
11. Enter `exit` to exit from the rescue mode. The system will now reboot.

# ACTIVITY 16-1
## Troubleshooting GRUB

**Before You Begin:**

1. On srvB, you have logged in as root in the CLI.
2. At the command line, enter `cd /boot/grub` to open the GRUB directory.
3. Enter `cp grub.conf grub1.conf` to back up the existing GRUB configuration file.
4. Enter `vi grub.conf` to open the current GRUB configuration file.
5. Comment all the lines.
6. Save and close the file.
7. Enter `reboot` to apply the settings.

**Scenario:**

Your system boots with the **grub** prompt rather than booting from the GUI prompt. Even after reboot, the situation remains the same. This indicates that there is an issue with the GRUB configuration. You require the system to boot through the GUI.

| What You Do | How You Do It |
| :--- | :--- |
| 1. Correct the GRUB settings. | a. At the **grub** prompt, enter `root`<br>b. Enter `cat /grub/grub.conf` to view the current bootloader settings.<br>c. Make a note of the kernel and module settings and press **Enter** to return to the **grub** prompt.<br>d. Enter `clear` to clear the terminal screen.<br>e. Enter `kernel /vmlinuz-2.6.18-128.el5 ro root=LABEL=/ rhgb quiet`<br>f. Enter `initrd /boot/initrd-2.6.18-128.el5.img`<br>g. At the **grub** prompt, enter `boot` to reboot the system. |
| 2. Check the corrected grub.conf file to ensure that the settings are correct. | a. Press **Ctrl+Alt+F1** to switch to the CLI.<br>b. Log in as **root** in the CLI.<br>c. Enter `cd /boot/grub/` to navigate to the grub directory.<br>d. Enter `rm grub.conf` to delete the current GRUB configuration file.<br>e. Enter `y` to confirm the remove action.<br>f. Enter `mv grub1.conf grub.conf` to replace the correct GRUB configuration file.<br>g. Enter `cat grub.conf` to view the current grub.conf file.<br>h. Enter `clear` to clear the terminal screen. |

# ACTIVITY 16-2
## Troubleshooting Partitions

**Before You Begin:**

1. On *srvB*, you have logged in as root in the CLI.
2. Enter `cd /root` to change to the root directory.
3. Enter `e2label /dev/sda2 /boo` to change the filesystem label.
4. Enter `reboot` to apply the settings.

**Scenario:**

A new employee, Jim, accidentally manipulated some files. When he tried booting the machine, he gets the error message "Checking filessystems. fsck.ext3: Unable to resolve 'LABEL=/boo'."

| What You Do | How You Do It |
| :--- | :--- |
| 1. Troubleshoot the partition label issue. | a. At the command prompt, enter the root password.<br>b. At the **Repair filesystem** prompt, enter `cat /etc/fstab` to view label entries of all partitions.<br>c. Enter `fdisk -l` to view the boot device information.<br>d. Observe that the boot device partition is `/dev/sda1`.<br>e. Enter `e2label /dev/sda1` to check if the label name is the same as that in the `/etc/fstab` file.<br>f. Observe that the boot directory information is specified as `/boo` instead of `/boot`.<br>g. Enter `e2label /dev/hda1 /boot` to rectify the mistake in labeling.<br>h. Press **Ctrl+D** to reboot the system. |
| 2. Check whether the system recovered. | a. Verify that the system reboots and the GUI login screen is displayed.<br>b. Log in as **root** in the GUI. |
