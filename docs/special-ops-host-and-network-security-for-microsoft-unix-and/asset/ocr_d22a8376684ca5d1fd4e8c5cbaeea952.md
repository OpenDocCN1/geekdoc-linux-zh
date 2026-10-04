# Network Architecture • Chapter 16 857

```
12/10/02 07:32:48 tcp johnbock.bhome.com.2508 -> intranet.bhome.com.21
(ftp)
```

```
USER jbock
PASS j0hnlik3$gun$
```

```
12/10/02 07:55:33 udp 10.10.12.7.1998 -> 10.10.129.161 (snmp)
[version 1]
public
```

I have cut much out of boring network traffic to highlight how powerful DSniff can. Within an hour, I was able to capture several HTTP, POP, FTP, and SNMP passwords, as shown in the preceding listing. This information can be easily used to compromise servers and workstations across your network. This helps to show powerful information that can be gathered from a simple MAC flooding attack.

# Defending Against MAC Flooding

Since MAC flooding convinces that all of the MAC addresses for a particular subnet are located on a single port, the easy defense for that utilizes port security. Port security for this exploit means allowing the switch to associate or learn only a particular number of MAC addresses for a specific port. In other words, you could limit the switch to learn only one MAC address per port. This would mean that only one computer could be connected to a specific port, disabling the capability for DSniff to incorrectly fill the CAM table with erroneous entries. Furthermore, depending on the vendor implementation, a port may be able to shut down if a large number of MAC addresses are requesting entry into the port (like how DSniff would work).

The downside to this security measure is that you would have to be cautious of how many computers or devices reside on a specific port. In our example, we said that only one MAC address could be present on the port. If we add another switch or hub to that port, and connect multiple computers, the port might shut down since you have more MAC addresses present on the port than the permitted one address. In order to accommodate this, you would have to change the security on the port to allow more than one MAC address. It is easy to see the administrative overhead that would occur, but this is relatively easy solution for such a severe problem.

![](bbox=[0.706, 0.943, 0.928, 0.966])