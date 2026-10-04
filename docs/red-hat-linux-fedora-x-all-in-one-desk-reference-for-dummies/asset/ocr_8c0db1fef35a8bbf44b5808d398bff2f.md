# Checking Out TCP/IP Networks

# /etc/nsswitch.conf

This file, known as the name service switch (NSS) file, specifies how services such as the name resolver library, NIS, NIS+, and local configuration files (such as /etc/hosts and /etc/shadow) interact.

NIS and NIS+ are network information services — another type of name-lookup service. Newer versions of the Linux kernel use the /etc/nsswitch.conf file to determine what takes precedence: a local configuration file, a service such as DNS (Domain Name Service), or NIS.

As an example, the following entries in the /etc/nsswitch.conf file says that the resolver first tries the /etc/hosts file, and then tries NIS+, and finally DNS:

```
hosts: files nisplus dns
```

You can find out more about the /etc/nsswitch.conf file by typing info "Name Service" (including the quotes) in a terminal window.

![](bbox=[0.1285, 0.3835, 0.185, 0.445])

# Checking Out TCP/IP Networks

After you configure Ethernet and TCP/IP (whether during Fedora Core Installation or by running the Network Configuration tool later on), you can use various networking applications without any problem. If you do run into trouble, Fedora Core includes several tools to help you monitor and diagnose-problems.

# Checking the network interfaces

Using the /sbin/ifconfig command to view the currently configured network interfaces (that is, to associate an IP address with a network). If you run ifconfig without any command-arguments, the command displays information about current interfaces. The following is a typical invocation of the result output:

```
/sbin/ifconfig
eth0  link: Ethernet  Haddr:00:08:74:e5:c1:60
       inet 192.168.0.2  broadcast:192.168.0.255  Mask:255.255.255.0
       inet6 addr:fe80::247ff:fe60/64  scope=link
       MTU:1500  ieLLIC1
       RX packets:93700 errors:0 dropped:0 overruns:1 frame:0
       TX packets:74097 errors:0 dropped:0 overruns:0 carrier:0
       collisions:0 txqueue:1000
       RX bytes:35734333 (32.0 Mb)  TX bytes:8832457 (8.4 Mb)
```

Managing the Network Chapter 4