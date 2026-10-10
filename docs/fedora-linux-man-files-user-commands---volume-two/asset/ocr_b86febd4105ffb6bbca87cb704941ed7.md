# > CONCEPTS

firewalld has a D-Bus interface for firewall configuration of services and applications. It also has a command line client for the user. Services or applications already using D-Bus can request changes to the firewall with the D-Bus interface directly. For more information on the firewall D-Bus interface, please have a look at **firewalld.dbus**(5).

firewalld provides support for zones, predefined services and ICMP types and has a separation of runtime and permanent configuration options. Permanent configuration is loaded from XML files in */usr/lib/firewalld* or */etc/firewalld* (see the section called “DIRECTORIES”).

If NetworkManager is not used, there are some limitations: firewalld will not get notified about network device renames. If firewalld gets started after the network is already up, the connections and manually created interfaces are not bound to a zone. You can add them to a zone with **firewall-cmd [--permanent] --zone=zone --add-interface=interface**, but make sure that if there's a /etc/sysconfig/network-scripts/ifcfg-*interface*, the zone specified there with ZONE=zone is the same (or both are empty/missing for default zone), otherwise the behaviour would be undefined.

# Zones

A network or firewall zone defines the trust level of the interface used for a connection. There are several pre-defined zones provided by firewalld. Zone configuration options and generic information about zones are described in **firewalld.zone**(5)

# Services

A service can be a list of local ports and destinations and additionally also a list of firewall helper modules automatically loaded if a service is enabled. Service configuration options and generic information about services are described in **firewalld.service**(5). The use of predefined services makes it easier for the user to enable and disable access to a service.

# ICMP types

The Internet Control Message Protocol (ICMP) is used to exchange information and also error messages in the Internet Protocol (IP). ICMP types can be used in firewalld to limit the exchange of these messages. For more information, please have a look at **firewalld.icmptype**(5).

# Runtime configuration

Runtime configuration is the actual active configuration and is not permanent. After reload/restart of the service or a system reboot, runtime settings will be gone if they haven't been also in permanent configuration.