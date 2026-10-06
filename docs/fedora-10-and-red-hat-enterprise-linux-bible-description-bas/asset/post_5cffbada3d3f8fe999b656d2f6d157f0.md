
# Part IV: Fedora and RHEL Network and Server Setup

- php.conf — Identifies and loads the libphp module so that your Web pages can include PHP scripting language. There is also a Directory setting that allows an index.php file you add to a directory to serve as a directory index. (Install the php package.)

- python.conf — Identifies and loads the mod_python module so Web pages include Apache handlers written in Python. (Install the mod_python package.)

- squirrel.conf — Identifies the location of the SquirrelMail Web-based interface so that it can be incorporated into your Apache Web server. To see the SquirrelMail login screen, type http://localhost/webmail in a browser window. (Install the squirrel package.)

- ssl.conf — Configure SSL so that Apache knows how to serve pages requested over a secure connection (https). (Install the mod_ssl package.)

- subversion.conf — Loads the mod_dav_svn and mod_auth_svn modules to let you set a Subversion repository from Apache. By uncommenting lines in this file, you can set /home/svnroot as the location where you hold authorization files. (Install the mod_dav_svn package.)

- webalizer.conf — Lets you identify who access the webalizer data (statistics about your site). (Install the webalizer package.)

- wordtrans.conf — Identifies the location of the WordTrans translation window so that it can be incorporated into your Apache Web server. To see the WordTrans login screen, type http://localhost/wordtrans in a browser window. (Install the mod_auth_pgsql package.)

These configuration files are read when the httpd server starts. The information in these files could have been added to httpd.conf. However, files are put so that different packages can add their configuration settings without having the RPM software package incorporate some automated method of adding their configuration information to the httpd.conf file.

# Starting and Stopping the Server

Chapter 21 Setting Up a Web Server

The procedure for starting and stopping the Apache Web server is no different from that of many other daemons. You can use the chkconfig command to set the httpd service to start at boot time.

> CROSS-REFERENCE: See Chapter 12 for detailed information on the inner workings of the shell scripts that control starting and stopping daemons and server processes.

The /etc/init.d/httpd shell script accepts any of a handful of command-line arguments. If it is called with the argument start, the httpd script will run one master daemon process (owned by root), which will spawn other processes (equal to the number specified by the StartServers directive owned by the user apache (from the User and Group directives). These processes are responsible for responding to HTTP requests. If called with stop, the server will be shut down after all http processes are terminated.

If a command-line argument of restart, the script will simply execute and send the hang signal (-HUP) to the master httpd daemon, which as reload causes it to reread its configuration files and restart all the other httpd processes. The shell script also supports an argument of status, which will report the daemon is running and, if it is, the PIDs of the running processes. All command-line arguments result in an error and cause a usage message to be printed.

The actual binary for Apache, /usr/bin/httpd, supports several command-line arguments, although the default values are typically used. The possible command-line arguments are listed in Table 21-7.

## Table 21-7: Command-Line Arguments to httpd

| Argument | Description |
|---|---|
| -c directive | Read the configuration files and then process the directive. This may supersede a definition for the directive within the configuration files. |
| -C directive | Process the directive and then read the configuration files. The directive may alter the evaluation of the configuration file, but it may also be superseded by another definition within the configuration file. |
| -d directory | Use directory as the ServerRoot directive, specifying which module, configuration, and log file directories are located. |
| -D parameter | Define parameter to be used for conditional evaluation within the If directive. |
| -f file | Use file as the ServerConfigFile directive, rather than the default of /etc/httpd/conf/httpd.conf. |
| -h | Display a list of possible command-line arguments. |
| -l | List the modules linked into the executable at compile time. |
| -L | Print a verbose list of directives that can be used in the configuration files, along with a short description and the module that contains each directive. |
| -S | List the configured settings for virtual hosts. |
| -t | Perform a syntax check on the configuration files. The results will either be: Syntax OK or an error notification; for example: Syntax error on line 118 of /etc/httpd/conf/httpd.conf |
| -T | Same as -t, except that there is no check of the DocumentRoot value. |
| -v | Print the server information:\nServer version: Apache/2.2.8 (Unix)\nServer built: Feb 25 2008 07:05:32 | |
| -V | List the server information and any values defined during compilation:\nServer version: Apache/2.2.8 (Unix)\nServer built: Feb 25 2008 07:05:32\nServer's Module Magic Number: 2005i1115:11\nArchitecture: 32-bit\nServer compiled with...-D APACHE_MPM_DIR="server/prefork" -D APR_HAVE_MMAP -D APR_HAVE_IPV6 (IPv4-mapped addresses)\n...\nServer settings enabled -D APR_HAVE_SMP | Use with the start, stop, restart, graceful or graceful options to change the current state. |

# Monitoring Server Activities

Apache Web server is a tempting target for someone with a desire to hijack a computer. There are many techniques you can use to secure your server (covered in Chapter 14), which range from SELinux to using certificates to controlling how scripts are. Described here, however, are techniques for keeping an eye on the performance and security. Watching your server carefully can often stop an attack before it gets anywhere.

Apache provides two built-in methods to check the performance and status of your server. The server-status handler can be configured to show information about server processes. The server-info handler can be configured to provide a detailed summary of the configuration. You can activate these by adding the following lines to the /etc/httpd/conf/httpd.conf file:

```
<Location /server-status>
  SetHandler server-status
  Order deny,allow
  Deny from all
  Allow from 127.0.0.1
</Location>

<Location /server-info>
  SetHandler server-info
  Order deny,allow
  Deny from all
  Allow from 127.0.0.1
</Location>
```

In this example, all users from the local computer can display the server-info and server-status pages. You can change 127.0.0.1 to the name of any domain or host that your Apache server is hosting.

## Displaying server information

The Server Information (server-info) page contains the server version information and various general configuration parameters and breaks up the rest of the data by module. Each loaded module is listed, with information about all directives supported by module, and the current value of any directive from module.

The Server Information is usually quite verbose and contains more information than can be displayed in Figure 21-3, which shows only the links to each module's section and the General Server Settings.

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_932_0.png)

Figure 21-3: The server-info page displays server and module information.

## Displaying server status

The contents of the server-status page include version information for the server, the current time, a timestamp of when the server was last started, and the server's uptime. The page also details the status of each server process, choosing from several possible states (waiting for a connection, starting up, reading a request, sending a reply, waiting to read a request).
