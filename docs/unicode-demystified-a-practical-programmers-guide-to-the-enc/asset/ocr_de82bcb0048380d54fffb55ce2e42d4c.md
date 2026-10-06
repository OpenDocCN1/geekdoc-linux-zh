The stops takes data are much quicker than those you would make in the car, but each message leaves each router on a path chosen on the most current information. Think of it as a GPS (global positioning system) setup that automatically gets updates at each intersection and tells you where to go, based on traffic and highway conditions.

9-1 shows an example of how LANs might be set up at three sites connected by a WAN (the Internet). In network diagrams such as this, Ethernet LANs are drawn as straight lines, with devices attached at right angles; WANs are represented as clouds, indicating that the details have been left out; wireless connections are drawn as zigzag with breaks, indicating that the connection may be intermittent.

In 9-1 a gateway or a router relays messages between each LAN and the Internet. Three of the routers in the Internet are shown (for, the one closest to each). Site A has a server, a workstation, a network computer, and a PC sharing a single Ethernet LAN. Site B has an Ethernet LAN that serves a printer and four GNU/Linux workstations. A firewall permits only traffic between the Internet router and the site router. Site C has three LANs linked by a single router, perhaps to reduce the load that would result if they were combined or keep workgroups or locations on separate networks. Site C includes a wireless access point that enables wireless communication with nearby computers.

# Firewall

A firewall in a car separates the engine compartment from the passenger compartment, protecting the driver and passengers from engine fires, noise, and fumes. Computer firewalls separate computers from malicious and unwanted users.

A firewall prevents certain types of traffic from entering or leaving a network. A firewall might prevent traffic from your IP address from leaving the network and prevent anyone except users from select domains from using tip to retrieve data from the network. The implementations of firewalls vary widely, from GNU/Linux machines with two interfaces running custom software to a router (page 1473) with simple access lists to esoteric, vendor-supplied firewall appliances. Most larger installations (page 1490) at least one kind of firewall in place. A firewall is often accompanied by a proxy server/gateway (page 397) to provide an intermediate point between you and the host you are communicating with.

In addition to those found in multipurpose computers, firewalls are becoming increasingly common in consumer appliances. Firewalls are built into cable 요즘, wireless gateways, routers, and stand-alone devices.

When your need for privacy is critical, you can meet with a consulting firm that will discuss your security needs, devise a strategy, produce a written implementation