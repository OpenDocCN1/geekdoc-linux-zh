# Installing the Software

Now you need to make sure that you have the required software to use quota. To install the software, use YaST to install the package called quota from the series AP1. To install it, follow these steps:

+   1. Log in as root.
+   2. Make sure that your SuSE installation CD is inserted in the CD-ROM drive.
+   3. Run YaST and choose Install.
+   4. A new menu loads. Choose Change/Create Configuration.
+   5. Choose series AP.
+   6. Look for a package called quota.
+   7. If you have an i next to it, you're fine. If not, then press the space bar to mark the package for installation.
+   8. Press F10 to exit.
+   9. Press Start Installation.
+   10. YaST will start to install the package for you.
+   11. When done, just exit from YaST and you're done.

# Modifying Your System to Run Quota Support

The next step is telling SuSE Linux which filesystems to monitor for quota. Quota only works on the second extended filesystem (ext2). This is the filesystem that is used by Linux by default. To mark a filesystem for monitoring by quota, you need to edit /etc/fstab.

/etc/fstab is the file that contains the information about your filesystems. Open the file in any editor. It should look something like this:

```
/dev/hda7   swap        swap        defaults    0
/dev/hda6   /           ext2        defaults    1
/dev/hda5   /boot       ext2        defaults    1
/dev/hdc    /cdrom      iso9660     ro,noauto,user 0
/dev/fd0    /floppy     auto        noauto,user 0
none        /proc       proc        defaults    0
# End of YaST-generated fstab lines
```

Your system might show something different than this, which is ok. You can see here that you have two ext2 filesystems—the root (/) and the boot (/boot). You are more interested in the root (/) because it is the one that contains the /home directory. You want to control the filesystem that has your users' homes. To enable quota support on a filesystem, add the option usrquota to the fourth field, and to enable group quota, add the option grpquota. For example:

```
/dev/hda7   swap        swap        defaults    0
/dev/hda6   /           ext2        defaults,usrquota,grpquota 1
/dev/hda5   /boot       ext2        defaults    1
/dev/hdc    /cdrom      iso9660     ro,noauto,user 0
/dev/fd0    /floppy     auto        noauto,user 0
```