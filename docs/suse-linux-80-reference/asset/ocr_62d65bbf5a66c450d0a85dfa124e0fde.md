+   - `httpd_accel_port 80` # the port number where the actual HTTP server is located
+   - `httpd_accel_with_proxy on`
+   - `httpd_accel_uses_host_header on`

# Firewall Configuration with SuSEfirewall

Now redirect all incoming requests via the firewall with help of a port forwarding rule to the Squid port.
To do this, use a SuSE-provided tool: SuSEfirewall. Its configuration file can be found in `/etc/sysconfig/scripts/SuSEfirewall2-custom`. Again, the configuration file consists of well-documented entries. Even to set only a transparent proxy, you must configure a couple firewall options. In our example:

+   - Device pointing to the Internet: `FW_DEV_WORLD="eth1"`
+   - Device pointing to the network: `FW_DEV_INT="eth0"`

Set ports and services (see `/etc/exports`) on the firewall being accessed from untrusted networks such as the Internet. In this example, only web services are offered to the outside:

```
FW_SERVICES_EXTERNAL_TCP="www"
```

Define ports or services (see `/etc/exports`) on the firewall to be accessed from the secure network, both TCP and UDP services:

```
FW_SERVICES_INTERNAL_TCP="domain www 3128"
FW_SERVICES_INTERNAL_UDP="domain"
```

We are accessing web services and Squid (whose default port is 3128).
The service “domain” specified before stands for DNS or Domain Name Server.
It is most common to use this service, otherwise we simply take it out of the above entries and set the following option to no:

```
FW_SERVICE_DNS="yes"
```

The most important option is number 15.