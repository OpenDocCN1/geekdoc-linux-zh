If you're running xinetd, edit the existing /etc/xinetd.d/swat file to enable the entry. Listing 8.1 shows a sample /etc/xinetd.d/swat file.

# **Listing 8.1 Sample /etc/xinetd.d/swat file**

```
# default: off
# description: SWAT is the Samba Web Admin Tool. Use swat \
#			to configure your Samba server. To use SWAT, \
#			connect to port 901 with your favorite web browser.

service swat
{
port	= 901
socket_type = stream
wait = no
only_from = 10.0.0.100
user = root
server = /usr/sbin/swat
log_on_failure  += USERID
disable = no
}
```

Note in Listing 8.1 that I have included the directive only_from to restrict connections to SWAT to my workstation (10.0.0.100). This is a very important security feature because you typically don't want people connecting to SWAT from just any host on your network, or on the Internet! If you're using inetd, make sure that only host 10.0.0.100 is able to connect to port 901 by adding the following line to /etc/hosts.allow:

```
swat: 10.0.0.100
```

In addition, add the following line to /etc/hosts.deny:

```
swat: ALL
```

> WARNING In order to avoid exposure of the root password, restrict access to the SWAT server to the Linux server itself (ideally), or at least to hosts that are on a protected segment that includes the server. If you must access the SWAT service remotely, follow the SSL instructions described in the following section.

# **SWAT-SSL**

Chapter 7, “HTTP Services,” described the use of the Secure Sockets Layer implementation for Linux (OpenSSL) and its ability to protect the communication between Web clients and Apache HTTP servers. Like Apache, SWAT is an HTTP server, and as such, it can be integrated with OpenSSL to ensure the privacy of your Samba administration commands.

+   Application Security
+   PART 3