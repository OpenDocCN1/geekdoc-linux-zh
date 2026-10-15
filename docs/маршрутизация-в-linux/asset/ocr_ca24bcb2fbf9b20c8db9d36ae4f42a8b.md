![](bbox=[0.45, 0.05, 0.62, 0.26])

# 3

# Introduction to Border Routing Protocols

SO FAR, THIS BOOK HAS DISCUSSED routing protocols that are used within a specific autonomous system (AS). This isn't enough, however, if your AS is connected to the Internet or another AS. Along with the internal routing protocols you choose for your network(s), you also need to consider the border routing protocol(s) you are going to use to allow your intranets to talk to the wider world of the Internet. Border protocols take the information passed throughout your AS and determine what portions need to be shared with your neighbors, as well as bring in relevant data from the outside world.

We'll start with a look at the distinctions between interior and exterior TCP/IP gateway protocols and work our way up from the most simple of the offerings in the Unicast field through more modern solutions that streamline the routing process for both unicast and multicast.

# Interior Gateway Protocol (IGP)

Let's start with a quick review of what's going on within the AS itself and introduce some terminology. Within this AS we have areas: at least one unicast routing protocol and perhaps one or more multicast protocols. All of the routing protocols used within the AS are Interior Gateway Protocols (IGPs).