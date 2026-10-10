+   ▶ 16 B Class Network Addresses 172.16.0.0\~172.31.0.0 (netmask 255.255.0.0)
+   
+   ▶ 256 C Class Network Addresses 192.168.0.0\~192.168.255.0 (netmask 255.255.255.0)

If you have a LAN for which you have *not* been allocated IP numbers by the responsible authority in your country, you should use one of the network numbers from the above sequences for your machines.

These numbers should *never* be used on the Internet.

However, they can be used for the local Ethernet on a machine that is connected to the Internet. This is because IP numbers are actually allocated to a network interface, not to a computer. So while your Ethernet interface may use 10.0.0.1 (for example), when you hook onto the Internet using PPP, your PPP interface will be given another (and valid) IP number by the server. Your PC will have Internet connectivity, but the other computers on your LAN will not.

However, using Linux and the IP Masquerade (also known as NAT\[Network Address Translation\]) capabilities of Linux and the ipfwadm software, you can connect your LAN to the Internet (with some restriction of services), even if you do not have valid IP numbers for the machines on your Ethernet.

For more information on how to do this see the IP Masquerade mini-HOWTO at Linux IP Masquerade mini HOWTO (see http://Metalab.unc.edu/mdw/HOWTO/mini/IP-Masquerade).

For most users, who are connecting a single machine to an Internet service provider via PPP, obtaining an IP number (or more accurately, a network number) will not be necessary.

If you wish to connect a small LAN to the Internet, many Internet Service Providers (ISPs) can provide you with a dedicated subnet (a specific sequence of IP numbers) from their existing IP address space. Alternatively, use IP Masquerading.

For users, who are connecting a single PC to the Internet via an ISP, most providers use *dynamic* IP number assigning. That is, as part of the connection process, the PPP service you contact will tell your machine what IP number to use for the PPP interface during the current session. This number will not be the same every time you connect to your ISP.

With dynamic IP numbers, you are *not* given the same IP number each time you connect. This has implications for server-type applications on your Linux machine such as *Sendmail*, *ftpd*, *httpd* and so forth. These services are based on the premise that the computer offering the service