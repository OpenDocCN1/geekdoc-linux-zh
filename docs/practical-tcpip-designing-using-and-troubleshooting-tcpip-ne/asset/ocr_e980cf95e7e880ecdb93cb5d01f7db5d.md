# ### 24.7 Choosing a firewall

Firewalls and security are two areas where we always advocate buying a product (even though free software packages are available) for the following reasons:

+   1. if your security matters at all, it's important to *know* that it really is doing what you think it is. Buying a firewall would be worthwhile just for the logging and alerting facilities, even if you ignored the protection it offers

+   2. nowadays you can buy a “firewall in a box,” i.e. a hardware firewall appliance. For many people these are a better option than a firewall software package running on a PC or workstation (see below)

+   3. firewalls aren’t ridiculously expensive any more. You can buy small appliances starting at about US$500

+   4. if you choose the right firewall, you can be up and running the same day.

However, if security isn't paramount, or if you have a lot of security expertise, or later on when you really know what you're doing and if you have the time, you could consider using the firewall facilities such as *ipchains* that are available free for Linux.

Below are some of the important factors to consider when choosing a firewall.

# #### Basic security features

+   1. how secure is the firewall? That’s a hard question for anyone to answer. Check out the fundamental features of the firewall: does it offer packet filtering, or stateful packet inspection, or application-level gateways/proxies? Look in the computer press for technical reviews on the firewalls you’re interested in.

+   2. does it support VPN (Chapter 27)?

+   3. does it support NAT (Chapter 23)? Almost every firewall does nowadays. Combining NAT and VPN in the one box overcomes the problems that NAT has trying to modify packets that have already been encrypted by a separate VPN system (Module 23.3)

+   4. does it support URL blocking (Module 25.3)?

+   5. does it support virus scanning for Web, e-mail, and FTP traffic (Module 25.2)?

# #### Other features

+   6. does it support only two Ethernet ports (for basic firewalling) or can it have a third port for implementing a DMZ, or even multiple DMZ ports?

+   7. does it have a high-availability option to let you run two firewalls in tandem, so that if one fails, the backup unit takes over automatically?

+   8. how easy is it to use? With some firewalls you need weeks of training before you can be confident using them. With others, a few hours will get you started. (We once had a customer who had a big complex firewall. They contacted us for help three years after the guy who installed it had left: they hadn’t touched it in the meantime and didn’t