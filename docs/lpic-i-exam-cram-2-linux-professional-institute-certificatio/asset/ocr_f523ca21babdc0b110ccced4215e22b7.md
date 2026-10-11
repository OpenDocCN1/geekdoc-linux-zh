+   4. A user is complaining that she can’t reach a Web mail site she fre-  
+   quents, but she can reach other hosts on your networks and on the  
+   Internet. Which command would show you where the problem is  
+   occuring? Fill in the blank with just the most appropriate command  
+   name:

The correct answer is `traceroute`. There are no correct alternative  
answers.

+   5. When a user tries to access a server that has recently had its IP  
+   changed, he gets a message stating *host not found*. Which of the fol-  
+   lowing commands shows the relationship between that server’s IP and  
+   the MAC address of its interface on the network?  
+   *   A. `ping`  
+   *   B. `arp`  
+   *   C. `host`  
+   *   D. `nslookup`

Answer B is correct because it shows the IP-to-MAC mapping for a  
particular host. Answers A, C, and D are incorrect because they have  
nothing to do with the IP-to-MAC mapping.

+   6. You are configuring a system and need to set your `eth0` interface to  
+   have a default gateway with the address `192.168.33.1`. Fill in the blank  
+   with the exact command and options to accomplish this from the com-  
+   mand line:

The correct answer is `route add default gw 192.168.33.1`. There are no  
correct alternative answers.

+   7. You want to find the mail servers for a particular domain but not see all  
+   the address records. Which of the following commands can accomplish  
+   this? (Choose all that apply.)  
+   *   A. `nslookup`  
+   *   B. `host`  
+   *   C. `resolver`  
+   *   D. `dig`

Answers A, B, and D are correct because they all can be used to show  
MX records or the names of the mail servers. Answer C is incorrect  
because there isn’t a command on a default machine named `resolver`.

+   8. On a Red Hat machine, you need to edit a file that will set the order  
+   for how names are resolved. Fill in the blank with the full path and  
+   filename for this file:

The correct answer is `/etc/nsswitch.conf`. There are no correct alter-  
ative answers.