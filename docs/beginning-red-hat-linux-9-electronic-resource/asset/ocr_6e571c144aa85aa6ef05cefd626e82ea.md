![](bbox=[0.13, 0.05, 0.87, 0.41])

Feel free to experiment further with this – adding more mailbox addresses and hooking it up to the Internet. You can also send and receive mail from Windows machines, using Microsoft Outlook. The same configuration settings should also suffice for Outlook: you'll need set the server type to SMTP, which is the only option in Outlook for sending e-mails.

# # Setting up a DHCP Server

We've already come across DHCP, during the installation process back in Chapter 1 – specifically, in the step where the installation tool invites us to specify our machine's network configuration. You may remember that, in that step, we are asked to choose between two options:

+   -   We can specify the TCP/IP settings (IP address, netmask, default gateway, and DNS servers) explicitly
+   -   We can allow a DHCP server to dictate those settings

This is what the **Dynamic Host Configuration Protocol (DHCP)** is all about. DHCP is a network protocol, whose purpose is to assign TCP/IP settings to client machines. By configuring a client machine to use DHCP, we're telling it that it **must contact a DHCP server** (on the network), and get its TCP/IP settings (IP address, netmask, default gateway, DNS servers) from there.