library that allows any program to perform DNS queries. The resolver comes standard with Red Hat Linux. In this section, you will learn to configure the resolver.

Typically, the Red Hat installation program asks you about your DNS server and automatically configures the necessary resolver configuration file. However, it is often necessary to change the resolver configuration to reflect any changes to the DNS server you use. For example, if you configure your resolver during Red Hat installation and later change your ISP, you need to configure it again manually. This section shows you how.

If you are planning on using your ISP's DNS server for resolving names and IP addresses, ask your ISP to give you the hostname and the IP address of its DNS servers. After you have the required information, you can configure the resolver.

First you need to modify the resolver configuration file called /etc/resolv.conf. Listing 15-1 shows a typical /etc/resolv.conf file for a domain called evoknow.com.

# Listing 15-1 An example /etc/resolv.conf file

```
# Default Domain
domain evoknow.com

# Default search list
search evoknow.com

# First name server
nameserver 206.171.50.50

# Second name server
nameserver 206.171.50.55
```

Like many other common Linux configuration files, this file has a very simple format. Any blank line or lines starting with # are ignored. The only meaningful lines are the ones with a domain, search, or name server directive.

The domain directive enables you to specify the default domain name for the system. If you do not have this line set to the domain name of your system, the default domain name is automatically extracted from the host name of your system.