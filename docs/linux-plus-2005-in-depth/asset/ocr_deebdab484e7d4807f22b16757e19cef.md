wu-ftpd. To configure vsftpd to host files for other computers to download, provided they log in as the user "user1" with a valid password, you can perform the following steps:

+   1. Create a directory underneath user1's home directory to host the files and ensure that user1 owns this directory.
+   2. At the command prompt, run the command /etc/rc.d/init.d/vsftpd start to start the vsftpd daemon.

Like wu-ftpd, anonymous FTP access is granted by default when the vsftpd daemon is started, and anonymous ftp clients are placed in the /var/ftp directory. In addition, to log in as the root user to vsftpd, you can remove the line root from the /etc/vsftpd.ftppers and /etc/vsftpd.user_list files.

# Configuring NIS

Network Information Service (NIS) can be used to coordinate common configuration files, such as /etc/passwd and /etc/hosts, across several Linux computers within an organization. Each computer that participates in NIS belongs to an NIS domain and uses an NIS map for accessing certain information rather than use the local configuration file. Furthermore, you can configure a master NIS server to send all NIS map configuration to NIS slave servers, which then hand out these NIS maps to all other Linux computers, known as NIS clients.

The most common configuration files that companies use NIS to coordinate are password databases (/etc/passwd and /etc/shadow) such that users can log in to several different Linux servers using the same user name and password. The steps required to set up an NIS server and NIS client for this purpose are shown in the following list:

+   1. Define the NIS domain name by typing the command domainname NIS_domain_name at a command prompt.
+   2. Add the following line to /etc/sysconfig/network to configure the NIS domain from Step 1 at every boot time:
+      NISDOMAIN="*NIS_domain*"
+   3. Edit the file /var/yp/Makefile, navigate to the line that starts with all, and edit the list of files to be made into maps. If you have no slave servers, also ensure that NOPUSH=true is true in this file. If you have slave servers, they must be listed in the /var/yp/yppervers file.
+   4. Add the names or IP addresses of allowed clients to the /var/yp/securenets file.
+   5. Allow the clients from Step 4 access to the appropriate maps in the /etc/ypserv.conf file.
+   6. Start the NIS server daemon by typing /usr/sbin/ypserv at the command prompt.
+   7. Start the NIS password server daemon by typing /etc/init.d.ypasswdd at the command prompt.