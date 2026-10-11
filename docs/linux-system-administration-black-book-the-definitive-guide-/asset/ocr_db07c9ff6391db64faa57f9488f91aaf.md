Unless you have done your homework, the intruder will find a way in. Even if you have done your homework, they still might be successful. “Preparing For A Breach,” in the Immediate Solutions section, explains what you should always have readily available for when you suspect you might have a break-in.

# Account Attacks

In a way, account attacks are the most insidious, because if the account breached is not used very often and you are not carefully monitoring user activities, they can go unnoticed for some time. I cannot stress how important it is to have a strong password policy and enforce it regularly. See the sections involving passwords in the Immediate Solutions section to learn more about the options available to you and how to use them.

Account attacks typically take the form of someone repeatedly trying passwords until they get in. They may be guessing them by hand, or running a utility that does the guessing for them. In fact, they may run the same Crack program covered in this chapter. In the Immediate Solutions section, “Analyzing Logs” explains one good way to watch for this type of activity.

# Firewalls And You

Many folks in the computer field think of firewalls immediately when they hear the word security. Whether a firewall is right for you depends on how much access you need to the outside world, and how much access you want people from the outside world to have to your system. Typically, when you build your firewall rules, you begin by denying all access, and then punch holes with specific rules allowing specific things. If you punch enough holes that your firewall looks like Swiss cheese, you have made it essentially useless. Firewalls are primarily useful for network segments or subnets that hold mission-critical data that should not be accessible to the outside world and so is worth restricting.

More than one type of firewall is available. On Linux, you typically implement either an IP filtering firewall or a proxying firewall. Which of these you choose depends on what you want people to be able to see in your network, and what amount of information you want to block. You also have the option of implementing a basic amount of IP filtering that is not a firewall at all.

What distinguishes a firewall from another form of security program is placement. A firewall lives on a single machine that is the only form of contact between the network segment it protects and the outside world, as represented in Figure 9.1. Because this scheme requires two entirely separate IP addresses and a significant amount of traffic, you need to have two Ethernet cards in the firewall machine; one to handle traffic to and from the outside world, and another to handle traffic to and from the internal network.