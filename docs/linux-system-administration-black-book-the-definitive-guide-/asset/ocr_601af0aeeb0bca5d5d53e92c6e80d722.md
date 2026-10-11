# Immediate Solutions

# Installing Samba

To install Samba on a Red Hat Linux machine, do the following:

+   1. Log on as root to the machine you want to install one or more Samba components on.
+   2. Insert the Red Hat CD-ROM into the CD-ROM drive, if you have not already done so.
+   3. Type “mount /mnt/cdrom” if the CD-ROM is not already mounted onto your file system.
+   4. Before you install either the Samba client or server, you need to install program items needed by both. Type “rpm -ivh samba-common”. Press Tab to expand the file name, and then press Enter to install the package.
+   5. If you want this machine to function as a Samba client, type “rpm -ivh samba-client”. Press Tab to expand the file name, and then press Enter to install the package.
+   6. If you want this machine to function as a Samba server, type “rpm -ivh samba-2”. Press Tab to expand the file name, and then press Enter to install the package.

# Configuring Samba

You should look over some specific items before you proceed to set up particular Samba functions. To set up Samba for general use, do the following:

+   1. Log on as root to the machine on which you want to set up Samba services.
+   2. Type “vi /etc/smb.conf” to open the Samba configuration file.
+   3. Cursor down to the following line:
+   
+   workgroup = MYGROUP
+   
+   4. If you have a Windows workgroup that all of your machines need to be a member of, then change MYGROUP to the workgroup’s name. Be sure to

![](bbox=[0.91, 0.76, 1.0, 0.91])