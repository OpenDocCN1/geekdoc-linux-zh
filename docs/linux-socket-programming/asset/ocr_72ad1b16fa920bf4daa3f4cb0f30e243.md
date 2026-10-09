To summarize, a rigid conducted conduit reduces the possibility of tapping. Optical has the added security of being impervious to electromagnetic snooping. Optical, additionally, has proven to carry very high bandwidths.

# Message Espionage

Protecting the message is less obvious. The firewalls pass through and filter information exposed to the Internet. They use specific ports and services that the client expects. Changing some of the expected settings and interfaces can increase your security.

While not encouraged in the Open Source movement, using privatized protocols can discourage intrusion (on the other hand, it can also increase attention). For example, instead of using HTTP as the protocol, invent a new and specialized version. This approach does have significant drawbacks: You must write the client interface and get that to your customers.

Another method is to limit windows of availability and information sent. For example, during World War II, the Allies used Native Americans to chat with each other over the airwaves for hours on end in their own language. At specified intervals, the message would shift to a tactical or strategic instruction or status.

Using that example, you could write a financial transfer mechanism that would fire up at specific intervals or even have it open all the time with irrelevant information during off hours.

Increasing randomness is the key to message security. For example, suppose you have an ATM (Automatic Teller Machine) that is connected to the Internet (scary thought!). It needs to send and receive transaction requests to the host server. One way it could use randomness is by continuously sending and receiving fake transactions. Then, at specified intervals, both the host and the ATM would recognize that a transaction is real. (Of course, this is still too loose for actual implementation.)

Another form of randomness is data encryption. Good data security depends strongly on the amount of randomness data encryption introduces. The more random the data is, the more difficult to decrypt the data. The key sets the range of possible outcomes. The perfect encryption key has no limit in size. Unfortunately, as the key increases in size, the computation time increases exponentially. So, a good key is one that is long enough to reduce the likelihood of discovery computationally. This is why everyone wants 128-bit encryption.

# NOTE

# Encryption Through Firewall Filters

You cannot join some technologies together to make a stronger defense against attack. For example, encryption defeats a firewall's active filtering. Again, active filtering looks into the packet for anything that might be suspicious. Unfortunately, if contents are encrypted, only the client and server know the contents (hopefully). If you have filtering enabled, you may only be able to expect passive filtering to work with encrypted messages.

128-bit encryption has a wide enough range that if a computer were to try each key in succession every nanosecond (1' 10-9 seconds), it would require over 1020 years to find the key. That's a long time. In terms of randomness, 128-bit encryption appears to be a large enough range to approximate the perfect key—at least for now.