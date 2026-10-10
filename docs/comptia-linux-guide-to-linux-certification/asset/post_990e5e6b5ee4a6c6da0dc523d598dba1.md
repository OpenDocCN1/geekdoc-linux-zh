
16. What directory are you placed in when you log in as the anonymous user to an Ubuntu Server 14.04 FTP server?
- a. /srv/ftp
- b. /var/www/ftp
- c. /home/anonymous
- d. /var/ftp/pub

17. ChronyD is an NTP daemon that offers a faster response time compared to the ntpd daemon. True or False?

18. Which SQL statement key word can be used to delete a record within a table?
- a. DELETE
- b. DROP
- c. REMOVE
- d. CLEAR

19. Which command can you use to synchronize ntpd with an NTP time source?
- a. ntp
- b. ntpquery
- c. ntpq
- d. hwclock

20. Mary is a system administrator in your organization. She has recently made changes to the DHCP configuration file, but the DHCP daemon does not seem to recognize the new changes. What should she do?
- a. Log in as the root user and recite the configuration file.
- b. Run the dhcpcronf command to edit the configuration file.
- c. Restart the DHCP daemon.
- d. Restart the inetd daemon.

## Hands-on Projects

![](img/c27875544958897d817484d558c208c8_641_0.png)

These projects should be completed in the order given. The hands-on projects presented in this chapter should take a total of three hours to complete. The requirements for this lab include:

- A computer with Fedora Linux installed according to Hands-on Project 2-1 and Ubuntu Server Linux installed according to Hands-on Project 6-1.

### Project 13-1

In this hands-on project, you configure the DHCP daemon on your Fedora Linux virtual machine and test your configuration by obtaining an IPv4 address from your Ubuntu Server Linux virtual machine.

1. Boot your Fedora Linux virtual machine. After your Linux system has been loaded, switch to a command-line terminal (tty2) by pressing Ctrl+Alt+F2 and log in to the terminal using the user name of root and the password of LNXRocks!.

2. At the command prompt, type `yum install dhcp` and press Enter to install the DHCP server daemon. Type `y` and press Enter when prompted to continue the installation.

3. Edit the `/etc/dhcp/dhcpd.conf` file with a text editor by adding the following lines:

   ```text
   default-lease-time 72000;
   option routers IP_address_of_your_class_default_gateway;
   option domain-name-servers IP_address_of_your_class_DNS_server;
   subnet class_network netmask subnet_mask {
     range class_network.50 class_network.100;
   }
   ```

   For example, if your class uses the 192.168.1 network (subnet mask 255.255.255.0) and a default gateway and DNS server of 192.168.1.254, you would add the following lines:

   ```text
   default-lease-time 72000;
   option routers 192.168.1.254;
   option domain-name-servers 192.168.1.254;
   subnet 192.168.1.0 netmask 255.255.255.0 {
     range 192.168.1.50 192.168.1.100;
   }
   ```

   When finished, save your changes and quit the editor.

4. At the command prompt, type `useradd -m dhcpd` and press Enter to create a dhcpd user account for the DHCP daemon.

5. At the command prompt, type `systemctl start dhcpd.service` and press Enter to start the DHCP daemon.

6. At the command prompt, type `ps -ef | grep dhcpd` and press Enter to ensure that the DHCP daemon has loaded successfully. If the DHCP daemon is not listed, check for errors in your `/etc/dhcp/dhcpd.conf` file and repeat the previous step.

7. At the command prompt, type `firewall-cmd --add-service dhcp` and press Enter to allow DHCP traffic through the firewall on your Fedora Linux virtual machine.

8. In your virtualization software, disable the virtual DHCP server used for your Ubuntu Server Linux virtual machine. Next, boot your Ubuntu Server Linux virtual machine and log into tty1 using the user name of root and the password of LNXRocks!.

9. At the command prompt on your Ubuntu Server Linux virtual machine, type `dhclient eth0` and press Enter to request a DHCP address.

10. At the command prompt on your Fedora Linux virtual machine, type `cat /var/lib/dhcp/dhcpd.leases` and press Enter. Note the line that details the lease information.

11. At the command prompt on your Fedora Linux virtual machine, type `systemctl stop dhcpd.service` and press Enter to stop the DHCP daemon.

12. At the command prompt on your Fedora Linux virtual machine, type `exit` and press **Enter** to log out of your shell.

13. At the command prompt on your Ubuntu Server Linux virtual machine, type `poweroff` and press **Enter** to shut down the system. Next, enable the virtual DHCP server used for your Ubuntu Server Linux virtual machine within your virtualization software.

### Project 13-2

In this hands-on project, you configure and test the DNS daemon on your Fedora Linux virtual machine.

1. On your Fedora Linux virtual machine, switch to a command-line terminal (tty2) by pressing **Ctrl+Alt+F2** and log in to the terminal using the user name of `root` and the password of `LNXRocks!`.

2. At the command prompt, type `yum install system-config-bind` and press **Enter** to install the graphical BIND configuration utility, which also installs the dependency package `BIND` (the named daemon). Type `y` and press **Enter** when prompted to continue the installation.

3. Switch to a graphical terminal by pressing **Ctrl+Alt+F1** and log in to the GNOME desktop with the user name `user1` and the password of `LNXRocks!`. Next, open a command-line terminal (**Activities** menu, **Show Applications**, **Utilities**, **Terminal**).

4. At the command prompt, type `su - root` and press **Enter**. Supply the password of `LNXRocks!` and press **Enter** when prompted to switch to the root user.

5. At the command prompt, type `system-config-bind` and press **Enter** to start the BIND configuration GUI program.

6. Highlight **DNS Server** and click **Properties**. Add the **forwarders** option to the Current Options box. In the New List Element section, highlight **IPv4 Address** and supply the IPv4 address of your classroom DNS server for this option and click **OK** when finished. Click **OK** to close the DNS server property window. This configures your DNS server to forward requests to the classroom DNS server if it cannot resolve the destination address using the information within its own zone files.

7. Click **New, Zone** and accept the default zone scope of **Internet** by clicking **OK** underneath the Class drop-down box. Next, accept the default zone type of **Forward** by clicking **OK** below the Origin Type drop-down box and type the zone name `class.com` (taking care to include the trailing `.` in the zone name). Accept the default DNS server zone role of **master** by clicking **OK**.

8. Examine the default `SOA` record parameters. What is the default minimum `TTL`? Briefly explain what this setting does. Click **OK** to return to the BIND configuration utility window.

9. Expand your `class.com` zone. What default records are created in this new zone?

10. Highlight the `class.com` zone and click **New, A IPv4 Address**. Type `gateway.class.com.` in the Domain Name dialog box (taking care to include the trailing `.` in the FQDN) and supply the IPv4 address of your classroom’s default gateway. Click **OK** to create the `A` record.

11. Highlight the `class.com` zone and click **New, A IPv4 Address**. Type `server1.class.com.` in the Domain Name dialog box (taking care to include the trailing `.` in the FQDN) and supply your computer’s IPv4 address. Click **OK** to create the `A` record.

12. Highlight the `class.com` zone and click **New, CNAME Alias**. Type `alias.class.com.` in the Domain Name dialog box, and type `server1.class.com.` in the Canonical Name dialog box (taking care to include the trailing `.` in both FQDNs). Click **OK** to create the `CNAME` record.

13. Highlight the `class.com` zone and click **New, MX Mail Exchange**. Note the default domain of `class.com.` in the Domain Name dialog box and type `server1.class.com.` in the Mail Server Name dialog box (taking care to include the trailing `.` in the FQDN). Click **OK** to create the `MX` record.

14. Expand your `class.com` zone. Are the new records visible?

15. Expand the zone that represents your classroom network. Are PTR records available for reverse lookups?

16. Click **Save**. Click **OK** when prompted to save your changes to the configuration files on the hard drive.

17. Close the BIND configuration utility, log out of the GNOME desktop environment, and switch back to tty2 by pressing Ctrl+Alt+F2.

18. At the command prompt, type `systemctl start named.service` and press Enter to start the DNS name daemon.

19. Edit the `/etc/resolv.conf` file with a text editor and remove any existing `nameserver` lines. Add the line `nameserver 127.0.0.1` to ensure that your Linux computer uses the local DNS server daemon for name resolution. Save your changes and quit the editor when finished.

20. At the command prompt, type `ping -c 4 gateway.class.com` and press Enter. Was the name resolved successfully? Explain.

21. At the command prompt, type `ping -c 4 server1.class.com` and press Enter. Was the name resolved successfully? Explain.

22. At the command prompt, type `ping -c 4 alias.class.com` and press Enter. Was the name resolved successfully? Explain.

23. At the command prompt, type `ping -c 4 www.yahoo.com` and press Enter. Was the name resolved successfully? Explain.

24. At the command prompt, type `dig @localhost class.com ANY` and press Enter. Are your resource records returned successfully?

25. At the command prompt, type `less /etc/named.conf` and press Enter. View the entries. Is `class.com` a Master zone? Do you see a line that forwards unknown requests to your classroom DNS server? Press `q` when finished.

26. At the command prompt, type `cat /var/named/class.com.db` and press Enter. View the entries. Are your resource records present?

27. At the command prompt, type `cat /var/named/network_ID.db` and press Enter where `network_ID` is your classroom network ID. View the entries. Are PTR resource records present?

28. At the command prompt, type `less /var/named/named.ca` and press Enter. View the entries. What do these entries represent?

29. Type `exit` and press Enter to log out of your shell.

![](img/c27875544958897d817484d558c208c8_644_0.png)
