associated RHCE objective. In either case, the service normally only listens on the localhost address, which is one level of security. Other levels of security are possible based on hosts, usernames, and more. For more information, see Chapter 13.

# SSH Service-Specific Security

The SSH service is installed by default even in the minimal installation of RHEL 6. That encourages its use as a remote administration tool. However, there are risks associated with the SSH server that can be minimized. For example, it's not necessary to send even encrypted passwords over a network. Remote logins to the root account do not have to be allowed. Security can be further regulated by user.

# Host-Based Security

Host-based security refers to access limits, not only by the system hostnames, but also by their fully qualified domain names and IP addresses. The syntax associated with host-based security can vary. For example, while every system recognizes a specific IP address such as 192.168.122.50, the use of wildcards or Classless Inter-Domain Routing (CIDR) notation for a range of IP addresses varies by service. Depending on the service, you may use one or more of the following options for the noted range of network addresses:

```
192.168.122.0/255.255.255.0
192.168.122.0/24
192.168.122.*
192.168.122.
192.168.122
```

Just be careful, some of these options may lead to syntax errors on some but not all network services. In a similar fashion, any of the following options may or may not work to represent all of the systems on an example.com network:

```
*.example.com
.example.com
example.com
```

# User-Based Security

User-based security includes users and groups. Generally, users and groups who are allowed or denied access to a service are collected in a list. That list could include a