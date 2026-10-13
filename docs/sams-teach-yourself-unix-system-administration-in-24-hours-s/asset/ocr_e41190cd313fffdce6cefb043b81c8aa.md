2. The default setup for dhclient is fine for 99% of the situations that you're likely to encounter as a Unix system administrator. The program has a variety of options that can be specified in the ifcfg file. These are alluded to in the following fragment of the important /sbin/ifup script, which brings up a specified interface:

```
if [ -n "${DYNC ONFIG}" ]; then
PUMPARGS=$PUMPARGS
DHCPDARGS="${DHCPDARGS} -n"
if [ -n "${DHCP_HOSTNAME}" ]; then
PUMPARGS="${PUMPARGS} -h ${DHCP_HOSTNAME}"
DHCPDARGS="${DHCPDARGS} -h ${DHCP_HOSTNAME}"
fi
if [ -n "${NEEDHOSTNAME}" ]; then
PUMPARGS="${PUMPARGS} -lookup-hostname"
DHCPDARGS="${DHCPDARGS} -H"
fi
if [ "${PEERDNS}" = "no" ]; then
PUMPARGS="${PUMPARGS} -d"
DHCPDARGS="${DHCPDARGS} -R"
fi
```

If you ignore the pump options (pump is an older alternative to dhclient in Linux, and most sites ignore it except for historical reasons), you can see that the arguments given to dhclient are the initial value of DHCPDARGS plus -n, -h dhcp hostname if specified as DHCP_HOSTNAME, -H if the system hostname should be set by the DHCP server (controlled by the presence of NEEDHOSTNAME in the config file), and -R if the existing /etc/resolv.conf DNS server list file should not be replaced by the information given by the DHCP server.

That's a bit confusing, so let's look again at the stock DHCP configuration. The variables that can affect how dhclient is invoked are DHCP_HOSTNAME, NEEDHOSTNAME, and PEERDNS. You'll notice that in /etc/sysconfig/network-scripts/ifcfg-eth0 the variable PEERDNS is set to "no," but the others are not referenced. This means that dhclient is invoked as

dhclient -n -R

which, as expected, prevents dhclient from overwriting the /etc/resolv.conf file, but otherwise assumes that the system is properly set up with its correct hostname.

That's the -R flag explained. What about the -n that's used regardless of configuration? Well, recall that DHCP is the Dynamic Host Configuration Protocol. One subtle ramification of the "dynamic" part of this is that while a DHCP server will assign an IP address to a specific workstation on request, it doesn't guarantee that IP address will stick with that workstation forever. Instead, systems are given a lease on their DHCP information, and have to renew the lease (for example, confirm that they're still up and online) with the DHCP server every so often.