| Type of Allocation | Description |
| :--- | :--- |
| Manual | To allocate IP addresses manually, the administrator has to visit each host. Hosts can be either workstations or servers. Smaller organizations that have plenty of IP addresses for workstations and servers often use this method. When IP address assignments need to change, this method requires higher maintenance by the administrator. |
| Automatic | By using automatic allocation, the DHCP server assigns a permanent IP address to the host. The administrator need not visit each system. While this method reduces the amount of administrative time, it does require an adequate supply of IP addresses. |
| Dynamic | By using dynamic allocation, the DHCP server assigns a temporary IP address to the host. The administrator need not assign the IP addresses, and a limited number of IP addresses serves a larger organization. When a workstation boots, it requests an IP address from the DHCP server along with other information, such as the DNS server IP address, the gateway IP address, and the subnet mask. The DHCP server takes an address from a pool of IP addresses and gives it to the workstation to use temporarily. The administrator can configure how long the address is leased. |

![](bbox=[0.03, 0.62, 0.11, 0.68])

# The dhcpd.conf File

# Definition:

The *dhcpd.conf* file is used to configure the DHCP server. To make changes on a Linux DHCP server, the *dhcpd.conf* file can be edited. By default, the file is located in the /etc directory, but the location of the file can be changed. Any changes made in the *dhcpd.conf* file will not take effect until the DHCP daemon is restarted. The *dhcpd.conf* file contains two types of statements: parameters and declarations. It also includes the *shared-network*, *subnet*, *host*, and *group* declarations.

> Usually, the *dhcpd.conf* file is created as an empty file when you install DHCP from the RPM package. However, you can copy the source content from a sample *dhcpd.conf* file, which is located in the /usr/share/doc/dhcp-<version-number>/etc directory. After copying the content, you can edit it according to your requirements.