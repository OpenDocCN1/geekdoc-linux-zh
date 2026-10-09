![](bbox=[0.42, 0.09, 0.66, 0.31])

to change the state of the firewall and specify preferences. The large round icon in the Firewall frame of the window indicates the status of the firewall:

+   - **Disabled**—The firewall is turned off—it is as though firestarter was not installed.

+   - **Active**—The firewall is up and running and implementing the policy you have set up (or the default policy).

+   - **Locked**—The firewall is up and running and blocking all packets. Nothing can get in or out of the firewall host over the network interfaces that firestarter controls.

Click the appropriate icon on the toolbar to change the state of the firewall.

**Events** An *event* occurs when the firewall blocks a packet based on a rule. The Events columns in the Firewall frame list the number of inbound and outbound events the firewall has blocked and indicate how many of those were of a serious nature. Events are considered serious if they could have been attempts by malicious users to gain access to the system. For example, a blocked attempt to log in using ssh is a serious event; a blocked ping is not.

The Network frame shows the activity on each of the system’s network connections. When you click the plus sign to the left of **Active connections**, *firestarter* displays a scrollable list of active connections; lengthen the window to display more connections. Click on a line in this list to select it and then right-click and select **Look up Hostnames** to change the value in the Source and Destination columns from IP addresses to hostnames. The Port column lists the port on the target host that the connection uses. The Service column indicates the service that is associated with the specified port. The Program column shows the name the program running the service if it is local and known to *firestarter*.

# THE EVENTS TAB

The Firestarter window Events tab (Figure 25-7) is the key to modifying the default firewall policy. It displays a list of blocked connections. Each line in this list specifies an event that the firewall blocked based on a rule. Events displayed in black are attempts to connect to a random port and are typically not of concern. Events in gray are harmless, consisting mostly of broadcast traffic. Events in red are attempts