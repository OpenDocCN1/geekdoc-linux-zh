# The **squid.conf** File

The Squid configuration file is **squid.conf**, located in the */etc/squid* directory. In the */etc/squid/squid.conf* file, you set general options such as ports used, security options controlling access to the server, and cache options for configuring caching operations. You can use a backup version called */etc/squid/squid.conf.default* to restore your original defaults. The default version of **squid.conf** provided with the Squid software includes detailed explanations of all standard entries, along with commented default entries. Entries consist of tags that specify different attributes. For example, **maximum_object_size** and **maximum_object_size** set limits on objects transferred.

```
maximum_object_size 4096 KB
```

As a proxy, Squid will use certain ports for specific services, such as port 3128 for HTTP services like Web browsers. Default port numbers are already set for Squid. Should you need to use other ports, you can set them in the */etc/squid/squid.conf* file. The following entry shows how you would set the Web browser port:

```
http_port 3128
```

> **NOTE** *Squid uses the Simple Network Management Protocol (SNMP) to provide status information and statistics to SNMP agents managing your network. You can control SNMP with the **snmp access** and **port** configurations in the **squid.conf** file.*

# Security

Squid can use its role as an intermediary between Web clients and a Web server to implement access controls, determining who can access the Web server and how. Squid does this by checking access control lists (ACLs) of hosts and domains that have had controls placed on them. When it finds a Web client from one of those hosts attempting to connect to the Web server, it executes the control. Squid supports a number of controls with which it can deny or allow access to the Web server by the remote host's Web client (see Table 24-2). In effect, Squid sets up a firewall just for the Web server.

The first step in configuring Squid security is to create ACLs. These are lists of hosts and domains for which you want to set up controls. You define ACLs using the **acl** command, in which you create a label for the systems on which you are setting controls. You then use commands such as **http_access** to define these controls. You can define a system, or a group of systems, by use of several **acl** options, such as the source IP address, the domain name, or even the time and date. For example, the **src** option is used to define a system or group of systems with a certain source address. To define an **acl** entry for a group of systems in a local network referred to as mylan with the addresses 192.168.0.0 through 192.168.0.255, use the following ACL definition:

```
acl mylan src 192.168.0.0/255.255.255.0
```

Once it is defined, you can use an ACL definition in a Squid option to specify a control you want to place on those systems. For example, to allow access by the mylan group of local systems to the Web through the proxy, use an **http_access** option with the **allow** action specifying **mylan** as the **acl** definition to use, as shown here:

```
http_access allow mylan
```