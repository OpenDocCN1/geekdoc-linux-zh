# Samba

Microsoft Windows computers communicate with each other through a language that uses server message blocks (SMB). Linux emulates this language through the Samba system. You need two daemons to run Samba: smbd and nmbd. The smb daemon is the common language; the nmb daemon allows Linux to recognize and use Microsoft-based computer names. Once Samba is set up, you can browse Linux computers as easily as any other Microsoft Windows computer in the Windows Network Neighborhood. And you can browse Microsoft Windows systems just as easily from Linux.

The sharing of directories and printers is set up in the /etc/samba/smb.conf or /etc/smb.comf configuration file. You can set up Samba to share in a Microsoft Windows domain governed by Windows NT/2000 servers or workstations, or you can set up Samba to share in Workgroups with Windows 95/98/ME systems.

# sendmail

When you set up email for your users, you can assign addresses through your ISP, or you can set up your own email server. If your users have a lot of email, you may want to set up your own mail server. Depending on your distribution, sendmail or smail is the mail server of choice. You can set up sendmail to carry messages through common receipt protocols, such as POP (Post Office Protocol) or IMAP (Internet Message Access Protocol). You can also set up sendmail to transmit messages through other mail protocols such as SMTP (Simple Mail Transfer Protocol).

*Note: Mail servers that use POP often use an updated version known as POP3. Similarly, the current version of IMAP is known as IMAP4.*

Sendmail is known as a mail transfer agent. Sendmail user accounts are based on files in the /var/spool/mail directory.

# Apache

The Linux Web server is known as Apache. When you set up Apache on Linux, you install the http daemon, httpd. You can configure Apache based on three files in your /etc/httpd/conf directory:

+   - access.conf—Sets up directories for use by your browser. The directory that you specify in this file becomes home to your home page file.
+   - httpd.conf—Is the main Apache configuration file. You can set up multiple Web sites on one computer (virtual hosting) through this file.
+   - srm.conf—Defines directory names that come after the fully qualified domain name.