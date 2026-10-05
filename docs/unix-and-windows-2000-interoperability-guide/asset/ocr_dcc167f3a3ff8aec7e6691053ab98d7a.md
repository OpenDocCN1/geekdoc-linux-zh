# Windows 2000 DHCP Server

![](bbox=[0.078, 0.121, 0.693, 0.613])

Figure 7-3 The DNS tab of the DHCP Manager. Open the Control Panel on the DHCP server, double-click on the DHCP icon, right-click on the server icon choose Properties. Then select the DNS tab.

# 7.2.1 DHCP/DNS Interoperability

7.2.1.1 HP-UX DHCP Client and Windows 2000 DHCP Server

On my test HP-UX 11 system, there was no problem making it a DHCP client of a Windows 2000 DHCP server. It received its IP address, domain name, and Network Information Service (NIS) domain successfully. However, the Windows 2000 DHCP server was unable to update the HP-UX client in DDNS (which ran on the same machine), and the client was not DDNS-aware. The HP-UX client supports neither Option 12 nor Option 81 and therefore has no way of informing the DHCP server of its host name.