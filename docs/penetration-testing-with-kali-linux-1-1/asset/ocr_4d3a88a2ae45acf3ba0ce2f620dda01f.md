We can validate that this is working by starting Wireshark to sniff the traffic, and verify it is being HTTP- encapsulated, before initiating a remote desktop connection against our Kali Linux machine’s listening port 8080:

![](bbox=[0.17, 0.16, 0.83, 0.48])

*Figure 305: RDP login on the Windows Server 2016 machine through the HTTP tunnel*

Excellent! The remote desktop connection was successful.

Inspecting the traffic in Wireshark, we confirm that it is indeed HTTP- encapsulated, and would have bypassed the deep packet content inspection device.