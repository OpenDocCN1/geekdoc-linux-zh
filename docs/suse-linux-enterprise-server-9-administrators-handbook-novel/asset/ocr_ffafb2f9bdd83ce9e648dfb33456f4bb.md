# NOTE

If your screen resolution is 800×600, the File Name edit box may be partially hidden if you have the task panel displayed.

If you need to do a one-off backup, you can select the Backup Manually button and walk through the same setup screens described in the preceding paragraphs, but not save the settings in a profile.

To perform a backup, simply select one of the existing profiles and then click Start Backup. YaST takes a few minutes to search through the system for files matching your selection and then creates the resulting archive (see Figure 10.2). The tarball created by YaST has the following “structure”:

```
Athena:/home/admin # tar -tvf backup.tar
-rw------- root/root   143 2005-01-14 06:07:42 info/files
-rw------- root/root   136 2005-01-14 06:07:42 info/packages
-rw------- root/root     6 2005-01-14 06:07:35 info/hostname
-rw------- root/root    17 2005-01-14 06:07:35 info/date
-rw------- root/root     0 2005-01-14 06:07:35 info/comment
-rw------- root/root   127 2005-01-14 06:07:35 info/complete_backup
-rw------- root/root 18754 2005-01-14 06:07:42 info/installed_packages
-rw------- root/root  1679 2005-01-14 06:07:42 NOPACKAGE-20050114-0.tar.gz
```

Instead of the tarfile holding the backed-up files, those files are actually placed in another tarball within the archive, and additional identification information is added. As a result, the YaST System Restore module does not accept a “standard” tarball created by tar unless you have packaged the files into the same structure.

The System Restore module enables restoration of your system from a backup archive. To access the Restore module, from the YaST Control Center, select System, System Restore; the Archive Selection dialog box is then shown (see Figure 10.3). (From a terminal session, you can use yast2 restore or yast restore.) First, specify where the archives are located (removable media, local hard disks, or network file systems). A description and the contents of the individual archives are then displayed, letting you decide what to restore from the archives. There are two dialog boxes for uninstalling packages that were added since the last backup and for the reinstallation of packages that were deleted since the last backup. These two steps let you restore the exact system state at the time of the last backup.