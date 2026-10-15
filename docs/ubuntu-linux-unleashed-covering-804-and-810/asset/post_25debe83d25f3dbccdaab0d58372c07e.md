
passive mode, the remote server tries to form a connection to your local host and gets blocked. For example, here is a connection to an FTP server (running ProFTPD), an attempt to view a directory listing, and the resulting need to use ftp's internal passive command:

```
$ ftp ftp.tux.org
Connected to gwny.tux.org.
220 ProFTPD 1.2.5rc1 Server (ProFTPD on ftp.tux.org) [gwny.tux.org]
500 AUTH not understood.
KERBEROS_V4 rejected as an authentication type
Name (ftp.tux.org:gbush): gbush
331 Password required for gbush.
Password:
230 User gbush logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> cd public_html
250 CWD command successful.
ftp> ls
500 Illegal PORT command.
ftp: bind: Address already in use
ftp> pass
Passive mode on.
ftp> ls
227 Entering Passive Mode (204,86,112,12,187,89).
150 Opening ASCII mode data connection for file list
-rw-r--r-- 1 gbush gbush 8470 Jan 10 2000 LinuxUnleashed.gif
-rw-r--r-- 1 gbush gbush 4407 Oct 4 2001 RHU72ed.gif
-rw-r--r-- 1 gbush gbush 6732 May 18 2000 SuSEUnleashed.jpg
-rw-r--r-- 1 gbush gbush 6175 Jan 10 2000 TYSUSE.gif
-rw-r--r-- 1 gbush gbush 3135 Jan 10 2000 TZones.gif
...
```

> **NOTE**
> 
> Browse to http://slacksite.com/other/ftp.html for a detailed discussion regarding active and passive FTP modes and the effect of firewall blocking of service ports on FTP server and client connections.

Other default settings that are specific user login controls are not set, but you can configure the controls to deny access to one or more users.

The data transfer rate for anonymous client access is unlimited, but you can set a maximum rate (in bytes per second) by using the anon_max_rate setting in vsftpd.conf.

This can be useful for throttling bandwidth use during periods of heavy access. Another default is that remote clients will be logged out after five minutes of idle activity or a stalled data transfer. You can set idle and transfer timeouts (stalled connections) separately.

Other settings that might be important for managing your system's resources (networking bandwidth or memory) when offering FTP access include the following:

- dirlist_enable—Toggles directory listings on or off.
- dirmessage_enable—Toggles display of a message when the user enters a directory. A related setting is ls_recurse_enable, which can be used to disallow recursive directory listings.
- download_enable—Toggles downloading on or off.
- max_clients—Sets a limit on the maximum number of connections.
- max_per_ip—Sets a limit on the number of connections from the same IP address.

## Configuring the Server

Wu-FTP uses a number of configuration files to control how it operates, including the following:

- ftpassess—Contains the majority of server configuration settings
- ftpconversions—Contains definitions of file conversions during transfers
- ftphosts—Settings to control user access from specific hosts

These files may be created in the /etc directory during installation, or may be created by a system administrator. The following sections describe each of these files and how to use the commands they contain to configure the Wu-FTP server so that it is accessible to all incoming requests.

> CAUTION
> When configuring an anonymous FTP server, it is extremely important to ensure that all security precautions are taken to prevent malicious users from gaining privileged-level access to the server. Although this chapter shows you how to configure your FTP server for secure use, all machines connected to the Internet are potential targets for malicious attacks. Vulnerable systems can be a source of potential liability, especially if anyone accesses and uses them to store illegal copies of proprietary software—even temporarily.

## Using Commands in the ftpaccess File to Configure wu-ftpd

The ftpaccess file contains most of the server configuration details. Each line contains a definition or parameter that is passed to the server to specify how the server is to operate. The directives can be broken down into the following categories, including:
