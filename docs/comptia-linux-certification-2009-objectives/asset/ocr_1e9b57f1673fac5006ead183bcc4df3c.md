+   2. Create the software RAID 5.

    a. Enter `rpm -qa | grep mdadm` to check if the `mdadm` package is installed on your system.

    b. Observe that the `mdadm` package is listed with the version and release number indicating that it is installed.

    c. Enter `mdadm → --create --verbose /dev/md0 → --level=5 --raid-devices=3 → /dev/sdb7 /dev/sdb8 /dev/sdb9` to create a RAID 5 array.

    d. If necessary, at the prompt, enter `y` to continue creating the array.

    e. Observe that the details about RAID are displayed and the array /dev/md0 is started. Press `Enter` to continue.

    f. Enter `mdadm --detail --scan > /etc/mdadm.conf` to create the RAID configuration file /etc/mdadm.conf with the RAID array information.

+   3. Specify the device information in the mdadm.conf file.

    a. Enter `vi /etc/mdadm.conf` to open the /etc/mdadm.conf file.

    b. On a new line, type `DEVICE /dev/sdb7 /dev/sdb8 /dev/sdb9` to specify the device information.

    c. Press `Esc` to exit the command mode.

    d. Save and close the file.

    e. Enter `clear` to clear the terminal screen.

+   4. Create a filesystem on the RAID device and mount the RAID device on a mount point called /raid.

    a. Enter `mkfs.ext3 /dev/md0` to create an ext3 filesystem on the RAID device /dev/md0.

    b. Observe that the inode tables are written and the journal is created.

    c. Enter `mkdir /raid` to create a mount point for RAID in the /raid directory.

    d. Enter `mount /dev/md0 /raid` to mount the RAID device /dev/md0 on the /raid mount point.