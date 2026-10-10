+   4. You are testing the connectivity to a server with an IP address 10.10.10.4.
+   You want to display a continuous output to the screen so that you can
+   see when the remote server is up. The correct command is
+   A. `ping -c 10.10.10.4`
+   B. `ping -v 10.10.10.4`
+   C. `ping -d 10.10.10.4`
+   D. `ping 10.10.10.4`

+   5. There has been a new system installed on your network that you do not
+   know about. You have performed a port scan and can see that port 80
+   and 22 are open. From your knowledge of the service ports, this is likely
+   to be which of the following:
+   A. a Web and FTP server
+   B. a Web and SSH server
+   C. a Web and Telnet server
+   D. a Web and mail server

+   6. You need to change the IP address of an NIC assigned eth0, which has
+   been assigned a static address to 10.10.100.45. This is installed in a
+   server in a small-company network. Which of the following will change
+   the IP address most effectively?
+   A. Change the /etc/hosts file to reflect the new IP address and reboot the
+   system.
+   B. Change the address in the routing table and force a reboot using the
+   command:
+   `/sbin/route add 10.10.100.45 netmask 255.255.255.0 dev eth0`
+   C. Use the `ifconfig` command to change the address:
+   `ifconfig eth0 10.10.100.45 netmask 255.255.255.0 up`
+   D. Change the IP address on the module using the following:
+   `/sbin/ifchange 10.10.100.45 netmask 255.255.255.0`

+   7. A user has a computer that does not use DHCP and he/she cannot use
+   hostnames in any command, although IP addresses do work. Where
+   would you look to see how the DN server is defined?
+   A. /etc/resolver.conv
+   B. /etc/resolv.conf
+   C. /etc/hosts
+   D. /etc/sysconfig/network