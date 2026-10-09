# Port Ranges

The Internet Assigned Numbers Authority (IANA), an international agency, separates port numbers into three blocks: well-known ports, which are preassigned to system processes; registered ports, which are available to user processes and are listed as a convenience; and dynamic ports, which are assigned by a client operating system when there is a request for service.

![](bbox=[0.78, 0.09, 0.92, 0.16])

| Block | Description |
| :--- | :--- |
| Well-known ports | Port range: 0 to 1,023. Well-known ports are pre-assigned for use by common, or well-known, services. Often the services that run on these ports must be started by a privileged user. Services in this range include HTTP on TCP port 80, IMAP on TCP port 143, and DNS on UDP port 53. |
| Registered ports | Port range: 1,024 to 49,151. These ports are registered by software makers for use by specific applications and services that are not as well known as the services in the well-known range. Services in the registered port range include SOCKS proxy on TCP port 1080, Kazaa peer-to-peer file sharing on TCP port 1214, and Xbox Live on TCP and UDP port 3074. |
| Dynamic or private ports | Port range: 49,152 to 65,535. These ports are set aside for use by unregistered services and by services that need a temporary connection. |

# Network Interfaces

*A network interface* is a point of connection between two systems. It can be implemented using hardware or software. There are different types of network interfaces.

![](bbox=[0.78, 0.57, 0.92, 0.64])

| Network Interface Type | Description |
| :--- | :--- |
| *Physical* | A physical network interface is implemented using a hardware device. |
|  | For example, an Ethernet interface (denoted by ethX, where X refers to the number of the interface) is set up using a Network Interface Card (NIC). |
| *Virtual* | A virtual network interface is implemented through software support. |
|  | For example, a loopback interface (*lo*) simulates a network interface without the help of a physical device. It is used to test network connectivity and accuracy of data transmission by sending data back to the generating source address. |