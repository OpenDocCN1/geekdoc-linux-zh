# Project 12-1

In this hands-on project, you view and modify the TCP/IP configuration of the network interface on your Fedora Linux and Ubuntu Server Linux virtual machines.

+   1. Boot your Fedora Linux virtual machine. After your Linux system has been loaded, log into the GNOME desktop using the user name of user1 and the password of LNXrocks!.  
+   2. Navigate to the Activities menu, Show Applications, Settings and click Network. Note the IPv4 and IPv6 configuration for your Wired network interface.  
+   3. Next, click the cog wheel icon in the lower-right corner and highlight IPv4 in the left pane. Click the drop-down box next to Addresses and select Manual. Supply the IP address, netmask, default gateway, and DNS server information shown in the previous step and click Apply.  
+   4. Switch to a command-line terminal (tty2) by pressing Ctrl+Alt+F2 and log in to the terminal using the user name of root and the password of LNXrocks!.  
+   5. At the command prompt, type ifconfig and press Enter. What IPv4 and IPv6 configuration do you see?

![](bbox=[0.15, 0.43, 0.36, 0.51])

The steps within the hands-on projects in this chapter assume that your first network interface is called eth0. If your network interface has a different name, use it in place of eth0 in any steps.

+   6. At the command prompt, type cat /etc/sysconfig/network-scripts/ifcfg-eth0 and press Enter. Is your configuration listed?  
+   7. Switch back to your graphical terminal (tty1) pressing Ctrl+Alt+F1. In the Network utility, click the cog wheel icon in the lower-right corner and highlight IPv4 in the left pane. Click the drop-down box next to Addresses, select Automatic (DHCP), and click Apply.  
+   8. Close the Network utility and log out of the GNOME desktop.  
+   9. Switch back to tty2 by pressing Ctrl+Alt+F2.  
+   10. At the command prompt, type cat /etc/sysconfig/network-scripts/ifcfg-eth0 and press Enter. What is the BOOTPROTO line equal to? Will the static IP configuration listed in this file be used?  
+   11. At the command prompt, type ifdown eth0 and press Enter. Next, type ifconfig at the command prompt and press Enter. Is eth0 listed?  
+   12. At the command prompt, type ipup ls and press Enter. Did the command probe for a DHCP server? Next, type ifconfig at the command prompt and press Enter. Is eth0 listed?  
+   13. At the command prompt, type ping interfaceIP and press Enter, where interfaceIP is the IPv4 address of eth0. Do you receive ping responses from your network interface? Press Ctrl+c when finished to quit the ping command.  
+   14. At the command prompt, type netstat -i and press Enter. View the statistics for your network interfaces. If necessary, consult the netstat manual page to determine the meaning of each column displayed.