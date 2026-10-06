# Chapter 18 ✨ Running a Linux Firewall/Router 479

Enter tty device name for modem (ttySO, etc)[ttySO]: ttySO
Enter ttySO's port speed (115200, 57600, etc)[115200]: 115200
Enter modem init string (Enter = ATZ): ATZ
Enter name of ISP (no whitespace)[isp]: att
Enter phone number to dial: 5551212
ter username: jmsit
Enter password: tkn0st

+   12. Type n to not send clear-text passwords during login. You may need to change this to y if your ISP requires CHAP or PAP authentication.

If you enable this, your password will be sent in clear text over the line. Yes here only despite having verified everything, you still cannot connect to your ISP.
Login during chat? [y/n]: n

+   13. Because this firewall will provide IP addresses to the other computers on your LAN, it needs to be assigned a DHCP server (y). Then the range of addresses it can assign to those computers. If you plan to have 100 or fewer computers on your LAN, the address range in this example should work for you:

Do you want the coyote DHCP server? [y/n]: y
ter DHCP starting IP [192.168.0.100]: 192.168.0.100
Enter DHCP range ending IP [192.168.0.200]: 192.168.0.200

+   14. A DMZ is a way of further shielding your local network from the outside world if you want to have a Web server protected by the same firewall. In this case, you can add another Ethernet card to the firewall, connect that to the Web server, and then allow incoming requests for Web services to go through to the Web server. This enables you to block all incoming traffic to the desktop-systems on your LAN. I just choose N.

If you don't know what a DMZ is, just answer NO
Would you like to configure a De-Militarized Zone? [Y/N]: N

+   15. Set the domain name with this firewall is associated, and enter the IP address(es) of the DNS server(s) it will resolve addresses (probably provided by your ISP, unless you are running your own DNS server:

Enter Domain Name: example.com
Enter DNS Server 1: 123.45.68.799
Enter DNS Server 2 (optional): 123.45.68.800

If you have a syslog server on your LAN you want Coyote to send its syslog data to, you can specify the address here.
If unsure or not have a syslog server, leave this entry blank.