In this project we will create the same domain as explained in the last section. However, we will be using Red Hat 8's GUI tool to do the configuration. You will need to have the X Window System on your DNS server in order to perform the configuration in this way.

# ## Step by Step

+   1.  Launch the tool by either selecting Domain Name Service from the Server Settings submenu, or launch it from the command line as **redhat-config-bind**. You'll notice that the **localhost** and caching part is already filled in and set up for you. Unfortunately that's all that can be set up automatically without your attention.

![](bbox=[0.318, 0.403, 0.684, 0.589])

+   2.  Click the Add button on the right, and select Forward Master Zone from the dialog box to start configuring our primary zone.

+   3.  Enter **domain.com** into the text widget (or substitute your own domain name) and click OK.

+   4.  You'll move on to a dialog box called Name to IP Translations. You'll probably recognize the entries on this dialog box as corresponding to the SOA section at the top of your zone file. You will probably want to update the Contact address at the very least.

+   5.  If you're looking to modify the time values related to your zone, look for the Time Settings button near the middle of the dialog box. The defaults are usually an adequate starting point, however.

+   6.  The bottom half of the dialog box shows records you have defined for the zone. The default for a new zone will be just the domain name—**domain.com**, in our example. Click the Edit button while that entry is highlighted, and you'll have the opportunity to add name servers and mail exchangers for the zone.

*(continued)*