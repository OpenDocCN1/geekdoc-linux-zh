# Configuring the hosts.allow and hosts.deny Files

The TCP Wrappers configuration files are /etc/hosts.allow and /etc/hosts.deny. TCP Wrappers uses the following logic to determine whether to allow a connection, stopping at the first match:

+   - If the connection matches a service/client pair in hosts.allow, access is granted.
- If the connection matches a service/client pair in hosts.deny, access is denied.
- Otherwise, access is granted.

The syntax of hosts.allow and hosts.deny files is simple:
service : client_address_list [ : option ] ...

# Enable the Extended Access Control Language

TCP Wrappers supports an extended version of its access control language used in the hosts.allow and hosts.deny files. This support is enabled by default on many systems, but if you are compiling TCP Wrappers from scratch, you should add -PROCESS_OPTIONS to your compile flags. Some options discussed in this section of the chapter are available only in the extended language.

In this example, the service is the service for which you are controlling access, such as telnet or ftp. The client_address_list is a list of one or more client addresses for which this rule applies. You can also specify various options after this second field to control logging, IND support, banners, and so on. Separate each option with a colon, and in the rest of the configuration.

To allow Telnet connections from 192.168.1.2, make the following entry in hosts.allow:

```
telnetd: 192.168.1.2
```

Note that the service name is the name of the daemon process specified in inetd.conf. You can also specify networks by omitting fields from IP addresses. For example, when denying FTP access from 192.168.2.0, add the following line to hosts.deny:

```
telnetd: 192.168.1.1
```

You can list multiple addresses in a single entry by separating them with a comma.

You can use hostname and domain instead of IP addresses to configure TCP Wrappers. If you use domains, precede them with a dot (\.") so that they do not match a substring of another longer domain name (for example, "example.com" instead of "example.com"),

# Beware of Hostname Spoofing

Anyone with control of reverse DNS (address to name mappings) for their network can spoof a host-name for any of their addresses. For this reason, you should only use domain names in your TCP Wrappers configuration as a last resort.