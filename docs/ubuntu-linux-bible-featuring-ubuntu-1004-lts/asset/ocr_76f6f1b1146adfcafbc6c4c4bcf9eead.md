(or are willing to accept the consequences). The next few sections explain how to manually create DHCP server's configuration file and discuss some of the more important options that you may need to add to a DHCP server configuration file to maximize its usability in your environment.

# Creating DHCP Configuration Files Using a Text Editor

This section explains the basics of a DHCP configuration file and the most common set of entries you will need to put in your configuration file to serve a specific range of IP addresses via a shiny new DHCP server.

# Tip

The file /etc/dhcp3/dhcpd.conf is the configuration file used by the dhcp3 server that I suggested installing in the process. If you installed another DHCP server, shame on you — I'm sure that you had your reasons, and your configuration file is probably /etc/dhcpd.conf, which is the traditional location for a DHCP server's configuration file. An easy way to verify the configuration file used by your DHCP server is the following command, where server-name is the name of the executable for your DHCP server:

```
strings $(which server-name) | grep dhcpd.conf
```

This will display several strings, one of which will be the full pathname of your DHCP server's configuration file. This works for all of the DHCP servers I've used —you may find that you need to be slightly creative with the arguments to the grep command, but you'll certainly find your config file with similar command.

To configure DHCP for your network, you will need to add the following section (referred to by DHCP config file fans as a *stanza*) to your DHCP server's configuration file:

```
1: option domain-name "your.domain.name";
2: option domain-name-servers nameserver1-address, nameserver2-address, ...;
3: option routers router-address;
4: option subnet-mask 255.255.255.0;
5: subnet-address netmask-for-subnet (
6: range full-start-address full-end-address;
7: )
```

# Note

The actual configuration file used by your DHCP server does not include line numbers (and cannot). I've added the line numbers to make it easier to match entries in this sample file with the explanations that follow.

This example provides an extremely minimal DHCP configuration file that is useful, which leverages many of the default values provided by the DHCP server. Each line of this stanza has the following meaning:

+   1. The name of the domain to any host that has an IP address from this server should belong. Replace *your.domain.name* with the name of your domain.