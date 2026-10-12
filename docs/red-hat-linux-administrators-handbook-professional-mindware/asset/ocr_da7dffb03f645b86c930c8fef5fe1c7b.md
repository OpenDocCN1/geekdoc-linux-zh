```
wait                = no
user                = root
server              = /usr/sbin/tcpd
server_args         = /usr/sbin/in.ftpd
log_on_success      += DURATION USERID
log_on_failure      += USERID
nice                = 10
}
```

The TCP wrapper program enhances security by providing the following services:

+   •  **Logging service** can log information about a request using the syslog facility.
+   •  **Host-based access control** can provide host-based access control using pattern matching.
+   •  **Host name and address verification service** can detect spoofing of host names or addresses when a host is pretending to be some other host.

You can guess how important the TCP wrapper is, as it comes as part of the default Red Hat Linux installation. There is absolutely no reason for not wrapping each of your xinetd services with the TCP wrapper.

# **Restricting host access via the TCP wrapper**

The TCP wrapper provides a great deal of flexibility in controlling access at an Internet host (or IP address) level. This flexibility can come in very handy for configuring a tight server system. Here I discuss an example of a tightly controlled system based on a system I use daily.

First, decide on the goal of the sample control configuration. Say that you want to create an Internet Web server system that allows only Telnet, FTP, POP3, and HTTP services. Because the Web service (HTTP) is typically a high-demand service, it is not run via xinetd. Let's assume that the Web server is Apache and it is run as a stand-alone service. In this example, then, xinetd manages the rest of the service. Also, let's assume that we want to restrict Telnet, FTP, and POP3 access to only a single network whose network address is 206.171.50.0.

Listing 15-3 shows the flags, server, and server argument lines for each of these services.