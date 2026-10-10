port number have been designated, the local port-forwarding options need to be set. As you can see, the syntax can be quite long if several port-forwarding options are used. Different configuration files are ideal when more than one port-forwarding option is required to be set. (Refer to the Unix Setup section in Chapter 3, “Secure Shell Clients,” on how to set up different configuration files.) Once the SSH client is authenticated and the SSH session is established, the port-forwarding options will automatically be enabled. To confirm, type **netstat -an | more** and the port-forwarded ports should be listening on the loopback interface (127.0.0.1).

Once you have confirmed that the port-forwarded sessions are enabled, use your client application to connect to your port-forwarded session. For example, to use the Windows Terminal Services port-forwarding session, execute the terminal services client and enter **127.0.0.1** for the server IP address. Since 127.0.0.1 is listening on the SSH client’s machine on port 3889, it will accept this connection request from the client application and forward it to 172.16.11.72 via the SSH connection and the SSH server. Similarly, other clients, such as mail clients and Web clients, will need to use the loopback interface (127.0.0.1) to connect to the remote server via the SSH session.

# Configuration for SSH Communications’ GUI SSH Client

SSH Communications also creates a GUI SSH client for Windows operating systems. Using SSH Client 1 from Figure 6.11 as the starting point, we can configure the local port-forwarding options quite easily using the following steps:

+   1. Start **Programs** **SSH Secure Shell** **SSH Client**.
+   2. Click **Profiles** **Add Profile**.
+   3. Name the profile **SSH server** or anything you wish.
+   4. Click **Profiles** **Edit Profile** **SSH Server**.
+   5. Select the **Tunneling** tab.
+   6. Under the **Outgoing** tab, select **Add**. At this point, you can add the specific local port-forwarding information.
+   7. Under **Display Name**, enter **Mail Relay**.
+   8. Leave the **Type** drop-down menu to **TCP**.
+   9. Enter **25** for **Listen Port**.
+   10. Enter **192.168.0.10** for **Destination Host**.
+   11. Enter **25** for **Destination Port**.
+   12. Select the **OK** button.

The final result should look similar to Figure 6.12, which shows the SSH client’s outgoing tunnel configuration.