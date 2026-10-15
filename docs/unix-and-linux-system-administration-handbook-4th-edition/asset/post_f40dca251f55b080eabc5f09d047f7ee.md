
256 virtual identities attached to it. If you need to change this limit, use ndd to change the parameter ip_addrs_per_if (see page 498 for details on using ndd).

To configure a virtual interface, just run ifconfig on one of the virtual names. (The underlying physical interface must already have been "plumbed.") In most cases, you'll want to set up the system so that the ifconfigs for virtual interfaces happen automatically at boot time.

Here is an example in which a Solaris machine has an address in private address space on an internal virtual private network (VPN) and an external address for the Internet, both associated with the same physical interface, hme0. To have these interfaces configured automatically at boot time, the administrator has set up two hostname files: /etc/hostname.hme0 and /etc/hostname.hme0:1.

```
$ ls -l /etc/host*
-rw-r--r-- 1 root root 10 Nov 4 10:19 /etc/hostname.hme0
-rw-r--r-- 1 root root 16 Dec 21 19:34 /etc/hostname.hme0:1
```

Hostname files can contain either hostnames from the /etc/hosts file or IP addresses. In this case, the administrator has used one of each:

```
$ cat /etc/hostname.hme0
overkill
$ cat /etc/hostname.hme0:1
206.0.1.133
$ grep overkill /etc/hosts
10.1.2.9 overkill overkill.domain
```

At boot time, both addresses are automatically configured (along with the loopback address, which we omitted from the output shown below):

```
$ ifconfig -a
hme0: flags=863<UP,BROADCAST,NOTRAILERS,RUNNING,MULTICAST> mtu 1500 inet 10.1.2.9 netmask ffffff00 broadcast 10.1.2.255
hme0:1: flags=863<UP,BROADCAST,NOTRAILERS,RUNNING,MULTICAST> mtu 1500 inet 206.0.1.133 netmask ffffff80 broadcast 206.0.1.255
```

## HP-UX virtual interfaces

On HP-UX, you add virtual interfaces with the ifconfig command. The syntax is very similar to that of Solaris. For example, to add the first interface, you would execute the command

```
$ sudo ifconfig lan0:1 192.168.69.1 up
```

## AIX virtual interfaces

On AIX, you create an "alias" to add additional IP addresses to an interface. For example, to add 192.168.1.3 as a virtual IP address for the en0 interface, you can use ifconfig:

```
$ sudo ifconfig en0 192.168.1.3 netmask 255.255.255.0 alias
```

However, this alias is only temporary. To create a permanent virtual IP, use the chdev command:

```
$ sudo chdev -l en0 -a alias4=192.168.1.3,255.255.255.0
```

## Telling Apache about virtual interfaces

In addition to creating the virtual interfaces, you need to tell Apache what documents to serve when a client tries to connect to each interface (IP address). You do this with a VirtualHost clause in the httpd.conf file. There is one VirtualHost clause for each virtual interface that you've configured. Here's an example:

```
<VirtualHost 128.138.243.150>
ServerName www.company.com
ServerAdmin webmaster@www.company.com
DocumentRoot /var/www/htdocs/company
ErrorLog logs/www.company.com-error_log
CustomLog logs/www.company.com-access_log combined
ScriptAlias /cgi-bin/ /var/www/cgi-bin/company
</VirtualHost>
```

In this example, any client that connects to the virtual host 128.138.243.150 is served documents from /var/www/htdocs/company. Nearly any Apache directive can go into a VirtualHost clause to define settings specific to that virtual host. Relative directory paths, including those for the DocumentRoot, ErrorLog, and CustomLog directives, are interpreted in the context of the ServerRoot.

With name-based virtual hosts, multiple DNS names all point to the same IP address. The Apache configuration is similar, but you specify the primary IP address on which Apache should listen for incoming named virtual host requests and you omit the IP address in the VirtualHost clause:

```
NameVirtualHost 128.138.243.150

<VirtualHost *>
ServerName www.company.com
ServerAdmin webmaster@www.company.com
DocumentRoot /var/www/htdocs/company
ErrorLog logs/www.company.com-error_log
CustomLog logs/www.company.com-access_log combined
ScriptAlias /cgi-bin/ /var/www/cgi-bin/company
</VirtualHost>
```

In this configuration, Apache looks in the HTTP headers to determine the requested site. The server listens for requests for www.company.com on its main IP address, 128.138.243.150.

## 23.4 THE SECURE SOCKETS LAYER (SSL)

The SSL protocol secures communications between a web site and a client browser. URLs that start with https:// use this technology. SSL uses cryptography to prevent eavesdropping, tampering, and message forgery.
