In Slackware, type **netconfig**. When you are finished, reboot and you should be up and running.

If this doesn’t work, make sure you do network card troubleshooting from the beginning of this document.

# Jones Intercable

This information was provided by Bob Kimble:

> Jones Internet Cable supplies a Hybri d cable modem that connects to your machine/network via 10 BaseT Ethernet. They provide you with a static IP address for your machine and another static IP address for the modem. The modem acts as a gateway to their network. Your IP address and the modem IP address are on the same network and have the same network mask (in my case 255.255.255.0 – 24 bits). They also provide two DNS IP addresses, which you enter into your configura- tion. I just entered the numbers when I installed Red Hat Linux 5 and it worked like a champ from the beginning. Since then I have configur- ed my Linux machine to enable IP masquerading and domain name ser- vices, and it now acts as a router for my entire private network. My other machines are connected via a private network using the addresses 192.168.0.x. They are running Windows 95, Windows NT (Intel and Alpha), and OS/2. My Linux machine has two IP addresses – the one from the cable company and one from the 192.168.0.x private network. Everything works like a champ. All six machines can browse the Web simultaneously. My kids are even able to connect to their favorite game site, The Realm from Sierra.

# GTE Worldwind

This information was provided by Mike Hughes:

> The information you provided for Rogers Wave works for GTE World- Wind cable modem services also. However, GTE’s service is extremely slow, barely faster than ISDN. More information at http://www .psi1ord.com.