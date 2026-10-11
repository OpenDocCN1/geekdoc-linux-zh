4.  The virtual interface in domain0 is added to the bridge with the physical interface.

These steps only affect the general network connectivity. The IP configuration in the Xen domains has to be done separately with DHCP or a static network configuration.

xend is performing these network changes with the help of scripts, which are located at /etc/xen/scripts/. The following scripts are used for bridged networking:

+   - network-bridge. This script is called initially when xend is started. It sets up the bridge xenbr0 and moves the physical interfaces onto that bridge.

+   - vif-bridge. This script is called for every domain that is started and adds the virtual interface to the bridge.

In the file /etc/xen/xend-config.sxp you can configure which network scripts are used by xend.

# Understand the Network Interfaces in domain0

When you look at the network interfaces in domain0 with the command ip a, you can see that there are many more interfaces than in a regular Linux installation.