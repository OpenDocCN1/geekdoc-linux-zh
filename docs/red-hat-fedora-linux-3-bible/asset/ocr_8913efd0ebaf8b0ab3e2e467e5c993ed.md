Then you could restart the `xinetd` daemon (without turning off the daemon itself):

```
```
# service xinetd restart
```
```

> **NOTE:** Although not all services support this, the `xinetd` services lets you use the `reload` instead of the `restart` option with the `service` command just shown. With `xinetd` already running, a reload can occur faster and with less interruption to system services by not completely shutting down `xinetd`.

In this case, you could look in the `/etc/services` file and see that tftp services are (by default) received on port number 69 for TCP/IP and UDP networks. So, any request that comes into your computer for port 69 is first directed to the `xinetd` daemon, then handled by the `tftpd` daemon. If authentication is correct, the requested file transfer can take place.

> **CROSS-REFERENCE:** The `xinetd` super-server is described in Chapter 12.

# The init.d start-up scripts

Network services that are not available via the `xinetd` daemon are typically handled by scripts in the `/etc/init.d` directory. For a script in the `/etc/init.d` directory to activate a service, it must be linked to a file in one of the run-level directories (`/etc/rc?.d`) that begins with the letter `S` followed by a two-digit number.

For example, the script for starting the print service daemon (`/etc/init.d/cups`) is linked to the file `S55cups` in the `/etc/rc2.d, /etc/rc3.d, /etc/rc4.d,` and `/etc/rc5.d` directories. In that way, the print service is started when Fedora Linux is running in initialization states 2, 3, 4, or 5.

> **CROSS-REFERENCE:** See Chapter 12 for more details on run levels and start-up scripts.

For the most part, system administrators are not expected to modify these start-up scripts. However, to have a service turned on or off for a particular run level, change the script to a filename that begins with an `S` (start) to one that begins with a `K` (kill). You can easily do this with the `chkconfig` command or the Service Configuration window. To start that window, type `serviceconf` from a Terminal window while you are logged in as the root user.

Start-up scripts typically start one or more daemon processes that represent a particular service. To add options to a particular service, you typically don't have to edit the start-up script directly. Instead, look for configuration files in the `/etc/sysconfig` directory. For example, daemons options representing the DNS (named), Samba (smbd and nmbd), and system logging (syslogd) services have options files in the `/etc/sysconfig` directory.