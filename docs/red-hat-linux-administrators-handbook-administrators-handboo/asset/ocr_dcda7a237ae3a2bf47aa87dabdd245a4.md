# Restricting host access via the TCP wrapper

As mentioned before, the TCP wrapper provides a great deal of flexibility in controlling access at an Internet host (or IP address) level. This flexibility can come in very handy for configuring a tight server system. This section discusses an example of a tightly controlled system that is based on a system I use on a daily basis.

First, decide on the goal of the example control configuration. Suppose that you want to create an Internet Web server system that allows only Telnet, FTP, POP3, and HTTP services. Because the Web service (HTTP) is typically a high-demand service, it is not run via inetd. Assume that the Web server is Apache and it is run as a standalone service. Thus, inetd will manage the rest of the service. Also, assume that you want to restrict Telnet, FTP, and POP3 access to only a single network whose network address is 206.171.50.0.

Listing 15-3 shows the /etc/inetd.conf file required for this example.

# Listing 15-3 The /etc/inetd.conf File

```
ftp stream tcp nowait root /usr/sbin/tcpd in.ftpd
-l -a
telnet stream tcp nowait root /usr/sbin/tcpd in.telnetd
in.telnetd
pop-3 stream tcp nowait root /usr/sbin/tcpd in.pop3d
```

As you can see, all three services are wrapped with the tcpd wrapper. Now, you need to restrict access to these services via the /etc/hosts.allow and /etc/hosts.deny files. The /etc/hosts.allow file is used to specify which hosts are allowed access to inetd services, and the /etc/hosts.deny file is used to specify which hosts are not allowed access to inetd services. Both of these files use the same configuration format, shown here:

```
daemon list : client list [ : shell command ]
```

The daemon list is a list of one or more service process names. For instance, in.ftpd, in.telnetd, and in.pop3d are daemon names for this example. The client list consists of one or more host names or IP addresses. You can use the wildcards shown in Table 15-6 in both daemon and client lists.