With inetd(8), almost anything can be a network service.

# # DHCP

Dynamic Host Configuration Protcol (DHCP) is the standard method for handing out IP addresses to client computers. While DHCP services aren’t integrated with FreeBSD out of the box, they’re commonly required to implement such services as diskless workstations. We’ll cover the basics of DHCP configuration here so you can set up your own network.

These days, every firewall and embedded device has a DHCP server. Why would you need a separate DHCP server? Most of the embedded DHCP servers lack functions needed to run diskless clients, such as network-booted servers and VoIP phones. When they do support such functions, those DHCP servers are often difficult to manage. Services are meant to run on actual servers. We’ll cover enough of DHCP to let you configure your own network clients, including diskless hosts.

FreeBSD packages include several DHCP servers. The two I like are OpenBSD’s dhcpd and ISC DHCP server. The ISC DHCP server is an industry standard and supports every feature you could possibly want. For small deployments, I recommend OpenBSD’s dhcpd. The OpenBSD folks took ISC DHCP, ripped out all the rarely used features, and made a smaller, simpler server. The configuration file is still one-way compatible; you can run an OpenBSD dhcpd configuration on ISC’s DHCP server without trouble. (The reverse is also true if you’re not using any of the features OpenBSD ripped out of the server.) If you want to run diskless FreeBSD clients, or if you need LDAP integration, switching to the more complex ISC server is fairly straightforward. You can install only one of the two servers.

The package for either server includes dhcpd(8), the configuration file /usr/local/etc/dhcpd.conf, and extensive man pages.

![](bbox=[0.12, 0.85, 0.85, 0.91])