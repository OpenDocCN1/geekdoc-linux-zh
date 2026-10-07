
# Configuring the Wu-FTPd Server

The data transfer rate for anonymous client access is unlimited, but a maximum rate (in bytes per second) can be set using the anon_max_rate setting in vsftpd.conf. This can be useful for throttling bandwidth during periods of heavy access. Another default is that remote clients will be logged out after five minutes of idle activity or a stalled data transfer. You can set idle and transfer timeouts (connected connections) separately.

You can edit vsftpd.conf to enable, disable, and configure many features and settings of the vsftpd server, such as user access, filtering of bogus passwords, and access logging. Some features might require the creation and configuration of other files, such as

```
/etc/vsftpd.user_list—Used by the userlist_enable and/or the userlist_deny options; the file contains a list of users to be denied access to the server.
```

```
/etc/vsftpd.chroot_list—Used by the chroot_list_enable and/or chroot_local_user_options, this file contains a list of users who are either allowed or denied access to a home directory. An alternate file can be specified using the chroot_list_file option.
```

```
/etc/vsftpd.banned_emails—A list of anonymous password entries used to deny access if the deny_email_enable setting is enabled. An alternate file can be specified using banned_email option.
```

```
/var/log/vsftpd.log—Data transfer information is captured to this file if xferlog_enable setting is enabled.
```

A number of techniques, such as adjusting TCP buffers by bandwidth, have been researched in an effort to speed up transfers. Many factors can slow FTP performance. Disk I/O, system resources such as RAM, and network speeds are just some factors. Directories containing large numbers of files can cause bottlenecks. Even the underlying filesystem can slow transfers. Tuning your system's I/O, network interfaces, and use of TCP are only a few approaches for improving speeds. For additional ideas and a list of links to other tuning information, browse to http://linuxperf.org/

# Configuring Wu-FTP Server

Wu-FTP uses a number of configuration files to control how it operates, including the following:

- passwd—Contains the majority of server configuration settings
- conversions—Contains definitions of file conversions during transfers
- hosts—Settings to control access from specific hosts

# CHAPTER 18 File Transfer Protocol (FTP) Service

These files are installed in the /etc directory by the package. The following sections describe each of these files and how to use the commands to configure the FTP server.

> CAUTION When configuring anonymous FTP server, it is extremely important to ensure that all security precautions prevent malicious users from gaining privileged access to the server. Although this chapter shows you how to configure your server for secure use, all machines connected to the Internet are potential targets for attack. Vulnerable systems can be a source of liability if anyone accesses and uses them temporarily. Use Red Hat's configsecurity to implement firewall on your system.

> TIP Whenever editing server files, make a backup first. Also it is always a good idea to comment out (using pound sign at the beginning of a line) instead of deleting entries. This makes a neat trail of what was done, by whom, and why. If you have any problems with the configuration, these comments will help you troubleshoot and return to valid entries if necessary. You can use tools (such as cp) to extract a fresh copy of the configuration from the archive. Be aware, however, that the extracted version will overwrite your changes.

> NOTE Back up the server configuration files to another machine, should any working copies become corrupt. By making regular backups before changing a file you guarantee that the changes can be undone and server restored with minimal downtime.

# Using Commands in ftpaccess File to Configure Wu-FTPd

The ftpaccess file contains most of the server configuration details. Each line contains a definition or parameter that is passed to the server to specify how to operate. The directives can be broken down into the following categories:

- Access Control—Settings that determine who can access the FTP server and how it is accessed
- Information—Settings that determine what information is displayed to a user
- Logging—Settings that determine if logging is enabled and what information is logged
- Permission Control—Settings that control the behavior of users when accessing the server; in other words, what actions users are allowed to perform, such as create directory, upload a file, delete a file or directory, and so on

> TIP More options can be specified for the FTP server in the ftpaccess file. The most common commands have been covered here. A full list of configuration options can be found in the man page.

If you have installed the Desktop Environment, you can also use KDE's kwftpd client to graphically configure your-ftpd server's ftpaccess file. You can edit the ftpaccess file at the command line to make configuration changes in any of these categories. The following sections describe some changes

# Configure Access Control

Controlling which users can access the FTP server and how they can access it is a critical part of system security. Using the following entries in the ftpaccess file to specify which group the user accessing the server is assigned:

# Limit Access for Anonymous Users

This command imposes increased security on the anonymous user:

```
group <username> <class>
```
If the user is a member of a group, he will only be allowed access to files and directories owned by him or his group. The group must be a valid group from /etc/groups or /var/ftp/etc/groups.

# Define User Classes

This command defines a class of users by the address to which the user is connected.

```
class <class> <typelist> <addrglob> [<addrglob>]
```
There might be multiple members for a class of users, and multiple classes might apply to individual members. When multiple classes apply to one user, the first class that applies will be used.

![](img/446debe023486a07fde575245cf7a3ff_630_0.png)

The typelist field is a comma-separated list of the keywords anonymous, guest, real. anonymous applies to the anonymous user, and guest applies to the guest access account, as specified in the guest directory. real defines those users who have a valid entry in the /etc/passwd file.

The addrglob field is a regular expression that specifies addresses to which the class is applied. The (*) entry specifies all hosts.

# Block Access to the Server

Sometimes it is necessary to block access to the server to entire hosts. This can be useful in order to protect the system from individual hosts or entire blocks of IP addresses, or to force the use of other servers. Use this command to do:

```
deny <addrglob> <message_file>
```
deny will always deny access to hosts that match a given address. addr_glob is a regular expression field that contains a list of addresses, either numeric or a DNS name. This field can also be a file reference, which contains a listing of addresses. If the address is a file reference, it must be an absolute file reference; that is, starting with a /. To ensure that IP addresses can be mapped to a valid domain name, use the nameserver parameter.

A sample deny line looks as follows:
deny *.exodous.net /home/ftp/message_exodous_deny

This entry will deny access to the FTP server from all users who are coming from the comodous.net domain, and will display the message contained in the file .message_exodous_deny in the /home/ftp directory.

| ftusers File Purpose Now Implemented in ftpasswd |
| :--- |
| Certain accounts are created during the installation of Linux that are for the system segment and separate tasks with specific permissions. The ftusers file (located in /etc/ftusers) is where accounts for system purposes are listed. The version of wu-ftp comes with Red Hat Linux has deprecated the usage of this file, implementing the specific functionality of this file in the ftpasswdwd with the commands of deny-uid/deny-gid. |

# Restrict Permissions Based on Group IDs

The guestgroup line assigns a given groupname or usernames to behave exactly like the anonymous user. Here is the command:

```
guestgroup <username> [<username>
```
