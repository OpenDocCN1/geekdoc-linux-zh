effective filesystem root"), meaning that to the user, /var/ftp appears to be the server root /. Nothing outside /var/ftp is accessible or even visible. A regular account user can enter a command such as cd /usr/local to move to any part of the system and access files with the same readability permissions as in a terminal session, but an anonymous FTP user can't get out of /var/ftp at all. An anonymous user who enters cd /pub will be taken to /var/ftp/pub.

# Enabling Anonymous FTP Access

By default, anonymous FTP is not enabled; the easiest way to enable it, if you choose to do so, is through sysinstall. Run /stand/sysinstall; then enter the Configure and Networking sections. Scroll to the Anon FTP option, and press the spacebar to enter the Anonymous FTP Configuration screen, as shown in Figure 24.2.

FIGURE 24.2
Anonymous FTP
configuration options.

![](bbox=[0.35, 0.5, 0.65, 0.7])

The default options are generally appropriate for a typical FreeBSD system. The UID, Group, and Comment fields control how the new ftp user will be created. This user's home directory is set to /var/ftp, which is how anonymous FTP works—the ftp login is treated as a regular user that behaves as if it's listed in /etc/ftpchroot, so anybody logging in as ftp (or its alias, anonymous) will be put into a chroot jail at /var/ftp.

You can change any of the fields to suit your system (for instance, if you already have a user with a UID of 14, or if you want a name for the upload directory that's different from incoming). When you select OK at the bottom of the screen, the ftp user will be created, as will the /var/ftp tree with its necessary subdirectories.

# Disabling Anonymous FTP Access

The /stand/sysinstall program doesn't provide the capability to disable anonymous FTP after it's been enabled, but you can do this a number of ways (any of the following will do the job):

+   - Remove the /var/ftp tree.