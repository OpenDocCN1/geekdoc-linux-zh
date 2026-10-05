# SOLUTION

# MANAGING NETWORKS

In this review, you will configure and test network connectivity.

# OUTCOMES

You should be able to:

+   - Configure the network settings.

+   - Test network connectivity.

+   - Set a static host name for the system.

+   - Use locally resolvable canonical host names to connect to systems.

# BEFORE YOU BEGIN

Log in to workstation as student using student as the password.

On workstation, run lab rhcsa-rh124-review4 to start the comprehensive review. This script creates the necessary files to set up the environment correctly.

```
$student@workstation~$ lab rhcsa-rh124-review4
```

# INSTRUCTIONS

Accomplish the following tasks on server of the Ethernet interface and its active connection profile on server.

+   - Determine the name of the Ethernet interface

+   - On server, create a new connection profile called static for the available Ethernet interface that locally sets network settings and does not use DHCP. It should be based on the settings in the table below.

| IPv4 address | 172.25.250.111 |
| Netmask | 255.255.255.0 |
| Gateway | 172.25.250.254 |
| DNS server | 172.25.250.254 |

Set the server's Ethernet interface to use the updated network settings displayed in the table above.

+   - Ensure that the name of server is statically set to server - review4.lab.example.com.

+   - On server, set client-review4 as the canonical host name for the IPv4 address 172.25.250.10 of the servera.lab.example.com.