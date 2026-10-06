# 464 Linux Administration: A Beginner's Guide

| Type of Option | Description | Example |
| :--- | :--- | :--- |
| Daemon | These options control the general behavior of the vsftpd daemon. | listen | listen_ipv6 When enabled, vsftpd will run in standalone mode instead of running under a superdaemon such as xinetd or inetd. vsftpd itself will take care of listening for handling incoming connections. Default value is NO. |
| Socket | These are the networking and port-related options. | listen_address Specifies the IP address on which vsftpd listens for network connections. option has no default value. anon_max_rate Maximum data transfer rate permitted, in bytes per second, for anonymous clients. The default value is 0. listen_port The port that vsftpd will listen on for incoming FTP connections. The default value is 21. pasv_enable Enables or disables PASV method of obtaining a data connection. The default value is YES. port_enable Enables or disables the PORT method of obtaining a data connection. The default value is YES. |
| Security | These options directly control the granting or denial of access to the server—the options offer a built-in access-control mechanism to the FTP server. | anonymous_enable Controls whether anonymous logins are permitted. If enabled, both the usernames ftp and anonymous recognized as anonymous logins. The default value is YES. |

Table 17-2 Configuration Options for vsftpd