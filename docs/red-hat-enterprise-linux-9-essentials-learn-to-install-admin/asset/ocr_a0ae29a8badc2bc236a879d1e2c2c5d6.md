# RHEL 9 Firewall Configuration with firewalld

where a greater level of trust is expected. New zones may be added to the system, and existing zones modified to add or remove rules. Zones may also be deleted entirely from the system. Table 14-1 lists the set of zones available by default on a RHEL 9 system:

| Zone | Description |
|---|---|
| drop | The most secure zone. Only outgoing connections are permitted, and all incoming connections are dropped without any notification to the connecting client. |
| block | Similar to the drop zone, with the exception that incoming connections are rejected with an icmp-host-prohibited or icmp6-adm-prohibited notification. |
| public | Intended for use when connected to public networks or the internet where other computers are not known to be trustworthy. Allows select incoming connections. |
| external | When a system acts as the internet gateway for a network of computers, the external zone is applied to the interface connected to the internet.

This zone is used with the *internal* zone when implementing masquerading or network address translation (NAT), as outlined later in this chapter. Allows select incoming connections. |
| internal | Used with the *external* zone and applied to the interface connected to the internal network. Assumes that the computers on the internal network are trusted. Allows select incoming connections. |
| dmz | For use when the system is running in the demilitarized zone (DMZ). These are generally computers that are publicly accessible but isolated from other parts of your internal network. Allows select incoming connections. |
| work | For use when running a system on a network in a work environment where other computers are trusted. Allows select incoming connections. |
| home | For use when running a system on a home network where other computers are trusted. Allows select incoming connections. |
| trusted | The least secure zone. All incoming connections are accepted. |
| nm-shared | This zone is used internally by NetworkManager when implementing connection sharing. |
| libvirt | Used by virtual networks, typically when the server is hosting virtual machines. |

Table 14-1

To review specific settings for a zone, refer to the corresponding XML configuration file located on the system in the `/usr/lib/firewalld/zones` directory. The following, for example, lists the content