To allow Web browsing and basic network setup, DNS replies and DHCP (to serve addresses) are allowed at this level.

+   • **Medium** — Select this security level if you want to block access to ports used to offer most basic TCP/IP services (standard, reserved ports lower than 1023). This selection denies access to ports used for NFS servers, remote X clients, and the X font server. Those services are available primarily to other computers your own local LAN.

+   • **No firewall** — Select this security level if you are not connected to a public network and do not want to deny requests for services from any computer on your local network. Of course, you can still restrict access to services by starting up only the services you want to offer and by using configuration files to restrict access to individual services.

If you know you want to allow access to particular services, you can click Customize and allow incoming requests for the following: DHCP, SSH, Telnet, WWW, Mail, and/or FTP services. You can also add a comma-separated list of port numbers to the Other Ports box to open access to those ports. (The /etc/services file lists which services are associated with which port numbers.)

If you have a LAN that consists of trusted computers, you can click the box representing your interface to that LAN (probably eth0). Clicking the box allows access to any services you care to share with the computers on your LAN.

> TIP: Adding firewall rules here results in rules being added to the /etc/sysconfig/iptables file. The rules are run from the /etc/init.d/iptables start-up script when you boot your system. To make permanent changes to your firewall rules, you can use the Configure Firewalling window, as described in Chapter 14.

+   17. **Choose language support.** Your installation language should be selected automatically as your default language on this screen. You can select to install support for additional languages by clicking the check boxes next to the languages you want. You can click the Select All button to install all supported languages to your system.

+   18. **Choose a time zone.** Select the time zone from the list of time zones shown. Either click a spot on the map or choose from the scrolling list. To see a more specific view of your location, click World and choose your continent. From the UTC Offset tab, you can choose a time zone according to the number of hours away from Greenwich Mean Time (GMT), known as the UTC offset.

+   19. **Set root password.** You must choose a password for your root user at this point. The root password provides complete control of your Red Hat Linux system. Without it, and before you add other users, you will have no access to your own system. Enter the Root Password, and then type it again in the Confirm box to confirm it. (Remember the root user’s password and keep it confidential! Don’t lose it!) Click Next to continue.