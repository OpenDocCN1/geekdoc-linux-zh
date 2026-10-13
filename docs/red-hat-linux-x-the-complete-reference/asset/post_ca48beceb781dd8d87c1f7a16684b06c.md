
## Table 21-4: ProFTPD Configuration Directives, proftpd.conf

| Directive | Description |
|---|---|
| MaxLoginAttempts number | Maximum number of times a client may attempt to log in to the server during a given connection. |
| Order allow, deny\|deny, allow | Configures the order that Allow and Deny directives are checked inside a <Limit> block. Default: Order allow,deny Context: <Limit> |
| PersistentPasswd on\|off | When on, proftpd, during login, opens the system-wide /etc/passwd, /etc/group files, accessing them even during a chroot operation that changes the root directory. |
| ServerAdmin "admin-email-address" | E-mail address of the server or virtual host administrator. |
| ServerType type-identifier | The server daemon's operating mode, either inetd or standalone. |
| TimeoutIdle seconds | Maximum number of seconds proftpd allows clients to stay connected without any activity. Default: TimeoutIdle 600 |
| Umask octal-mask | Permissions applied to newly created file and directory within a given context. |
| User userid | The user the proftpd daemon runs as. |
| UserAlias login-user userid | Maps a login name used by a client to a user ID on the server. A client logging in as login-user is actually logged in as user ID. Often used inside an <Anonymous> block to allow specified login-names to perform an anonymous login. |
| <VirtualHost address> | Configuration directives that apply to a particular hostname or IP address. Often used with virtual servers that run on the same physical machine. The block is terminated with a </VirtualHost> directive. |

## The Washington University FTP Daemon: WU-FTPD

The Washington University FTP server, though widely used, is no longer included with Red Hat 9 and up. The name of the Washington University FTP daemon is wu-ftpd; it must be running to allow FTP access by remote users. As with other servers, you can start the FTP server at boot time, through xinetd when a request is received, or directly from the command line. By default, the wu-ftpd server is installed to run using xinetd. The use of xinetd for the servers is described in detail in Chapter 20. The command name for the FTP server invoked by xinetd is in.ftpd. This is a link to the wu-ftpd command. xinetd will run a file called wu-ftpd located in the /etc/xinetd.d directory.

You can use numerous configuration options to tailor your FTP server to your site's particular needs. WU-FTPD makes use of several configuration files located in the system's /etc directory. All begin with the pattern ftp. The primary configuration file is named ftpaccess. Here, you provide basic server information and access for specified directories. The ftphosts, ftpusers, and ftpgroups files control access by systems, particular users, and groups. ftpconversions specifies how archive and compression operations are to be performed on files before or after they are transferred. xferlog is the log file that stores a running log of all transactions performed by the server.

## ProFTPD and WU-FTPD Server Tools

Both the WU-FTPD and ProFTPD daemons provide a set of FTP tools you can use to manage your FTP server. With the `ftpshut` command, you can smoothly shut down a running server, warning users of the shutdown well before it happens. `ftpwho` can tell you who is currently connected and what they are doing. `ftpcount` can give you the number of connections currently in effect. Although each daemon has its own set of tools, they perform the same action with much the same set of options. Tools provided by both ProFTPD and WU-FTPD have the same name and options, though ProFTPD provides more information on virtual hosts and has some added options.

### ftpshut

With the `ftpshut` command, you can have the FTP server shut down at a given time, rather than suddenly shutting it down by killing its process. This gives you the chance to warn users the server is shutting down and not to start any long downloads. `ftpshut` takes several options for specifying the time and including a warning message. `ftpshut` takes as its arguments the time until the shutdown, followed by the warning message you want sent to users. The time can be a word such as "now" that effects an immediate shutdown, a + sign with the number of minutes remaining, or a specific time of day indicated by an HHMM format, where HH is the hour in a 24-hour cycle and MM is the minute. The following example shuts down the FTP server in ten minutes, issuing a warning to users:

```
ftpshut +10 "Shutdown in ten minutes"
```

Shutdown disables any new FTP access ten minutes before a scheduled shutdown, though this can be changed using the `-l` option with the number of minutes you want. Five minutes before a scheduled shutdown, all current connections are disconnected. You can adjust the time with the `-q` option. The warning message is formatted at 75 characters, and you can use special formatting symbols for in-place substitutions of certain values in the warning message, such as the shutdown time. These symbols are called *magic cookies*. For example, `%s` is the shutdown time, `%r` is the time when new connections are refused, `%d` is the time when current connections are cut, `%M` is the maximum number of users, and `%l` is the local hostname.

### ftpwho and ftpcount

With the `ftpwho` command, you can find out who is currently connected to your FTP server. `ftpwho` shows the current process information for each user. The output displays five fields: the process ID, the tty connection, the status of the connection, the amount of CPU time used so far for the process, and the connection details. The status of the connection is R for running, S for sleeping, and Z for crashed. The connection details include the Internet address from where the connection is made, the user making the connection, and the task currently being performed, such as downloading a file. The field begins with the name of the FTP daemon, usually `ftpd`, followed by the different segments separated by colons.

The `ftpcount` command displays the number of users connected to your FTP server, broken down according to the classes specified in your `.ftpaccess` file. Along with the number of users, it shows the maximum number allowed to connect.

![](img/32a48d8db4c23e6e2eb70d1e5034c976_495_0.png)

## ABC Amber CHM Converter Trial version

Please register to remove this banner.

http://www.processestext.com/abcchm.html

## Chapter 22: Web Servers: Apache

### Overview

Linux distributions provide several Web servers for use on your system. The primary Web server is normally Apache, which has almost become the standard Web server for Red Hat Linux. It is a very powerful, stable, and fairly easy-to-configure system. Other Web servers are also available, such as Tux. Tux is smaller, but very fast, and is very efficient at handling Web data that does not change. Red Hat Linux provides default configurations for the Web servers, making them usable as soon as they are installed.

Other Web servers available for Linux include the Red Hat Secure Server (www.redhat.com), Apache-SSL ( www.apache-ssl.org), Stronghold Enterprise Server (www.redhat.com/software/stronghold), and Netscape Enterprise Server (home.netscape.com). Apache-SSL is an encrypting Web server based on Apache and OpenSSL (www.openssl.org). Stronghold is a commercial version of the Apache Web server featuring improved security and administration tools. You can also use the original NCSA Web server, though it is no longer supported (hoohoo.ncsa.uiuc.edu). AOLserver is America Online's Web server that is now available under the GPL license (www.aolserver.com).

Apache freely supports full secure shell encryption using OpenSSL. There are also private cryptographic products available only with licensing fees. Instead of obtaining the licensing directly, you can simply buy a commercial version of Apache that includes such licensing such as Stronghold and Raven ( www.covalent.net). Formerly, this kind of restriction applied to the use of RSA technology only in the United States, where it was once patented. The RSA patent has since expired and is now available for use in freely distributed products like OpenSSL.

![](img/32a48d8db4c23e6e2eb70d1e5034c976_496_0.png)
