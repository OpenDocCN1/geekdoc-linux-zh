# UNIX SYSTEM MANAGEMENT PRIMER PLUS

# Network Monitoring

At some point in their careers, system administrators must put on their network engineer hats. Some people are quite skilled at network design and router configuration, while some are network neophytes, skilled at system administration but clueless when confronted with a failing T1 circuit (a circuit is just another name for a network connection). At the very least, a system administrator should understand the networks that connect machines within the Unix system for which they are responsible and monitor the availability of those networks.

In Chapter 4, "Testing Your Systems," you learned about system testing using the example of Nearest Integer Bank; here, the same example illustrates the system monitoring process. Figure 6.1 shows a logical network diagram of a small part of Nearest Integer's network.

FIGURE 6.1
Logical diagram of
Nearest Integer Bank's
Web server and customer
service networks.

![](bbox=[0.318, 0.316, 0.933, 0.563])

The network portion depicted in the diagram includes four separate networks:

+   - The online services network (192.168.1.0/24)
- The customer service network (192.168.2.0/24)
- The New York database center (192.168.3.0/24)
- The San Francisco database center (192.168.4.0/24)

This portion of the network also includes two T1 circuits (1.544Mbps) and one DS3 circuit (45Mbps), each of which must be monitored. When monitoring a network circuit, two metrics to look at are the link status and bandwidth. You can monitor these metrics either at a router or firewall's console, or remotely via SNMP Network errors are also important to watch, using the tools in the following sections. Network errors are discussed in more detail in Chapter 11.