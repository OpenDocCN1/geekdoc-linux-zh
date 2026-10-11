```
postrotate
   /usr/sbin/accton /var/account/pacct
endscript
}

[root@server1 root]# _
```

The file just shown indicates that the `/var/account/pacct` file should be rotated daily, new log files are owned by root and have the permissions 600 (rw-------), and log files are only rotated if they are not empty. Log files are compressed after being rotated and up to 31 copies of old log files can exist. In addition, the `/usr/sbin/accton` program is run before each rotation and the `/usr/sbin/accton /var/account/pacct` program is run after each rotation.

On most Linux systems, the `logrotate` utility is automatically scheduled to run daily via the file `/etc/cron.daily/logrotate`; however, you might choose to run it manually by typing the command `logrotate /etc/logrotate.conf` at a command prompt.

Over time, the `logrotate` command generates several copies of each log file, as shown in the following listing of the `/var/log` directory:

```
[root@server1 log]# ls /var/log
acpid
httpd
ppsql
secure
amanda
iptraf
ppp
secure.1
boot.log
lastlog
prelink.log
secure.2
boot.log.1
mail
privoxy
spooler
boot.log.2
maillog
quagga
spooler.1
boot.log.3
maillog.1
radius
spooler.2
canna
maillog.2
routed
squid
cron
man
rpmkgs
tomcat
cron.1
messages
rpmkgs.1
ucwp
cups
messages.1
rpmkgs.2
wbox
dmesg
messages.2
rpmkgs.3
wtwp
exim
mysqld.log
sa
Xorg.0.log
fax
mysqld.log.1
samba
Xorg.0.log.old
gdm
news
scrollkeeper.log
Xorg.setup.log
[root@server1 root]# _
```

Given the preceding output, the most recent events are recorded in the `boot.log` file, followed by the `boot.log.1` file, followed by the `boot.log.2` file, and so on.

# Administering Users and Groups

You must log in to a Linux system with a valid user name and password before a BASH shell is granted. This process is called **authentication** because the user name and password are authenticated against a system database that contains all **user account** information. Authenti-