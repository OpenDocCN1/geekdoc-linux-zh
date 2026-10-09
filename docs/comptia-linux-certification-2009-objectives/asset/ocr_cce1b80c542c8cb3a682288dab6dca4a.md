| Option | Description |
| :--- | :--- |
| -t | -T | Allows the server to test the configuration file for the correct syntax without performing any network operations. This helps in testing new configuration files before installing them. A similar feature can be applied to a lease database file using the -T option. |
| -cf config-file | Allows the use of an alternate configuration file. |
| -lf lease-file | Allows the use of an alternate lease file. |

![](bbox=[0.03, 0.28, 0.08, 0.33])

> DHCP client daemon (dhcpcd) is an implementation of the dhcp client. It runs on the client machine and configures it to work smoothly without additional configuration.

# Syntax

The syntax of the dhcpcd command is dhcpcd `[options]`.

# General Guidelines to Maintain DHCP Servers

Some general guidelines that are required to maintain a DHCP server are:

+   - Ensure that the number of IP addresses are reserved and maintained with respect to the number of hosts on the network.

+   - Ensure that the lease period of hosts is changed according to the situation such as a scheduled maintenance.

+   - Ensure that free IP addresses are available after a major change of all lease periods.

# Static Hosts

**Definition:**

A *static host* is a host that always receives the same IP address from the DHCP server. The server detects the static host using the `dhcp-client-identifier` or `hardware ethernet` option, which is sent by the host to the server. If the host does not send the `dhcp-client-identifier` information, the server identifies the static host using the NIC address of the host. Declaring static hosts on a network aids in the easy identification of systems because the IP address remains the same.

![](bbox=[0.77, 0.58, 0.85, 0.62])

Static Hosts