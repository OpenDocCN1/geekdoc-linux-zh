# Part IV: Fedora and RHEL Network and Server Setup

+   - php.conf — Identifies and loads the libphp module so that your Web pages can include PHP scripting language. There is also a Directory setting that allows an index.php file you add to a directory to serve as a directory index. (Install the php package.)

+   - python.conf — Identifies and loads the mod_python module so Web pages include Apache handlers written in Python. (Install the mod_python package.)

+   - squirrel.conf — Identifies the location of the SquirrelMail Web-based interface so that it can be incorporated into your Apache Web server. To see the SquirrelMail login screen, type http://localhost/webmail in a browser window. (Install the squirrel package.)

+   - ssl.conf — Configure SSL so that Apache knows how to serve pages requested over a secure connection (https). (Install the mod_ssl package.)

+   - subversion.conf — Loads the mod_dav_svn and mod_auth_svn modules to let you set a Subversion repository from Apache. By uncommenting lines in this file, you can set /home/svnroot as the location where you hold authorization files. (Install the mod_dav_svn package.)

+   - webalizer.conf — Lets you identify who access the webalizer data (statistics about your site). (Install the webalizer package.)

+   - wordtrans.conf — Identifies the location of the WordTrans translation window so that it can be incorporated into your Apache Web server. To see the WordTrans login screen, type http://localhost/wordtrans in a browser window. (Install the mod_auth_pgsql package.)

These configuration files are read when the httpd server starts. The information in these files could have been added to httpd.conf. However, files are put so that different packages can add their configuration settings without having the RPM software package incorporate some automated method of adding their configuration information to the httpd.conf file.

# Starting and Stopping the Server

The procedure for starting and stopping the Apache Web server is no different from that of many other daemons. You can use the chkconfig command to set the httpd service to start at boot time.

> CROSS-REFERENCE: See Chapter 12 for detailed information on the inner workings of the shell scripts that control starting and stopping daemons and server processes.

The /etc/init.d/httpd shell script accepts any of a handful of command-line arguments. If it is called with the argument start, the httpd script will run one master daemon process (owned by root), which will spawn other processes (equal to the number specified