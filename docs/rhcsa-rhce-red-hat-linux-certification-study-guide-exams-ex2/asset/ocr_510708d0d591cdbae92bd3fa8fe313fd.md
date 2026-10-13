# Configure Name Resolution

The final piece in network configuration is typically name resolution. In other words, does the local system have the information required to translate domain names such as mcgraw-hill.com to IP addresses such as 198.45.24.143?

Name resolution was easy when Unix was first being developed. When the predecessor to the Internet was first put into use, the worldwide computer network had four hosts, one computer at each of four different universities. It was easy to set up a static file with a list of each of their names and corresponding addresses. That file has evolved into what is known in Linux as /etc/hosts.

But now the Internet is more complex. While you could try to set up a database of every domain name and IP address on the Internet in the /etc/hosts file, that would take almost forever. That's why most users set up connections to DNS, Domain Name Service, servers. On RHEL 6, that's still documented in the /etc/resolv.conf configuration file. On the baseline system created in Chapter 2, that file contains two lines:

```
search example.com
nameserver 192.168.122.1
```

The first line appends the example.com domain to given hostnames; for example, if you were to run the ping command on the server1 system, it would actually search for the server1.example.com system. The second line specifies the IP address associated with the local DNS server. As an RHCE, you need to know how to configure a caching-only DNS server; that subject is covered in Chapter 17. DNS configuration is not an RHCSA requirement.

On smaller networks, some administrators set up an /etc/hosts file as a database for the name of each system and IP address on the local network. If desired, administrators could even set up a few IP addresses of domains on the Internet. For the systems described in earlier chapters, an appropriate /etc/hosts file might contain the following directives:

```
192.168.122.50 server1.example.com
192.168.122.150 tester1.example.com
192.168.100.100 outsider1.example.org
```

But if you've configured a connection to a DNS server and systems in /etc/hosts, what's searched first? The search order is specified by one line in the /etc/nsswitch.conf configuration file, which searches for host names first in local files (/etc/hosts) followed by any accessible DNS servers.

```
hosts: files dns
```