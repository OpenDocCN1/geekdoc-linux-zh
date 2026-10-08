When using TCP wrappers in conjunction with xinetd access controls, it is important to understand the relationship between the two access control mechanisms.

The following is the order of operations followed by xinetd when client requests a connection:

+   1. The xinetd daemon accesses the TCP wrappers access rules through a libwrap.a library. If a deny rule matches the client host, the connection is dropped. If an allow rule matches the client host, the connection is passed to xinetd.
2. The xinetd daemon checks its own access control rules for the xinetd service and the requested service. If a deny rule matches the client host the connection is dropped. Otherwise, xinetd starts an instance of the requested service and passes control of the connection to it.

> Important
Care should be taken when using TCP wrappers access controls in conjunction with xinetd access controls. Misconfiguration can cause undesired effects.

# 15.4.3.3. Binding and Redirection Options

The service configuration files for xinetd support binding the service to an IP address and redirecting incoming requests for service to another IP address, hostname, or port.

Binding is controlled with the bind option in the service-specific configuration files and links the service to one IP address on the system. Once configured, the bind option only allows requests for the proper IP address to access the service. This way services can be bound to different network interfaces based on name.

This is particularly useful for systems with multiple networks or with multiple IP addresses configured. On such a system, insecure services like Telnet, can be configured to listen only on the interface connected to a private network and not to the interface connected with the Internet.

The redirect option accepts an IP address or hostname followed by a port number. It configures the service to redirect all requests for this service to the specified host and port number. This feature can be used to point to another port number on the same system, redirect the request to different IP address on the same machine, shift the request to a different system and port number, or any combination of these options. In this way, a user connecting to a system may be rerouted to another system with no disruption.

The xinetd daemon is able to accomplish this redirection by spawning a process that stays alive for the duration of the connection between the client machine and the host actually providing the service, transferring data between the two systems.

But the advantages of bind and redirect options are most clearly seen when they are used by binding to a particular IP address on a system and redirecting requests for this service to a second machine that only the first machine can use, an internal system can be used to provide services for a totally different network. Alternatively, these options can be used to limit the exposure of a particular service on a multi-homed machine to a known IP address, as well as redirect requests for that service to another machine specifically configured for that purpose.

For example, a system that is used as a firewall with its Telnet service:

```
service telnet
{
    socket_type = stream
    wait        = no
    server      = /usr/sbin/in.xinetd
```