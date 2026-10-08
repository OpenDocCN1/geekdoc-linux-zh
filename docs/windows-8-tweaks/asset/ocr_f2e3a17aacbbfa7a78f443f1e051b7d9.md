![](bbox=[0.14, 0.06, 0.86, 0.45])

**Figure 19-3:** Use Windows Firewall with Advanced Security.

This main screen is where you can see if the firewall is on and if the Inbound and Outbound Rules are active. The next step is to view the specific rules. You can do that by simply selecting Inbound Rules or Outbound Rules from the list on the left. Go ahead and click Inbound Rules now.

Shortly, you will see all the rules currently set up on your computer. If they are enabled, they will have the green icon. If not, the icon will be gray. You can also see what firewall profiles the rule is used in, as shown in the Profile column in Figure 19-4. If you ever need to enable or disable a rule, just right-click it and select Enable or Disable. You can also edit an individual rule’s properties by right-clicking the rule and selecting Properties. Working with the Outbound Rules is exactly the same as working with Inbound Rules; Outbound Rules just control a different direction of traffic.

For the sake of demonstrating how to add a new rule, say that you just installed some type of server on your computer that users will connect to on TCP port 800. Follow these steps to open up a hole so that your users can connect:

+   1. If the Windows Firewall with Advanced Security window is not already open, open the Start screen, type `wf.msc`, and press Enter.

+   2. After the management console loads, click Inbound Rules.