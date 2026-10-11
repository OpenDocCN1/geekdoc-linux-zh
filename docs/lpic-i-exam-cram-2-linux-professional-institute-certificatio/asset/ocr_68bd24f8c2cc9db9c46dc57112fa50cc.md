+   ▶ restart—Restarts the httpd daemon (also causes Apache to reread its configuration file)
+   
+   ▶ fullstatus—Reports the status (requires lynx and the mod_status module to be present and compiled into Apache)
+   
+   ▶ graceful—Restarts and lets current connections finish
+   
+   ▶ configtest—Checks syntax in the /etc/httpd/conf/httpd.conf file

Most sysadmins use apache ctl either from the shell to immediately affect the Apache server or from a script to cause actions that occur as part of normal maintenance.

> When you want to shut down Web services but not disconnect currently connected users, use the apache ctl graceful command. It’s designed to allow current connections to finish while disallowing new connections. This is much more acceptable on the users’ end than a cold stop is.

# # Apache Configuration Files

In the past, Apache used two configuration files in contrast to today’s main configuration file:

+   ▶ access.conf—Used to control access to directories and other access-related configuration
+   
+   ▶ srm.conf—Used to set directives or parameters for the server

Some instances of Apache use any or all of the files, depending on how old the server is and how much trouble the consolidation to a single configuration file was perceived to be.

Apache’s main configuration file in later versions is /etc/httpd.conf. Several years ago, the decision was made to move the plethora of configuration files that gathered in the /etc directory tree’s root to reside in their own named directories. This means that on a Red Hat machine, the httpd.conf file is located in /etc/httpd/conf/httpd.conf

On a Debian machine, the file now typically is located in /etc/apache/httpd.conf

> If you’re asked on an exam to choose which files are considered to be configuration files for Apache, all three of the access.conf, srm.conf, and httpd.conf files are valid and possible choices. If you’re asked to choose all that apply, all three would be correct. If you’re asked for a single answer, only httpd.conf is valid.