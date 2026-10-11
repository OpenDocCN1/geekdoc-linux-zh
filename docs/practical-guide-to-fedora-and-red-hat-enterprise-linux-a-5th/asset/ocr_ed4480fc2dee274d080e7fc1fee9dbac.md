/usr/share/doc/vsftpd*/vsftpd.xinetd. Copy the sample file to the /etc/xinetd.d directory, rename it vsftpd, and edit the file to change the disable parameter to no. With the listen parameter in vsftpd.conf set to NO, xinetd will take care of starting vsftpd as needed.

Security The safest policy is not to allow users to authenticate against FTP: Use FTP for anonymous access only. If you do allow local users to authenticate and upload files to the server, be sure to put local users in a chroot jail (page 658). Because FTP sends usernames and passwords in cleartext, a malicious user can easily sniff (page 1107) them. With a username and password, the same user can impersonate a local user, upload a Trojan horse (page 1112), and compromise the system.

Firewall An FTP server normally uses TCP port 21. If the FTP server system is running a firewall, you need to open this port. Using the Firewall Configuration window Trusted Services tab (page 824), put a check in the box labeled FTP to open this port 631. For more general information see Chapter 25, which details iptables.

SELinux When SELinux is set to use a targeted policy, FTP is protected by SELinux. You can disable this protection if necessary. For more information refer to “Setting the Targeted Policy with system-config-selinux” on page 416.

# JUMPSTART: STARTING A vsftpd SERVER

By default, under Fedora/RHEL vsftpd allows anonymous users to log in on the server and does not set up a guest account. RHEL allows local users to log in. Fedora requires you to set local_enable (page 658) to YES to allow local users to log in. When someone logs in as an anonymous user, that person is working in the /var/ftp directory. You do not have to configure anything.

# TESTING THE SETUP

Make sure vsftpd is working by logging in from the system running the server. You can refer to the server as localhost or by using its hostname on the command line. Log in as anonymous; use any password.

```
$ ftp localhost
Trying ::1...
ftp: connect to address ::1:Connection refused
Trying 127.0.0.1...
Connected to localhost (127.0.0.1).
220 (vsFTPd 2.2.0)
Name (localhost:mark): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> quit
221 Goodbye.
```

If you are not able to connect to the server, first make sure the server is running:

```
$ /sbin/service vsftpd status
vsftpd (pid 3091) is running...
```