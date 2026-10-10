```
`[--zone=zone] --remove-icmp-block=icmptype`
```

Remove the ICMP block for *icmptype* from *zone*. If *zone* is omitted, default *zone* will be used. This option can be specified multiple times.

```
`[--zone=zone] --query-icmp-block=icmptype`
```

Return whether an ICMP block for *icmptype* has been added for *zone*. If *zone* is omitted, default *zone* will be used. Returns 0 if true, 1 otherwise.

```
`[--zone=zone] --list-forward-ports`
```

List *IPv4* forward ports added for *zone* as a space separated list. If *zone* is omitted, default *zone* will be used.

For *IPv6* forward ports, please use the rich language.

```
`[--zone=zone] --add-forward-port=port=portid[-portid]:proto=proto[,top=portid[-portid]][:toaddr=address[/mask]]`
```

Add the *IPv4* forward port for *zone*. If *zone* is omitted, default *zone* will be used. This option can be specified multiple times.

The port can either be a single port number *portid* or a port range *portid-portid*. The protocol can either be *tcp* or *udp*. The destination address is a simple IP address.

For *IPv6* forward ports, please use the rich language.

```
`[--zone=zone] --remove-forward-port=port=portid[-portid]:proto=proto[,top=portid[-portid]][:toaddr=address[/mask]]`
```

Remove the *IPv4* forward port from *zone*. If *zone* is omitted, default *zone* will be used. This option can be specified multiple times.

For *IPv6* forward ports, please use the rich language.

```
`[--zone=zone] --query-forward-port=port=portid[-portid]:proto=proto[,top=portid[-portid]][:toaddr=address[/mask]]`
```

Return whether the *IPv4* forward port has been added for *zone*. If *zone* is omitted, default *zone* will be used. Returns 0 if true, 1 otherwise.

For *IPv6* forward ports, please use the rich language.

```
`[--zone=zone] --add-masquerade`
```

Enable *IPv4* masquerade for *zone*. If *zone* is omitted, default *zone* will be used. Masquerading is useful if the machine is a router and machines connected over an interface in another *zone* should be able to use the first connection.