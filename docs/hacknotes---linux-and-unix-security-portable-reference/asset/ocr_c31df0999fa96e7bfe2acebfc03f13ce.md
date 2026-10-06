# 134 Part II: Host Hardening

On hosts that have TCP Wrappers installed, edit /etc/hosts.allow and make sure the following line is the first uncommented statement:

```
ALL:deny
```

Also, make sure to deny connections from all hosts by default. This can be done by placing the following entry in /etc/hosts.deny:

```
all:all
```

Allow only trusted hosts to connect to services by placing appropriate entries in /etc/hosts.allow. See http://www.cert.org/security-improvement/implementations/i04i07.html for detailed instructions.

# HARDEN inetd AND xinetd CONFIGURATIONS

The Internet services daemon, inetd, is used to start daemons on all the required ports and starts the appropriate daemon process as soon as an incoming network connection arrives. Therefore, inetd is often called the "super-server". The xinetd daemon is similar to inetd, but it includes a bit more functionality, and xinetd users should strongly consider upgrading to xinetd.

# Disable Unnecessary Services

If using inetd, edit the /inetd.conf file and make sure unnecessary services are disabled. For example, consider the following line in inetd.conf that is responsible for the FTP daemon:

```
ftp stream tcp nowait root /usr/local/etc/tcp /usr/local/etc/ftpd
```

In order to disable FTP from inetd, place a # in front of the line:

```
#ftp stream tcp nowait root /usr/local/etc/tcp /usr/local/etc/ftpd
```

Restart inetd for changes to take effect:

```
killall -HUP inetd
```

If using xinetd, edit the appropriate service file in the xinetd.directory and ensure that the line "disable = yes" is present.

> Many services run independently of inetd and xinetd. Disable unnecessary services from starting up by editing or removing appropriate scripts in the /etc/rc.d/directory.