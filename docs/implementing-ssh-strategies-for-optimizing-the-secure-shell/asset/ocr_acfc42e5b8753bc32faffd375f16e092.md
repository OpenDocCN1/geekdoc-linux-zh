+   4. In the **Allow** section, select the **Allow** radio button.
+   
+   5. For the **Filter** type, select **IP address**.
+   
+   6. In the **IP address** field, type **192.168.0.10**.
+   
+   7. In the **Port** section, select the **Port** radio button and type **25** in the text box.
+   
+   8. In the **Comment** field, type **Mail Relay**.
+   
+   9. Select **OK**.
+   
+   10. Repeat steps 7 through 11 for the other three servers. The final result should look like **Figure 6.24**.

Once **Allow** rules are applied on the **VShell SSH** server, only the servers specifically allowed will be accessible via port forwarding; all other servers and /or devices will not be accessible. This makes any **Deny** rules redundant, since everything else is denied automatically besides the server that has been allowed. Furthermore, any server port-forwarding filters override any client port-forwarding rules on the SSH clients themselves.

If the entire network were allowed to port forward, except for a few specified servers, both **Allow** filters and **Deny** filters would be required. For example, if the internal network had an **IP range** of **172.16.1.1-172.16.1.254** and the only server restricted was **172.16.1.100**, the **VShell** port-forwarding filtering would need to look like **Figure 6.25**, where the **172.16.1.0** network is permitted and the **172.16.1.100** server is specifically denied.

![](bbox=[0.15, 0.58, 0.61, 0.95])