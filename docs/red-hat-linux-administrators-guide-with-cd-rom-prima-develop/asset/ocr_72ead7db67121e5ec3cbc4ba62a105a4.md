![](bbox=[0.12, 0.12, 0.48, 0.5])

# **FIGURE 20.2**

A sample *mrtg* Web page displaying the amount of traffic being routed through your network.

+   6. Define some parameters on your router. If you are using a Cisco router, the following rules will apply:
+   
+      a. The mrtg program uses snmp packets for monitoring traffic. You will need to enable this feature on your router. Log in to your router, type **enable password**, then enter **conf t**. This command displays the current configuration.
+   
+      b. Now enter **snmp-server community public RO** or the variables of your choice. The community and public features are insecure. Define something more unobvious.
+   
+      c. Save this information to your configuration by entering **exit**;
+   
+         **write mem**.
+   
+   7. Define on your Linux box a logs/ directory or make one in your mrtg directory. This is where you will be storing all data gathered from the router. Enter the following command: **cd /usr/local/gnu/mrtg/; mkdir logs/.**