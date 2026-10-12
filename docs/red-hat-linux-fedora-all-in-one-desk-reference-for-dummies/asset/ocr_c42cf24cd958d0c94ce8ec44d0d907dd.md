root and place the DVD in the DVD drive. If you're using the GNOME or KDE desktop, the DVD should mount automatically. If not, type the following command to mount the DVD:

```
mount /mnt/cdrom
```

Then type the following command to change the directory:

```
cd /mnt/cdrom/RedHat/RPMS
```

This is where you find the RPM files for FTP. You can install both the FTP server and the anonymous FTP package with the following RPM commands:

```
rpm -ivh vsftpd*
```

```
rpm -ivh anonftp*
```

# Configuring the FTP Server

Red Hat Linux comes with the very secure FTP daemon (vsftpd), written by Chris Evans. The executable file for vsftpd is /usr/sbin/vsftpd, and it uses a number of configuration files in the /etc and /etc/vsftpd directories. By default, the vsftpd server is disabled; if you want to use the FTP server, first you have to enable it. In this section, I show you how.

In previous versions of Red Hat Linux, the vsftpd server was set up to run under xinetd — the Internet super server. This required editing a configuration file in /etc/xinetd.d directory to enable the vsftpd server. However, starting in Red Hat Linux 8.1, the vsftpd server is configured to run standalone, and there is an initialization script (or init script) — /etc/init.d/vsftpd — to start and stop the server. To start the vsftpd server, log in as root and type the following command:

```
service vsftpd start
```

You can also type the following command as root to turn on vsftpd so that it starts at system startup:

```
chkconfig --level 35 vsftpd on
```

After you start the vsftpd server, the default settings should be all you need to begin using the server. That's because other FTP clients can now connect and request files from your FTP server. However, you should learn about the configuration files in case you have to customize them some other time.