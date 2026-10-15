# Exhibit B
A pair of DNS packets in Wireshark

![](bbox=[0.21, 0.2, 0.85, 0.7])

A note of caution regarding Wireshark: although it has lots of neat features, it has also required many security updates over the years. Run a current copy, and do not leave it running indefinitely on sensitive machines; it might be a potential route of attack.

# 21.8 THE iCSI NETALYZR

We have looked at several tools for network debugging and for reviewing specific aspects of the network configuration. But even with your own best efforts at monitoring, it’s useful to have someone else take a peek at your network from time to time. The Netalyzr is a service provided by the International Computer Science Institute at Berkeley that provides a useful “second opinion.” To use it, just point your Java-enabled browser at netalyzr.icsi.berkeley.edu (note: missing ‘e’).

The Netalyzr tests your Internet connection in a variety of ways. It has the advantage of being able to access your network both from inside (through the Java program that runs in your browser) and from the perspective of ICSI’s servers.

Exhibit C shows the Netalyzr report for a workstation on a private network that’s attached to the outside world through a DSL link. The Netalyzr seems to be generally happy with the setup except for a few quibbles about the Apache web proxy that’s in use. (Blocking malformed HTTP requests may actually be a useful feature, however.)