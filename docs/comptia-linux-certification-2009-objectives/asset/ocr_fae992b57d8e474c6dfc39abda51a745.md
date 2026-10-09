| Parameter | Description | Example |
| :--- | :--- | :--- |
| range (first IP address of the range) (last IP address of the range); | Specifies the range of IP addresses to be dynamically allocated to computers on a subnet. | range 192.168.0.1 192.168.0.100; |
| max-lease-time time in seconds; | Specifies the maximum time, in seconds, for which an IP address can be leased to a client. | max-lease-time 1200; |
| default-lease time time in seconds; | Specifies the default time, in seconds, for which an IP address will be leased if a client does not request a specific lease time. | default-lease time 1200; |
| min-lease-time time in seconds; | Specifies the minimum time, in seconds, for which an IP address can be leased to a computer. | min-lease-time 1200; |
| hardware ethernet network interface address; | Identifies a computer on a network. | hardware ethernet 00:04:75:E9:3A:55; |
| fixed-address fixed IP address; | Specifies the static IP address that is to be assigned to a client. This IP address should be excluded from the range parameters specified in the dhcpd.conf file. | fixed-address 192.168.0.1; |
| option dhcp-client-identifier string or network interface address; | Identifies a client on a network. It is usually specified within a host declaration. | option dhcp-client-identifier "srvA"; |

# The DHCP Process

DHCP is a system-V service that handles client requests on a network and allocates IP addresses. The service gets activated on the system by installing the DHCP package. The DHCP process can be divided into a number of phases.

+   1. In the IP request phase, a client broadcasts the IP address request to the DHCP server.
2. In the IP release phase, the DHCP server receives the request and processes it. It responds to the request by sending the IP address, the subnet mask, the duration of lease, and the IP address of the DHCP server to the client.

![](bbox=[0.762, 0.76, 0.851, 0.82])