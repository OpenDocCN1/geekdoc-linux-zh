but Microsoft clients would normally use port 80, which is not included.

+   9. In your DHCP server, you wish to allocate a fixed IP address to one of your color laser printers. What do you need to do to set this up?

+   A. Find the IP address the printer is currently assigned and fix it using the dhcpcd fix IPaddress command on your DHCP server.

+   B. Ensure bootp is available on the printer and then assign an IP address to this in the dhcpd.conf file with the host parameter.

+   C. Find the printers' MAC address and a spare IP address from the pool of IP addresses defined on your DHCP server and set this up in the dhcpd.conf file with the host parameter.

+   D. Set a fixed IP address directly on the printer and allow this to broadcast it to the DHCP server upon the printer being started.

Correct answer and explanation: C. Answer C is correct as you can set a fixed IP address against a specific MAC address using the host option.

Incorrect answers and explanations: A, B, and D. Answer A is incorrect as there is no command option to dhcpcd to fix the IP address. Answer B is incorrect as bootp is a program that will ask the DHCP server for an IP address. The DHCP server needs to know this is a fixed IP address and this has to be set up with the host option. Answer D is incorrect as this may cause an IP address conflict as the DHCP server has not allocated a fixed IP address to this and may issue that IP address to another client.

+   10. Your new Apache Web server has been set up and one of the developers wants to know which directory to load the Web pages. How can you find out which directory this is?

+   A. Look in the httpd.conf file for a WebRoot directive

+   B. Look in the httpd.conf file for a DocumentRoot directive

+   C. Look in the httpd.conf file for a ServerName directive

+   D. Look in the httpd.conf file for a WebBase directive

Correct answer and explanation: B. Answer B is correct as the DocumentRoot parameter correctly defines the root directory where the Web pages are stored.

Incorrect answers and explanations: A, C, and D. Answer A is incorrect as there is no WebRoot parameter. Answer C is incorrect as the ServerName parameter defines the name of the Web site. Answer D is incorrect because, again, there is no WebBase directive.