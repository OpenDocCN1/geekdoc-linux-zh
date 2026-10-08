# 262 PART 2 Layered Security and Linux

# technical TIP

With a few firewall rules, you can channel all Web requests from inside your network through a proxy server. On the gateway between the internal network and the Internet, you'll need to regulate opting traffic. Specifically, with the following iptables rule, all traffic destined for port 80 for regular outgoing Web connections are redirected to port 3128, the standard for proxy server connections:

```
iptables -t nat A PREROUTING -p tcp --dport 80
-j REDIRECT --to-port 3128
```

For information on firewall rules and the iptables command, see Chapter 7.

# Basic Squid Configuration

Squid is perhaps the leading open source proxy server. It is a caching proxy that supports Hypertext Transfer Protocol (HTTP), HTTPS, and FTP communications. The basic Squid configuration file is squid.conf in the /etc/squid/ directory. Although the file includes more than 4000 lines, it is simple to configure. First, the standard port number associated with Squid communication is 3128, which is documented in the following directive:

```
http_port 3128
```

Generally, access is limited based on access control lists (ACLs). Although they share the same acronym as access control lists for Linux files, they are different within Squid. ACLs on Squid can limit access by IP address, hardware address, source domain name, destination name, time, Universal Resource Locator (URL), port number, protocol, browser, referrer, username, and name.

The simplest use of Squid ACL limits access by IP address. For example, the following directive specifies an ACL for a local source private IP address network along with the localhost system:

```
acl localhost src 127.0.0.1/32
acl some_net src 192.168.0.0/24
```

Be aware, this command replaces the following default, which allows access from all systems:

```
acl all src 0.0.0.0/0
```

Then, the following commands allow access from the localhost system, with systems on the noted private IP address network, denying access to all other systems:

```
http_access allow localhost
http_access allow some_net
http_access deny all
```