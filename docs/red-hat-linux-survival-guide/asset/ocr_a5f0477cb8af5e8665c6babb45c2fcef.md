By default, bindconf creates a master zone called localhost with the appropriate reverse DNS configuration. This is shown in the main menu window. This configuration is used for the loopback address only.

![](bbox=[0.07, 0.2, 0.44, 0.36])

Figure 15-1 The bindconf main screen.

# Creating a forward master DNS zone for a domain

Say you want to create a forward master zone for a new domain called evoknow.com. Do the following:

+   1. Click the Add button in the main bindconf window and you will see a screen as shown in Figure 15-2. Select Forward Master Zone option and enter the appropriate domain name in the name entry area and click OK to continue.

![](bbox=[0.15, 0.66, 0.5, 0.81])

Figure 15-2 Selecting a zone type.

+   2. You will see a screen as shown in Figure 15-3. You can change the contact address to a more appropriate address than root@localhost.