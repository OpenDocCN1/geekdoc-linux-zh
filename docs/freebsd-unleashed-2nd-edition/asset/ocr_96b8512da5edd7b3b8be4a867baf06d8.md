# TABLE 34.2 Continued

| Option | Action |
|---|---|
| `request option` | The client will request information for the specified options from the DHCP server. See the `dhcp-options` man page for information on the available options. |
| `require option` | The client will require information for the specified options from the DHCP server. If the required information is not provided, the client will reject the offer. See the `dhcp-options` man page for information on the available options. |
| `default option value` | If the DHCP server does not provide information for the specified option, then `value` will be used for that option. See the `dhcp-options` man page for information on the available options. |
| `supersede option value` | The specified option will always use `value`, even if the DHCP server sends a different value for that option. See the `dhcp-options` man page for information on the available options. |
| `reject address` | Any offers sent from the DHCP server with the IP address of `address` will be rejected. |

Many more options can be used in the `/etc/dhclient.conf` configuration file. See the `dhclient.conf` man page for more information on options available in this file. Also, see the `dhcp-options` man page for more information about the DHCP options that can be requested or required from the DHCP server.

As mentioned previously, most users will not need to make any changes to `/etc/dhclient.conf` because the default `dhclient` values will usually work fine.

# DHCP Server Daemon

FreeBSD does not come with the software required to run a DHCP server. However, free software is available in the FreeBSD ports collection for running a DHCP server. The port, called `isc-dhcp3`, is available in the net directory of the ports tree. See Chapter 14, “Installing Additional Software,” for information on how to install ports.

In addition, a program called `dhcpconf` (also available in the FreeBSD ports collection under the net directory) helps you create the configuration files necessary to run a DHCP server on FreeBSD.

When `isc-dhcp3` is installed, it will create a startup file in `/usr/local/etc/rc.d` called `isc-dhcpd.sh.sample`. The next time you restart your system, this file will cause the DHCP server to start automatically on system boot. The default startup file will work fine for a basic DHCP server configuration. See the `dhcpd` man page for the various options available to `dhcpd`.