# on the Job

![](bbox=[0.38, 0.18, 0.87, 0.58])

Take care to avoid IP address conflicts with existing hardware on the local network, such as with routers and wireless access points. For example, at least one cable “modem” uses IP address 192.168.100.1 for maintenance. In that case, the noted 192.168.100.0/24 network would make that cable “modem” inaccessible. If you have such hardware, do change the network address shown in the illustration.

+   7. Now you can select the range of IP addresses within the configured network that can be assigned by a DHCP client. Per Chapter 1, Table 1-2, you'll configure a static IP address for the outsider1.example.org system on this network. As long as the noted 192.168.100.100 IP address is outside the range of DHCP-assignable IP addresses, no changes are required. Make any needed changes and click Forward to continue.
+   
+   8. Now you'll want a system that forwards network communication to the physical network, if only because that's how systems on this network communicate with systems on different virtual networks, possibly on different virtual hosts. The destination can be Any Physical Device, in NAT mode, to help hide these systems from remote hosts. Unless you want to limit routing from VMs to a specific physical network card, the defaults under Forwarding To Physical