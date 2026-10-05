# Installing and configuring Unbound

637

Private addresses private-address: ip-address-or-subnet [none] private-domain: domain-name [none]

The private-address statement blocks the listed IP addresses from being returned in query results. It's normally in conjunction with RFC1918 private IP addresses (see page 462) to keep shameful addresses from escaping to the Internet. This behavior is generally what you want for external sites, but if you are actually using RFC1918 addresses, you probably don't want to blacklisting your own internal addresses. The private-domain statement resolves this conflict by allowing the specified domain and all its subdomains to contain private addresses.

The next set of configuration options pertains to the remote-control statement, which controls communication between unbound and the unbound-control program. Communication is controlled by self-signed SSL/TLS certificates in X.509 format that are set up by unbound-control-setup program. There are only a few options, so we list them here:

+   - control-enable: yes | no [no]
- control-interface: ip-address [localhost(127.0.0.1 and ::1)]
- control-port: port [953]
- server-key: private-key-file [unbound-server.key]
- server-cert: certificate-file-pem [unbound-server.pem]
- control-key: private-key-file [unbound-control.key]
- control-cert: certificate-file-pem [unbound-control.pem]

You can control unbound from any network on the Internet. If you set authentication, run unbound-control-setup to create the necessary certificate files, set the control-enable option to yes, and set the control-interface to the network interface on which the server should listen for control commands. You can use 0.0.0.0 (:0) to enable all interfaces. The default is to require the controller to be logged in the same machine as unbound, which is fairly safest.

Stub zones stub-zone: name: domain-name [none] stub-host: hostname [none] stub-addr: ip-address@port [none]

A stub-zone clause lets you tunnel queries for a particular domain to an authoritative server that you designate rather resolving them in the usual hierarchy from the root. For example, you might want users to see a private view of your local network that includes more hosts than seen by DNS queries on the outside. The name “stub zone” is unfortunate and has no connection to the stub zones used in the BIND word.

To implement this configuration, run an authoritative server on a different host (or on the same host at a different port) to serve your local version of the zone. You point stub-zone options. You can specify the hostname of the server (stub-host) or its IP address (stub-addr). You can also specify the port, which defaults to 53. The address form