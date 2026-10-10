Options in this section affect only one particular zone. If used with `—zone=zone` option, they affect the zone *zone*. If the option is omitted, they affect default zone (see **`—get-default-zone`**).

For a list of predefined zones use **firewall-cmd `—get-zones`**.

An interface name is a string up to 16 characters long, that may not contain , / ! and *.

[**`—permanent`**] [**`—zone=zone`**] `—list-interfaces`

List interfaces that are bound to zone *zone* as a space separated list. If *zone* is omitted, default zone will be used.

[**`—permanent`**] [**`—zone=zone`**] `—add-interface=interface`

Bind interface *interface* to zone *zone*. If *zone* is omitted, default zone will be used. As a end user you don’t need this in most cases, because NetworkManager (or legacy network service) adds interfaces into zones automatically (according to *ZONE=* option from *ifcfg-interface* file). You should do it only if there’s no /etc/sysconfig/network-scripts/ifcfg-*interface* file. If there is such file and you add interface to zone with this `—add-interface` option, make sure the *zone* is the same in both cases, otherwise the behaviour would be undefined. For permanent association of interface with a zone, see also ‘How to set or change a zone for a connection?’ in **firewalld.zones(5)**.

[**`—zone=zone`**] `—change-interface=interface`

Change zone the interface *interface* is bound to to zone *zone*. It’s basically `—remove-interface` followed by `—add-interface`. If the interface has not been bound to a zone before, it behaves like `—add-interface`. If *zone* is omitted, default zone will be used.

[**`—permanent`**] [**`—zone=zone`**] `—query-interface=interface`

Query whether interface *interface* is bound to zone *zone*. Returns 0 if true, 1 otherwise.

[**`—permanent`**] `—remove-interface=interface`

Remove binding of interface *interface* from zone it was previously added to.

# Options to Handle Bindings of Sources

Binding a source to a zone means that this zone settings will be used to restrict traffic from this source.