Such tests are important because a configuration file error can result in your server shutting down when you try to restart it.

# NOTE

When you build and install Apache from source and don't use Fedora's Apache RPM files, start the server manually from the command line as root (such as when testing). You do this for two reasons:

+   - The standalone server uses the default HTTP port (port 80), and only the super-user can bind to Internet ports that are lower than 1024.
+   - Only processes owned by root can change their UID and GID as specified by Apache's User and Group directives. If you start the server under another UID, it runs with the permissions of the user starting the process.

Note that although some of the following examples show how to start the server as root, you should do so only for testing after building and installing Apache. Fedora is set up to run web services as the apache user if you use Fedora RPM files to install Apache.

# Using /etc/rc.d/init.d/httpd

Fedora uses the scripts in the /etc/rc.d/init.d directory to control the startup and shutdown of various services, including the Apache web server. The main script installed for the Apache web service is /etc/rc.d/init.d/httpd, although the actual work is done by the apachectl shell script included with Apache.

# NOTE

/etc/rc.d/init.d/httpd is a shell script and isn't the same as the Apache server located in /usr/sbin. That is, /usr/sbin/httpd is the program executable file (the server); /etc/rc.d/init.d/httpd is a shell script that uses another shell script, apachectl, to control the server. See Chapter 11 for a description of some service scripts under /etc/rc.d/init.d and how the scripts are used to manage services such as httpd.

You can use the /etc/rc.d/init.d/httpd script and the following options to control the web server:

+   - **start**—The system uses this option to start the web server during bootup. You, as root, can also use this script to start the server.
+   - **stop**—The system uses this option to stop the server gracefully. You should use this script, rather than the kill command, to stop the server.
+   - **reload**—You can use this option to send the HUP signal to the httpd server to have it reread the configuration files after modification.
+   - **restart**—This option is a convenient way to stop and then immediately start the web server. If the httpd server isn't running, it is started.