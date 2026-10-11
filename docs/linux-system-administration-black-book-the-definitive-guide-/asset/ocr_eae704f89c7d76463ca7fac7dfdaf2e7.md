# # Immediate Solutions

# ## Changing The Active Shell

To change which shell is currently active for your account, do the following:

+   1. Log in to the account you want to set the shell in.
+   2. Type “chsh -l” to see what shells you have available to you, including their full pathname. With the default Red Hat installation, you should have the following available:

/bin/bash
/bin/sh
/bin/ash
/bin/bash
/bin/tcsh
/bin/csh

+   3. Type “chsh -s /path/shell” to change the default shell for your account.

> > **TIP:** If you want to do this for someone else’s account as root, you can either change the shell entry for their account in the /etc/passwd file or type “chsh -s /path/shell -u user”.

# ## Installing The Public Domain Korn Shell

To install the public domain korn shell in Red Hat Linux, do the following:

+   1. Log in as root.
+   2. Insert the Red Hat CD-ROM into the CD-ROM drive, if necessary.
+   3. Type “mount /mnt/cdrom” to mount the CD-ROM onto the file system, if necessary.
+   4. Type “cd /mnt/cdrom/RedHat/RPMS” to change to the packages directory on the CD-ROM.
+   5. Type “rpm -ivh pdksh” and press Tab to complete the file name, and then press Enter to install the shell. It will now show up when you use the chsh command.