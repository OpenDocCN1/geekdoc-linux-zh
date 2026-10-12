+   if you are traveling with a laptop and want to plug in to the network at the site you are visiting, you have to configure all your IP settings. (Even finding someone who can tell you which settings to use can be a big job.) From the site administrator's point of view, transient users are hard to manage: they have to be be allocated an IP number when they arrive, and the number has to be de-allocated when they leave

+   network settings also have to be changed:
+   
+   - when you first connect your site's LAN to the Internet, if you weren't already using legal addresses specifically allocated to your organization. Most sites get their legal addresses only when they join the Internet, so this is a common occurrence
+   - if you alter your network to use Network Address Translation (NAT, Module 23.2) instead of public IP addresses
+   - when you change to a new ISP, because your public IP addresses are normally allocated to you by your ISP
+   - when you add extra services to your network. For example, if you install a second DNS server for reliability, you have to add these extra DNS server details to every host on your network. Or, if you are using Microsoft Windows Networking, and decide to use a WINS server (Chapter 19), you must configure all Windows hosts with the IP address of the WINS server

DHCP and dynamic addresses overcome all these problems

+   diskless machines must of necessity obtain all their configuration parameters from elsewhere, as they cannot store them locally. This was important when graphical workstations first came on to the market; disks were very expensive and running diskless workstations was a cost-effective way to implement a distributed network. Diskless operation remains necessary for thin-client devices such as Windows terminals (for Windows NT Server Terminal Edition) and X windows system (Module 17.6) terminals.

DHCP servers are now deployed very widely. In fact they are built as standard into many network devices such as firewalls, leased-line and ISDN routers, etc.

ISPs also need to allocate IP addresses dynamically to users connecting via dial-up modems, dial-up ISDN or ADSL connections. This is important because the Internet is running out of public IP addresses and there just aren't enough IP addresses to give every dial-up user a permanent address specific to themselves. However, because only a small proportion of an ISP's dial-up users are connected at any one time, the ISP can share a small number of IP addresses amongst a much larger number of users, by allocating addresses dynamically each time a dial-up user connects. While this may not involve DHCP, in Module 16.6 we outline how ISPs allocate IP addresses dynamically.

In the next module we explain in detail how the DHCP client and server interact.