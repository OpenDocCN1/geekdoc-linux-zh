# # Installing swatch

To install the **swatch** log-analysis tool, do the following:

+   1. Log in as root.
+   2. Type “man swatch” to see whether the **swatch** (Simple Watcher) program is already installed. If it is, skip to the section “Analyzing Logs.”
+   3. Place the first Red Hat CD-ROM in the CD-ROM drive.

> **NOTE:** Not all distributions come with **swatch**. You can FTP this tool from ftp.stanford.edu/general/security-tools/swatch.

+   4. Type “mount /mnt/cdrom” to mount the distribution CD-ROM.
+   5. Type “cd /mnt/cdrom/RedHat/RPMS” to change to the directory that contains the RPMs that come with Red Hat.
+   6. Type “rpm -ivh swatch” and press the Tab key to let the bash shell complete the file name for you.
+   7. Type “umount /mnt/cdrom” to unmount the CD-ROM. You can now remove it from the drive.

# # Analyzing Logs

To watch your log files for signs of trouble, do the following:

+   1. Follow the instructions in the preceding section, “Installing swatch,” to see whether the tool is installed, and if it is not, follow the instructions to install it.
+   2. Log in as root. You need root’s privileges and file access to monitor all the log files.
+   3. Type “vi /etc/swatchrc” to create the **swatch** configuration file.
+   4. Type “i” to enter Insert mode.
+   5. Determine the text you need to watch out for in each of the log files. Unfortunately, no cookie-cutter approach is available for this yet. You have to build your rules based on experience.
+   6. After you know what to watch for, use the format and values discussed in the In Depth section “Log Monitoring With swatch” to build your rules.
+   7. When you are finished, press the Esc key, and then type “ZZ” to save and exit the file.

![](bbox=[0.88, 0.74, 0.99, 0.91])