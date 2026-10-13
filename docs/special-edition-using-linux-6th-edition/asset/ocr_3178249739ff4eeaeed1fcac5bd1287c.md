I have a new print server box that needs to get an IP as part of its setup. How can I set up this print server under Linux?

The print server is looking for its address through ARP when it comes online. Do the following:

+   1. Make sure you have a DNS entry or an entry for the print server in your `/etc/hosts` file. For this example the print server will be called `rps1.fish.net`.
+   2. Look on the print server itself for a hardware address (also called a MAC address). This will be six hexadecimal numbers that can be separated by spaces or colons. A sample can look like this:
+   
+      `00:00:C0:7B:C0:00`
+   3. Use the following command to send the print server its IP/hostname mapping:
+   
+      `arp -s rps1.fish.net 00:00:c0:7b:c0:d0 temp`

This command tells your system to communicate with the print server’s Ethernet card and send it (at its MAC address of `00:00:c0:7b:c0:d0`—your address will be different) the IP that corresponds to `rps1.fish.net`. You should now be able to telnet to your print server to program it according to the instructions that came with your print server. You might have to repeat the arp command if the print server is powered off.