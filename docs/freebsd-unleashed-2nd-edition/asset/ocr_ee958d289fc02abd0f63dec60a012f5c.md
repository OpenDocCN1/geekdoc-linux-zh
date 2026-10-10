# # Configuring the FTP Server

The FTP service involves a fairly large number of configuration files; some of them exist in /etc, and some are in /var/ftp/etc. The reason for this is that some of the files have to be accessible by anonymous FTP users, and, as you’ve seen, such users can’t see any files outside of /var/ftp. Here are a few of the files in /etc that apply globally to the FTP server as a whole (not all of them exist in the default installation—some must be created manually):

+   - /etc/ftppusers—A “blacklist” of users who are disallowed FTP access. Add usernames to this file to prevent them from logging in via FTP.
+   - /etc/ftpchroot—Any users listed in this file will be placed in a chroot “jail,” similar to that of anonymous FTP, limiting the user’s access solely to his or her home directory.
+   - /etc/ftphosts—Allows you to configure virtual hosts, much like with Apache (as you saw in Chapter 25, “Configuring a Web Server”). You’ll learn more about virtual hosting later in this chapter.
+   - /etc/ftpwelcome—A welcome notice. The contents of this file are displayed to everyone who connects, immediately after the connection is opened, before the login prompt.
+   - /etc/ftpmotd—A second welcome notice (message of the day); this one appears after a regular account user has logged in.
+   - /etc/shells—You encountered this file in Chapter 11, “Customizing the Shell.” Its purpose is to ensure that anybody logging in to the system has a valid shell, thus preventing people from logging in to accounts such as bin, tty, and nobody, which don’t have shells listed in this file.

Beyond the config files in /etc, a number of additional files control anonymous FTP. These aren’t just config files, either. If /var/ftp is mapped to / for anonymous users, that means the tools in the system binary directories (such as /bin) are inaccessible as the files in /etc. The FTP server relies on a few system tools—notably /bin/ls and /bin/date—to generate file listings to send to the client. These tools have to be available to anonymous users, too; that’s what the /var/ftp/bin directory is for.

The /var/ftp tree contains the following files and directories. Any anonymous user can see these files, but none of them are inherently “dangerous” for users to see (the /var/ftp/etc files don’t contain any passwords, for example):

+   - /var/ftp/bin—This directory contains ls and date executables. These are provided because they’re necessary for the FTP server to be able to generate directory listings, and the system /bin/ls and /bin/date programs are not available if you’ve configured the server to chroot or have limited the anonymous FTP user’s access to within /var/ftp. (This is the default behavior.)