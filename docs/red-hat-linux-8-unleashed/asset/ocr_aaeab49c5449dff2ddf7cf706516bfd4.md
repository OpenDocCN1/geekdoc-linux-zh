# Configuring the Very Secure FTP Server

```
socket_type = stream
wait = no
user = root
server = /usr/sbin/vsftpd
nice = 10
}
```

Restart the xinetd daemon to start the service. You can now run wu-ftpd and vsftpd at the same time. If you enable one FTP server and restart xinetd, the other server will be stopped.

> TIP
You can use xinetd's server_args keyword, along with appropriate options, to pass command line arguments to wu-ftpd or vsftpd servers. One handy use is to test different configuration files. For example, vsftpd's default configuration file is /etc/vsftpd.conf, but you can specify a different file with an entry in /etc/xinetd.d/vsftpd like this:

```
server_args = /etc/vsftpd.custom
```

# Configuring the Very Secure FTP Server

The vsftpd server, although not as popular as Wu-FTPD, is used by Red Hat, Inc. for its FTP server operations (the vsftpd server home page is located at http://vsftpd.beasts.org/). The server offers features such as simplicity, security, and speed. It is used by many of sites, such as ftp.debian.org, ftp.gnu.org, rpmfind.net, and ftp.gimp.org. Despite its name, the server does not enable use of encrypted usernames or passwords.

Its main configuration file is vsftpd.conf and resides under the /etc directory. The server has a number of features and default policies, but these can be overridden by changing the installed configuration file.

By default, anonymous logins are enabled, but users are not allowed to upload files, create new directories, or delete or rename files. The configuration file installed by Red Linux allows local users (that is, users with a login and shell account) to log in and access their home directory. This configuration presents potential security risks because usernames and passwords are passed without encryption over a network. The best policy is to deny your users access to the server from their user accounts. The standard vsftpd configuration disables this.

The contents of a file named .message (if it exists in the current directory) are displayed when a user enters the directory. This feature is enabled in the installed configuration file, but disabled by the daemon. FTP users are also not allowed to perform recursive directory listings, which can help reduce bandwidth use.