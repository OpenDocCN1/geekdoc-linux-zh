This option will result in a warning message.

Add the IPv4 forward port in the default zone. This option can be specified multiple times.

The port can either be a single port number portid or a port range portid-portid. The protocol can either be tcp or udp. The destination address is an IP address.

# —block-icmp=icmptype

This option will result in a warning message.

Add an ICMP block for icmptype in the default zone. This option can be specified multiple times.

The icmptype is the one of the icmp types firewalld supports. To get a listing of supported icmp types: **firewall-cmd** **—get-icmptypes**

# Zone Options

# —get-default-zone

Print default zone for connections and interfaces.

# —set-default-zone=zone

Set default zone for connections and interfaces where no zone has been selected. Setting the default zone changes the zone for the connections or interfaces, that are using the default zone.

# —get-zones

Print predefined zones as a space separated list.

# —get-services

Print predefined services as a space separated list.

# —get-icmptypes

Print predefined icmptypes as a space separated list.

# —get-zone-of-interface=interface

Print the name of the zone the interface is bound to or no zone.

# —get-zone-of-source=source[/mask]