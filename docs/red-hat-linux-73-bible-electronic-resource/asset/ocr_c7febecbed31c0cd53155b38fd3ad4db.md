# Table C-1: Quick Reference to Network Services

| Feature | Package names | Startup script(s) | Daemon | Configuration file(s) |
| :-- | :-- | :-- | :-- | :-- |
| Web Server | | | | | |
| Web Page Server (Apache) | apache apache-manual apache-devel | /etc/init.d/ httpd | /usr/sbin/ httpd | /etc/httpd/conf/ httpd.conf |
| (Tux) | tux | /etc/init.d/tux | /usr/sbin/ tux | /etc/sysconfig/tux |
| File Servers | | | | | |
| FTP Servers (Wu-ftpd) | wu-ftpd | /etc/init.d/xinetd /etc/xinetd.d/ wu-ftpd | /usr/sbin/ xinetd /usr/sbin/ in.ftpd | /etc/ftpaccess /etc/ftphosts /etc/ftpusers /etc/ftpgroups |
| (Vs-ftpd) | vsftpd | /etc/init.d/xinetd /etc/xinetd.d/ vsftpd | /usr/sbin/ vsftpd | /etc/vsftpd.conf /etc/vsftpd.user_list |
| FTP Server with Kerberos support (Gss-FTP) | krb5-workstation | /etc/init.d/ xinetd /etc/xinetd.d/ gssftp | /usr/sbin/xinetd /usr/ kerberos/sbin/ ftpd | /etc/krb5.conf |
| Samba/Windows File & Printers (SMB) | samba-common samba-client samba-swat | /etc/init.d/smb /etc/init.d/ winbind | /usr/sbin/smbd /usr/sbin/nmbd /usr/sbin/ winbind | /etc/samba/smb.conf |