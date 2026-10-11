+   6. It is useful to learn how to read these dialog boxes. If the first line mentions whether or not to support a feature, consider this first before fussing with anything below it. The reason I selected this dialog box as an example is that unless you have a CD-ROM drive that is old enough to not be SCSI, IDE, or anything related to these, you do not need it. Click on the “n” next to Support Non-SCSI/IDE/ATAPI CDROM Drives to deactivate this option. Notice that all the other options in the dialog box are no longer available.
+   7. Click on the Main Menu button to close the dialog box.
+   8. Click on the Native Language Support button to open the Native Language Support dialog box.
+   9. Click on “n” for each language you do not need support for.
+   10. When finished, click on the Main Menu button.
+   11. When you are finished with the configuration, click on the Save And Exit button to save the changes. A dialog box opens.
+   12. Read the contents of the dialog box, which explains that you have just completed configuring your kernel and what the next command in the kernel compilation process is. Then click on OK.

| Related solution: | Found on page: |
| :--- | :--- |
| Getting A Command Prompt | 14 |

# Listing Loaded Modules

To see what kernel modules you currently have loaded, use the **lsmod** command or use **more /proc/modules**.

# Inserting Modules Manually

To insert a kernel module, do the following:

+   1. Use the **cd** command to change to the **/lib/modules** directory.
+   2. View the directory’s contents with the **ls** command. If you have never added a new kernel before, there should be just one subdirectory. This subdirectory is named for the kernel version it serves.
+   3. Change to the appropriate kernel version’s directory.