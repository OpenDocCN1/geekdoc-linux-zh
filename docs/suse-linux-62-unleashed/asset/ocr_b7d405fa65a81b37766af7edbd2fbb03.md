# # Configuring Your FTP Server

Although the default configuration of the FTP server is reasonably secure, you can fine-tune access rights by adding and editing the following files:

+   * /etc/ftpaccess
* /etc/ftpconversions
* /etc/ftphosts

The following file is the FTP logging file. It contains useful information and should be examined on a regular basis.

/var/log/xferlog

With all these files, you can control which connects to your server, when they connect, and from where they can connect. Also, you can create an audit trail of what they do after connecting. The ftpaccess file is the most significant of these because it contains the most configuration options; however, misconfiguring any of the others can lead to denied service.

> **Tip**

When editing any of the files in the /etc directory (FTP-related or not), comment the file liberally and keep backups of original or previously working configuration files. Keeping an edit history at the end of the file—listing who last edited the file, when it was edited, and what was changed—is a good way to track down problems and the source of those problems.

# # Controlling Access—The ftpaccess File

The ftpaccess file is the primary means of controlling who can access your server. Each line in the file defines an attribute or sets its value.

The following commands control access:

+   * class
* autroup
* deny
* guestgroup