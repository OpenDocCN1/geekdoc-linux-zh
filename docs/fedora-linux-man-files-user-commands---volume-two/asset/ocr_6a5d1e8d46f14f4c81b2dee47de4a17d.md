```
[**-permanent** [**-zone=zone**] **-add-forward-port**=port=portid[-portid]:proto=protocol
[:toport=portid[-portid]][[:toaddr=address[/mask]]] [**-timeout**=timeval]
```

Add the IPv4 forward port for zone. If zone is omitted, default zone will be used. This option can be specified multiple times. If a timeout is supplied, the rule will be active for the specified amount of time and will be removed automatically afterwards. timeval is either a number (of seconds) or number followed by one of characters s (seconds), m (minutes), h (hours), for example 20m or 1h.

The port can either be a single port number portid or a port range portid-portid. The protocol can either be tcp or udp. The destination address is a simple IP address.

The **-timeout** option is not combinable with the **-permanent** option.

For IPv6 forward ports, please use the rich language.

```
[**-permanent** [**-zone=zone**] **-remove-forward-port**=port=portid[-portid]:proto=protocol[:toport=portid[-portid]][[:toaddr=address[/mask]]]]
```

Remove the IPv4 forward port from zone. If zone is omitted, default zone will be used. This option can be specified multiple times.

For IPv6 forward ports, please use the rich language.

```
[**-permanent** [**-zone=zone**] **-query-forward-port**=port=portid[-portid]:proto=protocol[:toport=portid[-portid]][[:toaddr=address[/mask]]]]
```

Return whether the IPv4 forward port has been added for zone. If zone is omitted, default zone will be used. Returns 0 if true, 1 otherwise.

For IPv6 forward ports, please use the rich language.

```
[**-permanent** [**-zone=zone**] **-add-masquerade** [**-timeout**=timeval]
```

Enable IPv4 masquerade for zone. If zone is omitted, default zone will be used. If a timeout is supplied, masquerading will be active for the specified amount of time. timeval is either a number (of seconds) or number followed by one of characters s (seconds), m (minutes), h (hours), for example 20m or 1h. Masquerading is useful if the machine is a router and machines connected over an interface in another zone should be able to use the first connection.

The **-timeout** option is not combinable with the **-permanent** option.

For IPv6 masquerading, please use the rich language.

```
[**-permanent** [**-zone=zone**] **-remove-masquerade**
```