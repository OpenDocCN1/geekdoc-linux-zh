The data transfer rate for anonymous client access is unlimited, but you can set a maximum rate (in bytes per second) by using the anon_max_rate setting in vsftpd.conf. This can be useful for throttling bandwidth use during periods of heavy access. Another default is that remote clients are logged out after five minutes of idle activity or a stalled data transfer. You can set idle and transfer timeouts (stalled connections) separately.

Other settings that might be important for managing your system's resources (networking bandwidth or memory) when offering FTP access include the following:

+   dirlist_enable—Toggles directory listings on or off.
+   dirmessage_enable—Toggles display of a message when the user enters a directory. A related setting is ls_recurse_enable, which can be used to disallow recursive directory listings.
+   download_enable—Toggles downloading on or off.
+   max_clients—Sets a limit on the maximum number of connections.
+   max_per_ip—Sets a limit on the number of connections from the same IP address.

# ## Configuring the wu-ftpd Server

wu-ftp uses a number of configuration files to control how it operates, including the following:

+   ftpaccess—Contains the majority of server configuration settings
+   ftconversions—Contains definitions of file conversions during transfers
+   ftphosts—Holds settings to control user access from specific hosts

These files may be created in the /etc directory during RPM installation, or may be created by a system administrator. The following sections describe each of these files and how to use the commands they contain to configure the wu-ftpd server so that it is accessible to all incoming requests.

> **CAUTION**
> When configuring an anonymous FTP server, it is extremely important to ensure that all security precautions are taken to prevent malicious users from gaining privileged-level access to the server. Although this chapter shows you how to configure your FTP server for secure use, all machines connected to the Internet are potential targets for malicious attacks. Vulnerable systems can be a source of potential liability, especially if anyone accesses and uses them to store illegal copies of proprietary software—even temporarily. There is little value in configuring a secure FTP server if the rest of the system is still vulnerable to attack. Use Red Hat's *lokkit* or *system-config-securitylevel* client to implement a firewall on your system.