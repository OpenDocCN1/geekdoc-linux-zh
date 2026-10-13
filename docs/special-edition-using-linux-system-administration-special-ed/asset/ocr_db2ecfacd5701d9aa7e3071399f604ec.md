+   - Unlike most FTP servers, for better security, it does not support any SITE EXEC commands. In addition it does not use any external programs, which are also a major source of security problems in most FTP daemons.
+   - It runs as a configurable, non-privileged user, and thereby offers a higher level of security.
+   - It supports hidden directories and files.
+   - It provides logs that are compatible with the WU-FTPd logs. More extended logging is possible.
+   - It supports shadow passwords.

# INSTALLING A PRECOMPILED BINARY

Precompiled binary distributions of ProFTPD for Linux are available from ftp://ftp.proftpd.net/pub/proftpd. The latest version at the time of this writing is proftpd-1.2.0pre10. Note these are development releases; a stable version is yet to be released.

To install the standalone version on an Intel architecture machine with support for Red Hat package files, download proftpd-core-1.2.0pre10-1.i686.rpm and proftpd-standalone-1.2.0pre10-1.i686.rpm, and run the following commands:

```
```bash
# rpm -i proftpd-core-1.2.0pre10-1.i686.rpm
# rpm -i proftpd-standalone-1.2.0pre10-1.i686.rpm
```
```

To install the inetd version instead, download proftpd-core-1.2.0pre10-1.i686.rpm and proftpd-inetd-1.2.0pre10-1.i686.rpm, and run the following commands:

```
```bash
# rpm -i proftpd-core-1.2.0pre10-1.i686.rpm
# rpm --install proftpd-inetd-1.2.0pre10-1.i686.rpm
```
```

The ProFTPD RPM packages install the following files:

+   - `/usr/sbin/proftpd`
+   - `/usr/sbin/ftpshut`
+   - `/usr/bin/ftpwho`
+   - `/usr/bin/ftpcount`
+   - A symbolic link `/usr/sbin/in.proftpd` pointing to `/usr/sbin/proftpd`

In addition a default configuration file proftpd.conf is placed in /etc directory.

The RPM installation for the inetd version of ProFTPD edits the /etc/inetd.conf file, and signals inetd with a SIGHUP signal. It adds an entry to start proftpd when a connection attempt to port 21 is detected.

The RPM installation for the standalone version of ProFTPD also edits the /etc/inetd.conf file to remove any invocation of the FTP daemon, and sends a SIGHUP signal to inetd. In addition, it places a startup script called proftpd in the /etc/rc.d/init.d directory. After the