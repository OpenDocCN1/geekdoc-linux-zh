# ## Manually Starting and Stopping Your Network

Sometimes, the Network Configuration Utility configures your network stuff but cannot activate it. Why does that happen? Who knows? It may be because the Network Configuration Utility is still relatively young and should become better with age. In the meantime, you can start your networking systems another way, by following these steps:

+   1. Click the GNOME Menu button, choose System Settings\u003eServer Settings\u003eServices, and then enter your root password, if you're prompted.
2. Select the Network option and then click the Restart button.
3. If you're using a wireless NIC that doesn't communicate, you may have to restart your PCMCIA system. Here's how:
	1. Locate and click the PCMCIA service in the Service Configuration Utility.
	2. Click the Restart button.
	3. Repeat Step 3 to restart your network.

All networking is stopped and then started again.

Alternatively, you can log in as root in a terminal emulator and run this command: `/etc/init.d/network restart`. (Or to stop your network, run `/etc/init.d/network stop`.)