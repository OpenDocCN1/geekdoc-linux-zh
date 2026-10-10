Absolutely. Most of the documentation follows the same pattern that ours does to assign a private address and then assign a floating IP connected to a provider network as needed. However, it's common for operators to instead assign these addresses directly from a provider network if they know their services need to be on a specific network or on the Internet.

Refer back to Chapter 3, “Networking,” for in-depth discussion about networking and the decisions made for this book.

We will now walk through how to add a floating IP to your instance so we can SSH into it and then run a web server on it. In the Actions menu for your instance you want to select Associate Floating IP to bring up the screen to work with your IPs. Under IP Address you can click on the plus sign to add a new IP, which will bring up the Allocate Floating IP screen. This will ask you what pool to get the addresses from and your only option should be ext-net. When you click Allocate IP it will select an address from the pool and make it available to assign to your VM, by default it will bring you back to the Manage Floating IP Associations screen with that new IP address filled in to the IP Address field, as seen in Figure 6.9.

You now click Associate to add it to your instance. This is done live and is typically available very quickly without rebooting your instance. You should get a green Success dialog and in the IP Address column for your instance you should have something like:

10.190.0.11
Floating IPs:
203.0.113.9

![](bbox=[0.1, 0.61, 0.9, 0.88])

Figure 6.9 Allocate IP