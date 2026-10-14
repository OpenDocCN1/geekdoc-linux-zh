+   4. In the Network Configuration proposal, under Firewall, select **enabled**. The entry will change to **Firewall is Disabled**.

+   5. Make sure that the text beneath Network Interfaces says the interface is configured to use DHCP.

+   6. (Conditional) In a self-study environment with no other students in the network and with no DHCP server running, do the following:
+   
+      a. From the Network Configuration proposal, select **Network Interfaces**.
+   
+      b. Select the first detected network card, then select **Edit**.
+   
+      c. Select **Static Address Setup**.
+   
+      d. In the **IP Address** field, enter **10.0.0.10**.
+         Note: If your self-study environment is connected to a network, you could use an unused address from that network.
+   
+      e. In the **Subnet Mask** field, enter **255.255.255.0**.
+   
+      f. Configure the hostname and name server:
+         i. Select **Hostname and Name Server**.
+         ii. Your hostname and domain name should already be filled in correctly; if not, enter **da10** and the domain name **digitalairlines.com**.
+         iii. In the **Name Server 1** field, enter **10.0.0.254**.
+              Note: If your self-study environment is connected to a network, you should use the name server available in that network instead.
+         iv. Return to the Network setup dialog by selecting **OK**.
+   
+      g. Configure routing:
+         i. Select **Routing**.
+         ii. In the **Default Gateway** field, enter **10.0.0.254**.
+             Note: If your self-study environment is connected to a network, you should use the default gateway available in that network instead.
+         iii. Return to the Network setup dialog by selecting **OK**.
+   
+      h. Return to the Network Card Configuration Overview dialog by selecting **Next**; select **Next** once more to return to the Network Configuration dialog.

+   7. Continue with the installation by selecting **Next**.

+   8. From the Test Internet Connection dialog, select **No**, **Skip This Test**; then select **Next**.

+   9. For the User Authentication Method, select **Local (/etc/passwd)**; then select **Next**.

+   10. Add a user:
+   
+      a. User’s Full Name: **GeekoNovell**
+   
+      b. User Login: **geeko**
+   
+      c. Password: **novell**