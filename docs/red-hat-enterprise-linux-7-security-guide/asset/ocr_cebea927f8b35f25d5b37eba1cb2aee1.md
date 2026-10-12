```
`~]# firewall-cmd --zone=zone-name --list-sources`
```

+   2. Remove the source from the zone permanently:
+   `~]# firewall-cmd --zone=zone-name --remove-source=<source>`

+   3. Make the new settings persistent:
+   `~]# firewall-cmd --runtime-to-permanent`

# 5.8.3. Adding a Source Port

To enable sorting the traffic based on a port of origin, specify a source port using the `--add-source-port` option. You can also combine this with the `--add-source` option to limit the traffic to a certain IP address or IP range.

To add a source port:

```
`~]# firewall-cmd --zone=zone-name --add-source-port=<port-name>/<tcp|udp|sctp|dccp>`
```

# 5.8.4. Removing a Source Port

By removing a source port you disable sorting the traffic based on a port of origin.

To remove a source port:

```
`~]# firewall-cmd --zone=zone-name --remove-source-port=<port-name>/<tcp|udp|sctp|dccp>`
```

# 5.8.5. Using Zones and Sources to Allow a Service for Only a Specific Domain

To allow traffic from a specific network to use a service on a machine, use zones and source.

For example, to allow traffic from 192.168.1.0/24 to be able to reach the HTTP service while any other traffic is blocked:

+   1. List all available zones:
+   `~]# firewall-cmd --get-zones`
+   `block dmz drop external home internal public trusted work`

+   2. Add the source to the trusted zone to route the traffic originating from the source through the zone:
+   `~]# firewall-cmd --zone=trusted --add-source=192.168.1.0/24`

+   3. Add the http service in the trusted zone:
+   `~]# firewall-cmd --zone=trusted --add-service=http`