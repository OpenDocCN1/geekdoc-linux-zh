Web Server. Therefore, the sender will receive a message informing him or her that service is not available.

![](bbox=[0.05, 0.15, 0.95, 0.65])

Figure 11.7: Without NAT, the virtual machines can not be accessed.

With port mappings, you can build a configuration where the packets received for a specific port can be sent to the correct virtual machine when they are received on the host's 'outside' network adapter. In the previous example, configuring the NAT service to forward all incoming traffic at address 192.168.1.1 for port 80 to 192.168.244.128 effectively let's the PC on the local network communicate with the http service running on the virtual machine. The sender could think that the web server is at address 192.168.1.1, while it is actually on the virtual machine's address at 192.168.244.128

Figure 11.7 also shows the host-only network adapter for VMnet8. This adapter is being used by the host operating system to communicate with the guest operating system, in much the same way as you would normally use a host-only network.

To set up this configuration on a Windows host, click the Edit button on the NAT tab of the Virtual Network Editor. In the NAT Settings window, click the Port Forwarding button to define port mappings.

You can choose between TCP or UDP port mappings. Make sure to set up the correct type of traffic for your service. In the Port forwarding screen, click Add in the TCP or UDP chapter.