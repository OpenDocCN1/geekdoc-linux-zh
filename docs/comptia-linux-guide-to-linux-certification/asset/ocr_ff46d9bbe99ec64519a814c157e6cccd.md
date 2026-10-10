+   1. Boot your Fedora Linux virtual machine. After your Linux system has been loaded, switch to a command-line terminal (tty2) by pressing Ctrl+Alt+F2 and log in to the terminal using the user name of root and the password of LN XRocks!.

+   2. At the command prompt, type yum install dhcp and press Enter to install the DHCP server daemon. Type y and press Enter when prompted to continue the installation.

+   3. Edit the /etc/dhcp/dhcpd.conf file with a text editor by adding the following lines:
+   
+   default-lease-time 72000;
+   option routers IP_address_of_your_class_default_gateway;
+   option domain-name-servers IP_address_of_your_class_DNS_server;
+   subnet class_network netmask subnet_mask {
+     range class_network.50 class_network.100;
+   }
+   
+   For example, if your class uses the 192.168.1 network (subnet mask 255.255.255.0) and a default gateway and DNS server of 192.168.1.254, you would add the following lines:
+   
+   default-lease-time 72000;
+   option routers 192.168.1.254;
+   option domain-name-servers 192.168.1.254;
+   subnet 192.168.1.0 netmask 255.255.255.0 {
+     range 192.168.1.50 192.168.1.100;
+   }
+   
+   When finished, save your changes and quit the editor.

+   4. At the command prompt, type useradd -m dhcpd and press Enter to create a dhcpd user account for the DHCP daemon.

+   5. At the command prompt, type systemctl start dhcpd.service and press Enter to start the DHCP daemon.

+   6. At the command prompt, type ps -ef | grep dhcpd and press Enter to ensure that the DHCP daemon has loaded successfully. If the DHCP daemon is not listed, check for errors in your /etc/dhcp/dhcpd.conf file and repeat the previous step.

+   7. At the command prompt, type firewall-cmd --add-service dhcp and press Enter to allow DHCP traffic through the firewall on your Fedora Linux virtual machine.

+   8. In your virtualization software, disable the virtual DHCP server used for your Ubuntu Server Linux virtual machine. Next, boot your Ubuntu Server Linux virtual machine and log into tty1 using the user name of root and the password of LNXRocks!.

+   9. At the command prompt on your Ubuntu Server Linux virtual machine, type dhclient eth0 and press Enter to request a DHCP address.

+   10. At the command prompt on your Fedora Linux virtual machine, type cat /var/lib/dhcp/dhcpd.leases and press Enter. Note the line that details the lease information.

+   11. At the command prompt on your Fedora Linux virtual machine, type systemctl stop dhcpd.service and press Enter to stop the DHCP daemon.