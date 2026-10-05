# 708 CHAPTER 19 FTP: TRANSFERRING FILES ACROSS A NETWORK

ls_recurse_enable YES permits users to give ls -R commands. Setting this parameter to YES may pose a security risk giving an -R command at the top of a large directory hierarchy can consume a lot of system resources.

Default: NO

# LOGS

By default, logging is turned off. However, the vsftpd.conf file distributed with Ubuntu Linux turns it on. This section describes parameters that control the details and locations of logs.

log_ftp_protocol YES logs FTP requests and responses, provided that xferlog_std_format is set to NO.

Default: NO

xferlog_enable YES maintains a transfer log in /var/log/vsftpd.log (or another file specified by xferlog_file). NO does not create a log.

Default: NO

Ubuntu: YES

xferlog_std_format YES causes a transfer log (not covering connections) to be written in standard xferlog_format, as used by wu-vsftpd, as xferlog_file is explicitly set. If xferlog_std_format is set to YES and xferlog_file is not explicitly set, logging is turned off. The default vsftpd log format is more readable than xferlog format, but it cannot be processed by programs that generate statistical summaries of xferlog files. Search for xferlog on the Internet to obtain more information on this command.

Default: NO

xferlog_file See xferlog_enable and xferlog_std_format.

Default: /var/log/vsftpd.log

# CONNECTION PARAMETERS

You can allow clients to establish passive and/or active connections (page 689). Setting timeouts and maximum transfer rates can improve security and performance. This section describes parameters that control the types of connections a client can establish, the length of time vsftpd wait while establishing a connection, and the speeds of connections for different types of users.

# PASSIVE (PASV) CONNECTIONS

pasv_enable NO prevents the use of PASV connections.

Default: YES

pasv_promiscuous NO causes PASV to perform a security check that ensures that the data and control connections originate from a single IP address. YES disables this check; it is not recommended for a secure system.

Default: NO