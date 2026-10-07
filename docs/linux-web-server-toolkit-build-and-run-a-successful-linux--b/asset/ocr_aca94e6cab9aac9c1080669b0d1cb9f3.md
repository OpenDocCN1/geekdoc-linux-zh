# Linux Web Server Toolkit

+   - Do you charge per IP address? A one-time fee or monthly use?
- Do you charge for a domain name above the InterNIC fee? Is it a one-time fee for helping get it registered or a monthly fee providing a point of presence for it?
- Do you charge for me to use you as my primary name server, listing the machines at my site in your configuration files?
- Do you charge hourly fees for initial setup of my connection, beyond the setup fee? What exactly do I get for that setup fee?
- What type of troubleshooting or regular maintenance will you assist with when I buy a connection of this speed?
- Do you provide consulting services? What is your hourly rate for your middle- and top-level experts? Can you come on-site? For how much?
- Do you also do Web site design or consulting? Can you recommend companies to do this that you've had good experience?
- Do you have a listing of fees that have been incurred for various services, like a bank's list of fees?

Getting a domain name and IP address is a lot easier than it used to be. That's the good news. The bad news is that it is used to be free and now you have to pay.

# Acquiring an IP Address

A quick answer to how you get a domain and IP address for your site is. As described in Chapter 4, your ISP has control over a block of IP numbers. The ISP can give them out to customers, provided their use is justified. You can't have 200 IP addresses just because you ask for them. It's probably reasonable to ask for it to a dozen or two IP addresses for you directly from your ISP.

You can start this process by going to the InterNIC Web page at http://internic.net/. If you get an IP address from the InterNIC, you will need to give information to your ISP to facilitate routing your network onto the Internet.

Because the Internet is running out of IP addresses, you'll have trouble getting any that you don't need — least until the larger address space, IPv6, is firmly in place.

Remember also that you can use the reserved IP addresses starting with 192.168 for your Internet networks without getting "real" Internet addresses for them. You can also use the IP masquerading feature of Linux to provide live Internet access to an entire network using only one real IP address on the computer that is acting as the gateway to the Internet.