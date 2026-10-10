
Correct answer and explanation: **A.** Answer **A** is correct as the apachectl script correctly starts the server with the right environment variables.

Incorrect answers and explanations: **B**, **C**, and **D.** Answer **B** is incorrect as there is not an apacheweb script. Answer **C** is incorrect as the *apache* command does not exist. Answer **D** is incorrect as although this command would start the server, it is not recommended to do so. The best method is **A**, which will call the *httpd* command correctly.

5. Your company has installed a MySQL server on your network. You have used tracroute to confirm that you have network connectivity to that server. Which port would your client program use to connect to the MySQL server?

- **A.** TCP port 631
- **B.** UDP port 3306
- **C.** TCP port 3306
- **D.** TCP port 631 and UDP port 3306

Correct answer and explanation: **C.** Answer **C** is correct as the default port to connect to a MySQL server is TCP 3306/3306.

Incorrect answers and explanations: **A**, **B**, and **D.** Answer **A** is incorrect as port 631 is associated with the CUPS management interface. Answer **B** is incorrect as MySQL needs TCP port 3306 and not UDP port 3306. Answer **D** is incorrect as port 631 is used by CUPS and MySQL does not connect on UDP port 3306.

6. You are administrating a Samba server on your network. You want each user to connect to his/her own home directory. What configuration changes would you need?

- **A.** Add the line *valid users = %S* in the smb.conf file
- **B.** Add the line *browseable = yes* in the smb.conf file
- **C.** Add the line *home = %S* in the smb.conf file
- **D.** Add the line *path = ~* in the smb.conf file

Correct answer and explanation: **A.** Answer **A** is correct as setting this will allow users to connect to their home directory \\servername\username. It will require other parameters to allow these directories to be writable as well.

Incorrect answers and explanations: **B**, **C**, and **D.** Answer **B** is incorrect as this sets the home directories to be browseable and does not connect the users to their own directory. Answer **C** is incorrect as this is not a valid parameter. Answer **D** is incorrect as this sets the path name when shares are being defined.

7. You have just added a DHCP server onto your network to reduce the network administration tasks you have. Before you turn on DHCP on each of the clients, you want to test the connection. Which is the best command to achieve this?

- **A.** `dhcpd`
- **B.** `bootp`
- **C.** `dhcpcd`
- **D.** `pumpd`

Correct answer and explanation: **C.** Answer **C** is correct as this will request an IP address from the DHCP server.

Incorrect answers and explanations: **A**, **B**, and **D.** Answer **A** is incorrect as although it looks like it should be the *dhcp* daemon command, the right syntax is `dhcpcd`. Answer **B** is incorrect as this is usually run at boot time to allocate an IP address. It is often used with windowless devices. Answer **D** is incorrect, as this is not a valid command. The correct command should have been `pump`.

8. You want to install a proxy server in your network and have chosen the Squid proxy. You have a mixed network of Linux, Sun Solaris, and Microsoft XP clients. You want to keep the default Squid port but allow for migration of existing clients. What would be the best setting for the squid.conf file?

- **A.** `http_port 80`
- **B.** `http_port 3128 8080`
- **C.** `http_port 3128`
- **D.** `http_port 3128 80`

Correct answer and explanation: **D.** Answer **D** is correct as this will keep the default Squid port (3128) and allow the existing Microsoft clients to still access the proxy through port 80, which is the default for Microsoft. You can systematically change this port to 3128 at your leisure.

Incorrect answers and explanations: **A**, **B**, and **C.** Answer **A** is incorrect as although this will allow most clients (particularly Microsoft ones) to access the proxy, it does not include the default Squid proxy port. Answer **B** is incorrect as this includes the default Squid proxy port but the normal proxy port for Microsoft is 80. Answer **C** is incorrect as this is the standard port for Squid, but Microsoft clients would normally use port 80, which is not included.

9. In your DHCP server, you wish to allocate a fixed IP address to one of your color laser printers. What do you need to do to set this up?

- **A.** Find the IP address the printer is currently assigned and fix it using the dhcpcd fix IPaddress command on your DHCP server.
- **B.** Ensure bootp is available on the printer and then assign an IP address to this in the dhcpd.conf file with the host parameter.
- **C.** Find the printers' MAC address and a spare IP address from the pool of IP addresses defined on your DHCP server and set this up in the dhcpd.conf file with the host parameter.
- **D.** Set a fixed IP address directly on the printer and allow this to broadcast it to the DHCP server upon the printer being started.

Correct answer and explanation: **C.** Answer **C** is correct as you can set a fixed IP address against a specific MAC address using the host option.

Incorrect answers and explanations: **A**, **B**, and **D.** Answer **A** is incorrect as there is no command option to dhcpcd to fix the IP address. Answer **B** is incorrect as bootp is a program that will ask the DHCP server for an IP address. The DHCP server needs to know this is a fixed IP address and this has to be set up with the host option. Answer **D** is incorrect as this may cause an IP address conflict as the DHCP server has not allocated a fixed IP address to this and may issue that IP address to another client.

10. Your new Apache Web server has been set up and one of the developers wants to know which directory to load the Web pages. How can you find out which directory this is?

- **A.** Look in the httpd.conf file for a WebRoot directive
- **B.** Look in the httpd.conf file for a DocumentRoot directive
- **C.** Look in the httpd.conf file for a ServerName directive
- **D.** Look in the httpd.conf file for a WebBase directive

Correct answer and explanation: **B.** Answer **B** is correct as the DocumentRoot parameter correctly defines the root directory where the Web pages are stored.

Incorrect answers and explanations: **A**, **C**, and **D.** Answer **A** is incorrect as there is no WebRoot parameter. Answer **C** is incorrect as the ServerName parameter defines the name of the Web site. Answer **D** is incorrect because, again, there is no WebBase directive.

11. You have been told that your mail MTA is being used as a relay by spammers. You want to stop this happening. What is the best course of action?

- **A.** Relocate the mailserver behind your corporate firewall and only allow TCP port 25 to and from this server.
- **B.** Ensure that the only hosts that the mailserver will allow to relay are on your local network by configuring the /etc/mail/access file.
- **C.** Ensure that only your domain can be relayed by configuring the relay-domains file.
- **D.** Configure the mailserver to stop all relaying of mail and make sure all the users connect to it via an approved client.

Correct answer and explanation: **B.** Answer **B** is correct as this will specify which of your networks can connect to this mailserver and have their mail relayed. If you configure the networks correctly, the spam mail will not be relayed.

Incorrect answers and explanations: **A**, **C**, and **D.** Answer **A** is incorrect as relocating the mailserver behind a firewall will not help. The server will have to have port 25 open on it, and this is used by spammers to force the mailserver to relay messages. This option would be useful if the correct configuration files as specified in Answer **A** were done. Answer **C** is incorrect as this will allow the domain users to still send e-mail, but spammers can easily spoof the domain name and could continue to use this as a relay mailserver. Answer **D** is incorrect because if you stop the mailserver from relaying all mail, users will not be able to send any mail.

12. The speed of your Internet connection has slowed down because of the increase in the number of employees in your company. You have installed a Squid proxy and now wish to restrict the browsing of certain sites to lunchtimes only. You have set the list of banned sites up as an acl called banned_sites. Which is the correct configuration in the squid.conf file?

- **A.**
  ```
  acl lunchtime MWWTFSS 12:00 13:00
  http_access allow banned_sites lunchtime
  ```

- **B.**
  ```
  acl lunchtime MTWTFFSS 12:00 13:00
  http_access allow banned_sites lunchtime
  http_access deny banned_sites NOT lunchtime
  ```

- **C.**
  ```
  acl lunchtime MWHFFSS 12:00 13:00
  http_access allow banned_sites lunchtime
  http_access deny banned_sites
  ```
