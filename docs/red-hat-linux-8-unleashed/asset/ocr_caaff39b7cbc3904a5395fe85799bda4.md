# Ports

Most servers on your network have more than one task. For example, Web servers have to serve both standard and secure pages. You might also be running an FTP server on the same host. For this reason, applications are provided ports to use "direct" connections for specific software services. These ports help TCP/IP distinguish services so that data can get to the correct application. If you check the /etc/services, you will see the common ports and their usage. For example, FTP, HTTP, and Post Office Protocol (email retrieval server), you'll see

```
ftp     21/tcp
http    80/tcp      www-http    # WorldWideWeb HTTP
pop3    110/tcp    pop-3       # POP version 3
```

The ports defined in this example are 25 for FTP, 80 for HTTP, and 110 for POP3. Other common port assignments are 25 for Simple Mail Transport Protocol (SMTP) and 22 for Secure Shell (SSH) remote login. Note that these are not set in stone, and you can set up your server to respond to different ports. Although port 22 is listed in /etc/services as a default for SSH, the ssh server can be configured to listen on a different port by editing its configuration file /etc/ssh/sshd_config. The default setting (commented out with a pound sign) looks like this:

# Port 22

Edit the entry to use a different port, making sure to select an unused port number, such as

Port 2224

Make your changes, and then restart the ssh server. (See Chapter 7, "Managing Services," to see how to restart a service.) Remote users must now access the host through port 2224, which can be done using ssh -p (port) option like so:

```
$ ssh -p 2224 remote_host_name_or_IP
```

# Network Organizing Organization

Properly organizing your network addressing process grows more difficult as the size of your network grows. Setting up network addressing for a Class C network with less than 254 devices is simple. Setting up addressing for a large, worldwide company with a Class A network and many different users can be extremely complex. If your company has fewer than 254 hosts (meaning any device that requires an IP address, including computers, printers, routers, switches, and other devices) and all your workgroups can share information, a single Class C network will be sufficient.