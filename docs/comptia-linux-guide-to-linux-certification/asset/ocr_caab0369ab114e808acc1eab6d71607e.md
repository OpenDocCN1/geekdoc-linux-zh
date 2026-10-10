+   12. Highlight the class.com zone and click New, CNAME Alias. Type alias.class.com. in the Domain Name dialog box, and type server1.class.com. in the Canonical Name dialog box (taking care to include the trailing . in both FQDNs). Click OK to create the CNAME record.
+   13. Highlight the class.com zone and click New, MX Mail Exchange. Note the default domain of class.com. in the Domain Name dialog box and type server1.class.com. in the Mail Server Name dialog box (taking care to include the trailing . in the FQDN). Click OK to create the MX record.
+   14. Expand your class.com zone. Are the new records visible?
+   15. Expand the zone that represents your classroom network. Are PTR records available for reverse lookups?
+   16. Click Save. Click OK when prompted to save your changes to the configuration files on the hard drive.
+   17. Close the BIND configuration utility, log out of the GNOME desktop environment, and switch back to tty2 by pressing Ctrl+Alt+F2.
+   18. At the command prompt, type systemctl start named.service and press Enter to start the DNS name daemon.
+   19. Edit the /etc/resolv.conf file with a text editor and remove any existing nameserver lines. Add the line nameserver 127.0.0.1 to ensure that your Linux computer uses the local DNS server daemon for name resolution. Save your changes and quit the editor when finished.
+   20. At the command prompt, type ping -c 4 gateway.class.com and press Enter. Was the name resolved successfully? Explain.
+   21. At the command prompt, type ping -c 4 server1.class.com and press Enter. Was the name resolved successfully? Explain.
+   22. At the command prompt, type ping -c 4 alias.class.com and press Enter. Was the name resolved successfully? Explain.
+   23. At the command prompt, type ping -c 4 www.yahoo.com and press Enter. Was the name resolved successfully? Explain.
+   24. At the command prompt, type dig @localhost class.com ANY and press Enter. Are your resources records returned successfully?
+   25. At the command prompt, type less /etc/named.conf and press Enter. View the entries. Is class.com a Master zone? Do you see a line that forwards unknown requests to your classroom DNS server? Press q when finished.
+   26. At the command prompt, type cat /var/named/class.com.db and press Enter. View the entries. Are your resource records present?
+   27. At the command prompt, type cat /var/named/network_ID.db and press Enter where network_ID is your classroom network ID. View the entries. Are PTR resource records present?
+   28. At the command prompt, type less /var/named/named.ca and press Enter. View the entries. What do these entries represent?
+   29. Type exit and press Enter to log out of your shell.

![](bbox=[0.925, 0.685, 0.985, 0.745])