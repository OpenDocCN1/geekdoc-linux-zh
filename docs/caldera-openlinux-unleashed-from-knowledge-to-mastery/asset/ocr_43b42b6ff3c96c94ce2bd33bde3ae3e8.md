# Putting SOCKS to Work

SOCKS is an umbrella proxy server that conducts transactions in HTTP, FTP, and other protocols, all under one roof. This is in contrast to TIS, for example, which breaks the protocols up into discrete areas of responsibility, so that it is necessary to configure a proxy service for the World Wide Web, FTP, the ARPA/Berkeley “r-” commands (rlogin, rsh, rcp), and other protocols. SOCKS is very easy to set up; there are really only two configuration files to be concerned with after installation. The first is the file sockd.conf, which is the “butter at the door” for Internet access.

The sockd.conf file contains pass and block lines, each to be customized according to IP address ranges. To bar an IP range from access, the deny line would contain that number range. Similarly, allowing only a certain range of IP addresses is also possible. An additional number can be applied exactly like a netmask to further tune the permit and deny IP ranges.

We will look at the Dante SOCKS package, which is freely available Open Source software and is extremely simple to get running. For the RPM version, simply log in as root and type

```
```
# rpm -ta dante-VERSION.tar.gz
```
```

Compiling the old-fashioned way is nearly as simple, because it uses autoconfig. Simply untar the package and type

```
```
# ./configure
# make
# make install
```
```

The file /etc/sockd.conf (in the Dante implementation; it is called socksd.conf in the NEC version) configures how the SOCKS server itself runs, who it allows in, and where they can go. An annotated example of a working Dante sockd.conf file is shown below. You should note that this is a simple example that will get you a working sockd. It does not use some of the advanced features of SOCKS, such as authentication. You will want to refer to your documentation and man pages for more advanced configurations.

```
```
# /etc/sockd.conf - Example configuration file for the Dante SOCKS server.

# Log information via syslog
logoutput: syslog
# It can also log to stderr, stdout, or a file (as shown here)
#logoutput: /var/log/sockd.log

# The server can be made to bind to only one address and port - very
# useful in a multihomed (multiple network interfaces) setup.
internal: 192.168.7.1 port = 1080
```
```