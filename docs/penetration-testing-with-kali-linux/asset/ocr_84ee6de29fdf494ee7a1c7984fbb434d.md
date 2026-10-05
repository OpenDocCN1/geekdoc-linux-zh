# OffSec

Penetration Testing with Kali Linux

Figure 263: The high-level DNS request flow, with MULTISERVER3 configured as the DNS resolver

It's common to use the recursive resolver provided by an ISP (which is usually pre-programmed into the stock ISP router), but other well-known public recursive name servers950 can be used. For example, Google has a public DNS server at 8.8.8.8.

Lets try this out in a new scenario in the lab, which is configured precisely for this purpose. In this scenario, we have FELINEAUTHORITY. This alongside our Kali machine. This means that MULTISERVER3, CONFLUENCE01, and our Kali machine route to it, but DATABASE01 and HRSHARES cannot.

FELINEAUTHORITY is registered within this network as the authoritative name server for the feline.corp zone951 We will use it to observe how DNS packets reach an authoritative name server. In particular, we will watch DNS packets being exchanged between PGDATABASE01 and FELINEAUTHORITY.

While PGDATABASE01 cannot connect directly to FELINEAUTHORITY, it can connect to MULTISERVER3. MULTISERVER3 is also configured as the DNS resolver server for PGDATABASE01.

![](bbox=[0.125, 0.473, 0.875, 0.706])

Figure 264: The network layout for our DNS experiments

In the real world, we will have the feline.corp domain name ourselves, set up the authoritative name server machine ourselves, and tell the domain registrar that this server should be known as the authoritative name server for

950 (Wikipedia, 2022), https://en.wikipedia.org/wiki/Public_recursive_name_server
951 (Wikipedia, 2022), https://en.wikipedia.org/wiki/DNS_zone

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

623