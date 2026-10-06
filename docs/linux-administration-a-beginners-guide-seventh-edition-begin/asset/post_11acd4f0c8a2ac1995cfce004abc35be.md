
# CHAPTER 17 File Transfer Protocol (FTP)

| File | Description |
| --- | --- |
| /usr/sbin/vsftpd | This is the main vsftpd executable. It is the daemon itself. |
| /etc/vsftpd/vsftpd.conf | This is the main configuration file for the vsftpd daemon. It contains the main directives that control the behavior of the FTP server. |
| /etc/vsftpd/ftpususers | Text file that stores the list of users not allowed to log into the FTP server. This file is referenced by the Pluggable Authentication Module (PAM) system. |
| /etc/vsftpd/user_list | Text file used either to allow or deny access to users. Access is denied or allowed according to the value of the userlist_deny directive in the vsftpd.conf file. |
| /var/ftp | This is the FTP server's working directory. |
| /var/ftp/pub | This serves as the directory that holds files meant for anonymous access to the FTP server. |

Table 17-1 vsftpd Configuration Files and Directories

> CAUTION The options and values in vsftpd.conf have very finicky syntax! No space(s) should appear between the option directive, the equal sign (=), and the value. Having any spaces therein can prevent the vsftpd FTP daemon from starting up!

As with other Linux/Unix configuration files, comments in the file are denoted by lines that begin with the pound sign (#). To see the meaning of each of the directives, you should consult the vsftpd.conf man page, using the man command like so:

```
[root@server ~]# man vsftpd.conf
```

> NOTE vsftpd configuration files are located directly under the /etc directory on Debian-like systems. For example, the equivalent of /etc/vsftpd/ftpususers is located at /etc/ftpusers in Ubuntu.

The options (or directives) in the /etc/vsftpd/vsftpd.conf file can be categorized according to the role they play. Some of these categories are discussed in Table 17-2.

# 464 Linux Administration: A Beginner's Guide

| Type of Option | Description | Example |
| :--- | :--- | :--- |
| Daemon | These options control the general behavior of the vsftpd daemon. | listen | listen_ipv6 When enabled, vsftpd will run in standalone mode instead of running under a superdaemon such as xinetd or inetd. vsftpd itself will take care of listening for handling incoming connections. Default value is NO. |
| Socket | These are the networking and port-related options. | listen_address Specifies the IP address on which vsftpd listens for network connections. option has no default value. anon_max_rate Maximum data transfer rate permitted, in bytes per second, for anonymous clients. The default value is 0. listen_port The port that vsftpd will listen on for incoming FTP connections. The default value is 21. pasv_enable Enables or disables PASV method of obtaining a data connection. The default value is YES. port_enable Enables or disables the PORT method of obtaining a data connection. The default value is YES. |
| Security | These options directly control the granting or denial of access to the server—the options offer a built-in access-control mechanism to the FTP server. | anonymous_enable Controls whether anonymous logins are permitted. If enabled, both the usernames ftp and anonymous recognized as anonymous logins. The default value is YES. |

Table 17-2 Configuration Options for vsftpd

# CHAPTER 17 File Transfer Protocol (FTP) 465

# Type of Option Description Example

Security tcp Assuming vsftpd was compiled with tcp_wrappers support, incoming connections will be fed through tcp-wrappers access control. The default value is NO.

local_enable Controls whether local logins are permitted. If enabled, normal user accounts in /etc/passwd can be used to log in. The default value is NO.

userlist_enable Loads a list of usernames from the filename userlist_file directive when this option is enabled. If a user tries to log using a name in this file, that user will be denied access before even prompted for a password. The default value is NO.

userlist_deny Examined if the userlist_enable option is active. When its value is set to NO, users will be denied login unless they are explicitly listed in the file specified by userlist_file. When login is denied, the denial is issued before the user is asked for a password; this prevents users from sending cleartext across the network. The default value is YES.

userlist_file This option specifies the name of the file to be loaded when the userlist_enable option is active. Depending on the distro, the default value is either vsftpd.user_list or user_list.

# Table 17-2 Configuration Options for vsftpd (Continued)

# 466 Linux Administration: A Beginner's Guide

| Type of Option | Description | Example |
| :--- | :--- | :--- |
| Security (continued) | | cmds_allowed Specifies a list of allowed FTP commands. However, the post-login commands are always allowed--USER, PASS |
| File-transfer | These options relate to file transfers to from the server. | This has no default value. download_enable If set to NO, permission will be denied. The default value is YES. write_enable This option controls whether any commands change the system. These commands are DELE, RETTR, MKD, SITE. The default value is NO. chown_uploads This option has the effect of changing the ownership of anonymously files. chown_username Specifies the name of the user who is given of uploaded files. The default value is root. |
| Directory | These options control the behavior of directories served by the FTP. | use_localtime When enabled, vsftpd will display the time in local zone. The default value is NO. |
| Logging | These options control how and where vsftpd logs. | vsftpd_log_file Specifies the main log file. The default value is /var/log/vsftpd.log. xferlog_enable If enabled, any log that would have gone to /var/log/vsftpd instead. syslog_enable Logging is done under the File Transfer Daemon (FTP) facility. The default value is NO. |

# Table 17-2 Configuration Options for vsftpd (Continued)

# CHAPTER 17 File Transfer Protocol (FTP)

| Type of Option | Description | Example |
| --- | --- | --- |
| Directory (continued) | | dirlist_enable Enables disables the ability to perform directory listings. If set to NO, a permission-denied error will be given. The default value is YES. |

> NOTE The possible values of the options in the file can be divided into three categories: the Boolean options (such as YES, NO), the Numeric options (such as 007, 700), and the String options (such as root, /etc/vsftpd.chroot_list, and so on).

## Starting and Testing the FTP Server

Because it comes with some default settings that allow it to hit the ground running, the vsftpd daemon is pretty ready to run out of the box.

Of course, we'll need to start the service. Once you've learned how to start the daemon, the rest of this section will walk you through testing the FTP server by connecting to it. But first we'll start the FTP service.

> TIP The ftp daemon is automatically started after installing the software via apt-get. Check to make sure it's already running before trying to start it again. You can examine the output of the command ps -aux | grep vsftd to check this.

1. Start the FTP service:
`root@server -]# service vsftd`

On Linux distributions systemd, you can alternatively start the vsftpd daemon using the systemctl command:
`root@fedora-server -]# systemctl start vsftpd.service`

> TIP If the service command is not available on your Linux distribution, you might be able to restart the service by directly executing its run control script. For example, you may be able to restart vsftpd by issuing the following command:
`root@server -]# /etc/init.d/vsftd start`

2. Launch the command-line FTP client program, and connect to the local FTP server as an anonymous user:
`root@server -]# ftp localhost`
Connected to localhost (127.0.0.1).
220 (vsFTPd 3.**)
Name (localhost:root):

3. Enter the name of the anonymous user when prompted—that is, type ftp:
Name (localhost:root): ftp
331 Please specify the password.

> TIP Most FTP servers that allow anonymous logins often permit the implicit use of the username "anonymous." Instead of supplying ftp as the username to use to connect anonymously to our sample Fedora FTP server, we can instead use the popular username anonymous.
