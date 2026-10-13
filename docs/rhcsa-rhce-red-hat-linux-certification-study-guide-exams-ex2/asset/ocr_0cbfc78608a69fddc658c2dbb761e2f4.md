# Regular and Secure Virtual Hosts

+   9. The file associated with secure servers for virtual hosts is ssl.conf in the /etc/httpd/conf.d directory.
+   10. One IP address is required for a name-based virtual server, no matter how many virtual sites are configured.
+   11. To check your configuration of virtual hosts, you can use one of two switches with the httpd command: httpd -S checks the configuration file, including virtual host settings. Alternatively, httpd -D DUMP_VHOSTS focuses on the virtual host configuration, and is therefore also an acceptable answer.

# Deploy a Basic CGI Application

+   12. The Options ExecCGI directive is commonly used in Apache-configured directories that contain CGI scripts such as Perl programs.

# LAB ANSWERS

# Lab I

First, make sure the Apache web server is installed. If an rpm -q httpd command tells you that it is missing, the Web Server package group has not yet been installed. The most efficient way to do so is with the yum groupinstall "Web Server" command. (To find appropriate package group names, run the yum grouplist command.) This assumes a proper connection to a repository, as discussed in Chapter 7.

To configure Apache to start, run the apachectl start command. To make sure it starts the next time the system is booted, run the chkconfig httpd on command.

Once Apache is installed, you should be able to access it from a browser via http://localhost. From the default Apache configuration file, you can verify that the DocumentRoot is located in /var/www/html. You can copy the index.html file from the /usr/share/doc/HTML/en-US directory to the /var/www/html directory. Then you can test the result by navigating once again to http://localhost. If you did not copy the other files associated with the default home page, the display will be missing some icons, but that's not an issue for this lab.