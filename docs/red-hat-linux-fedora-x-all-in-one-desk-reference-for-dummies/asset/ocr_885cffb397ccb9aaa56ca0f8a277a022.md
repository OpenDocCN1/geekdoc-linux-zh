# 642 Configuring the FTP Server

+   - ascii_download_enable=YES enables file downloads in ASCII mode. Unfortunately, a malicious remote user can issue the SIZE command with the name of a huge file and essentially cause the FTP server to waste huge of resources opening that file and determining its size. This technique is used in a Denial of Service attack (as mentioned later in this section).

+   - ascii_upload_enable=YES enables file uploads in ASCII mode (for text files).

+   - async_abor_enable=YES causes vsftpd to recognize ABORT (abort) requests that arrive at any time. You may have to allow older FTP clients to work with vsftpd.

+   - banned_email_file=/etc/vsftpd.banned_emails specifies the file with the list of banned e-mail addresses (used only if deny_email is set to YES).

+   - chown_uploads=YES allows anonymous files to be owned by a different user specified by the chown_username option. Don't enable this option unless absolutely necessary — and dont root the chown_username (that's a disaster just waiting to happen).

+   - chown_username=NAME specifies the username that owns files uploaded by anonymous FTP users.

+   - chroot_list_enable=YES causes vsftpd to confine all users except those on a list by the chroot_list_file to their home directories they log in for FTP service. This option prevents these users from getting to any other files besides what's in their home directories.

+   - chroot_list_file=/etc/vsftpd.chroot_list is the list of users who are either confined to their home directories or not, depending on the setting of chroot_local_user.

+   - connect_port_20=YES causes vsftpd to make sure that data occurs through port 20 (the FTP data port).

+   - data_connection_timeout=120 is in the seconds after which an inactive connection is timed out.

+   - deny_email_enable=YES causes vsftpd to check a list of banned e-mail addresses and deny access to anyone who tries to log anonymously with a banned e-mail address as password.

+   - dismissage_enable=YES causes vsftpd to display messages when FTP users change to certain directories.

+   - ftpd_banner=Welcome to my FTP service sets the banner that vsftpd displays when a user logs in. You can change the message to anything you want.