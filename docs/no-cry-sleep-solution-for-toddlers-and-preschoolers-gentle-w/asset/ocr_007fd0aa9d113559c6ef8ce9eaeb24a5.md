# vsftpd Virtual Hosts

Though the capability is not inherently built in to vsftpd, you can configure and set up the vsftpd server to support virtual hosts. Virtual hosting is where a single FTP server operates as if it has two or more IP addresses. Several IP addresses can then be used to access the same server. The server will then use a separate FTP user directory and files for each host. With vsftpd, this involves manually creating separate FTP users and directories for each virtual host, along with separate vsftpd configuration files for each virtual host in the /etc/vsftpd directory. On Red Hat, vsftpd is configured to run as a standalone service. Its /etc/rc.d/init.d/vsftpd start-up script will automatically search for and read any configuration files listed in the /etc/vsftpd directory.

If, on the other hand, you wish to run vsftpd as a xinetd service, you would have to create a separate xinetd service script for each host in the /etc/xinetd.d directory. In effect, you have several vsftpd services running in parallel for each separate virtual host. The following example uses two IP addresses for an FTP server.

+   - First, create an FTP user for each host. Create directories for each host. (You could use the one already set up for one of the users.) For example, for the first virtual host you could use FTP-host1. Be sure to set root ownership and the appropriate permissions.
+   
+     useradd -d /var/ftp-host1 FTP-host1
+     chown root.root /var/ftp-host1
+     chmod a+rx /var/ftp-host1
+     umask 022
+     mkdir /var/ftp-host1/pub

+   - Set up two corresponding vsftpd service scripts in the /etc/xinetd.d directory. On Red Hat, the vsftpd directory in /usr/share/doc has an xinetd example script, vsftpd.xinetd. Within each, enter a bind command to specify the IP address the server will respond to.
+   
+     bind 192.168.0.34

+   - Within the same scripts, enter a server_args entry specifying the name of the configuration file to use.
+   
+     server_args = vsftpd-host1.conf

+   - Within the /etc/vsftpd directory, create separate configuration files for each virtual host. Within each, specify the FTP user you created for each, using the ftp_username entry.
+   
+     ftp_username = FTP-host1

# vsftpd Virtual Users

Virtual users can be implemented by making use of PAM to authenticate authorized users. In effect, you are allowing access to certain users, while not having to actually set up accounts for them on the FTP server system. First create a PAM login database file to use along with a PAM file in the /etc/pam.d directory that will access the database. Then create a virtual FTP user along with corresponding directories that the virtual users will access