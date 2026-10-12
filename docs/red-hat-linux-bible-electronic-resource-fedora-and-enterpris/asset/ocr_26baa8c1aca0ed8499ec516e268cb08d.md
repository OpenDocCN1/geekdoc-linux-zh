```
# /etc/init.d/xinetd restart
```

In this case, you could look in the /etc/services file and see that POP3 services are (by default) received on port number 110 for TCP/IP networks. So, any request that comes into your computer for port 110 is first directed to the xinetd daemon, then handled by the ipop3d daemon. If authentication is correct, e-mail is downloaded to the user’s mailbox (typically /var/spool/mail/user, where user represents the user’s name).

> **CROSS-REFERENCE:** The xinetd super-server is described in Chapter 12.

# The init.d start-up scripts

Network services that are not available via the xinetd daemon are typically handled by scripts in the /etc/init.d directory. For a script in the /etc/init.d directory to activate a service, it must be linked to a file in one of the run-level directories (/etc/rc?.d) that begins with the letter “S” followed by a two-digit number.

For example, the script for starting the print service daemon (/etc/init.d/lpd) is linked to the file S60lpd in the /etc/rc2.d, /etc/rc3.d, /etc/rc4.d, and /etc/rc5.d directories. In that way, the print service is started when Red Hat Linux is running in initialization states 2, 3, 4, or 5.

> **CROSS-REFERENCE:** See Chapter 12 for more details on run levels and start-up scripts.

For the most part, system administrators are not expected to modify these start-up scripts. However, to have a service turned on or off for a particular run level, change the script to a filename that begins with an S (start) to one that begins with a K (kill). You can easily do this with the chkconfig command or the Service Configuration window. To start that window, type serviceconf from a Terminal window while you are logged in as the root user.

Start-up scripts typically start one or more daemon processes that represent a particular service. To add options to a particular daemon, you typically don’t have to edit the start-up script directly. Instead, look for configuration files in the /etc/sysconfig directory. For example, daemons options representing the DNS (named), Samba (smbd and nmbd), and system logging (syslogd) services have options files in the /etc/sysconfig directory.

# Choosing Alternatives

Some services in Red Hat Linux can be implemented by several different software packages. Although you can, you probably don’t want to run multiple mail and print servers on the same computer. At the very least, you should set the software you want to use by default.

In Red Hat Linux, an “alternatives” feature is packaged into the operating system. Alternatives is an implementation of the Debian GNU/Linux alternatives feature. In essence, alternatives