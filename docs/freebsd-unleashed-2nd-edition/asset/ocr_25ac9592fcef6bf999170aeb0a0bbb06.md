![](bbox=[0.35, 0.08, 0.69, 0.25])

FIGURE 26.2 Anonymous FTP configuration options.

You can change any of the fields to suit your system (for instance, if you already have a user with a UID of 14, or if you want a name for the upload directory that’s different from incoming). When you select OK at the bottom of the screen, the ftp user will be created, as will the /var/ftp tree with its necessary subdirectories.

Note that /stand/sysinstall doesn’t provide the capability to disable anonymous FTP after it has been enabled, but you can do this a number of ways. The following methods are ranked in descending order of preferability:

+   - Add the ftp user to /etc/ftpusers (probably the easiest and cleanest method).
+   - Change the permissions on the /var/ftp tree so that its contents can’t be read by regular users—0700 will work.
+   - Remove the /var/ftp tree.
+   - Remove the ftp user.

Similarly, you can disable the upload (incoming) directory by simply removing it, or else by changing its permissions to 755 (the default directory permissions, in which only the owner—root—can write into it). Re-enable it (or any other directory to which you want anonymous users to be able to upload files) by changing its permissions to 1777—for instance, chmod 1777 /var/ftp/incoming.

# Virtual Hosting

If you have multiple IP addresses bound to your machine, you can map different FTP server behaviors to each one. This virtual hosting mechanism is controlled with the /etc/fthosts file, which does not exist in the default FreeBSD system (you need to create it).

Each virtual host is defined on its own line, with fields specifying alternate config files for each host separated by whitespace. Table 26.2 describes the various fields, their meanings, and the default values (the ones that the server uses without an /etc/fthosts file present).