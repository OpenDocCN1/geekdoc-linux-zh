> "Now configure the Windows workstation. Change Network Neighborhood properties to the following:"

+   - Identification Tab to the new workgroup (csd28)
+   - Access Control to Share level access control
+   - Client for Microsoft Networks properties to new workgroup (csd28)
+   - TCP/IP properties
+     IP Number: 192.168.3.10 (Initially, any static number)
+     DNS Configuration:
+     Domain: mtc.net
+     Host:
+     DNS Search Order: Initially Disabled Later added 192.168.3.15 (MTC proxy server, it was the ESD server)
+     Gateway: 198.236.3.1
+   - Turn on File & print sharing
+   - Add to the end of the c:/Windows/LM Hosts file 192.168.3.15 CSD28 (ip & workgroup)
+   - Reboot"

The Bynari approach uses gradients to teach the administrators how to configure any service. In the beginning of the samba process, the Centennial team only performed one function. They created a user called "guest" and added the user to both the Linux password file and the smbpasswd file. They also configured a Windows 98 system to log on to the Samba server. They added the Windows information to the Linux "hosts" file and made entries to the smb.conf.

Once the team experienced success with a simple guest share, they added functionality until the test LAN had domain authentication, Dynamic Host Configuration Protocol (DHCP), mail, and the ability to browse the Internet through a Linux firewall.

# Back to Samba

Samba 2.0 introduced a program to assist in setting up and administering Samba via a Web browser. People know the program as SWAT, for Samba Web Administration Tool. With Centennial's scarce resources, the technical department needed a simple way to provide administration for Microsoft workstations. Red Hat 6.0 provides SWAT on its distribution.