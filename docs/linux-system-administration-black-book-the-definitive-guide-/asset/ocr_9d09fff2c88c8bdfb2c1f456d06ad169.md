+   12. Do one of the following:
+       * Return to the section you came here from and continue through its instructions.
+       * Press the Esc key to go to Command mode and then type “ZZ” to save and close the file.

# Setting Up Multicasting

To set up Web cache multicasting, do the following:

+   1. Log in as root to the machine you installed Squid on.
+   2. Type “/vi /etc/squid/squid.conf” to open the Squid configuration file for editing.
+   3. Type “/mcast_groups” and press Enter to jump down to to:
+      ```
+      #mcast_groups  239.128.16.128
+      ```
+   4. If you want this machine to listen for offerings of multicast broadcasts, then uncomment this line and type “i” to enter Insert mode. Change the given IP address to the address for the group you are connected to.
+   5. Type “/mcast_icp” and press Enter to jump down to:
+      ```
+      #mcast_icp_query_timeout 2000
+      ```
+   6. If you want to set how long Squid waits to hear back from its ICP attempts to find out who is listening, uncomment this line and change the number of milliseconds listed.
+   7. Return to the section you came here from, or press the Esc key to enter Command mode, and then type “ZZ” to save and close the file.

# Configuring A Client To Utilize Caching

To configure Netscape to look to the caching server instead of directly to Apache, do the following:

+   1. Log into the account you want to set up.

> *TIP:* If you take good notes, you can send each new user instructions on how to do this themselves.