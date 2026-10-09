# # How to Configure a Web Server

# ## Procedure Reference: Install Apache

To install Apache:

+   1. Log in as root.
2. Mount the Linux installation media that contains Apache.
3. Navigate to the /media/name of the media/Server directory.
4. Install the dependency packages for Apache.
    a. Enter `rpm -ivh apr-(version).(release).rpm`.
    b. Enter `rpm -ivh postgresql-libs-(version).(release).rpm`.
    c. Enter `rpm -ivh apr-util-(version).(release).rpm`.
5. Enter `rpm -ivh httpd-(version).(release).rpm` to install Apache.
6. Enter `rpm -qi httpd` to verify that Apache has been installed.
7. If necessary, enter `umount /media/cdrom` to unmount the installation CD.

# ## Procedure Reference: Configure the Apache Web Server

To configure the Apache web server:

+   1. Log in as root.
2. Using the vi editor, open the httpd.conf file.
    - Open the httpd.conf file from the /etc/httpd/conf directory when Apache is installed using RPM.
    - Open the httpd.conf file from the /[Installation Directory]/conf directory when Apache is installed from a user source.

![](bbox=[0.34, 0.53, 0.99, 0.62])

+   3. Locate the ServerAdmin statement and enter the email address of the webmaster.
    `ServerAdmin (email address)`
4. Locate the ServerName option and then enter the IP address of the web server.
    `ServerName (IP address: Port)`
5. Locate the DocumentRoot option and enter the path of the directory that is used to serve web content.
    `DocumentRoot (Absolute path of the web content directory)`
6. Locate the DirectoryIndex option and enter the list of index files for the directory.
    `DirectoryIndex (List of index files)`
7. Save and close the file.
8. Enter `service httpd start` to start the httpd service for the configuration changes to take effect.
9. Enter `chkconfig httpd on` to enable the httpd service during system startup.