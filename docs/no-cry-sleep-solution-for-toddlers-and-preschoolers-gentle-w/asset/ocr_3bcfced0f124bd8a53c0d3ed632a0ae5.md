then run KonCD from the menu entry. You could also open a terminal window and enter the program's name.

# Security Configuration

Once you have installed your Linux system, you should carry out some basic security measures to protect your system from outside attacks. Systems connected to the Internet are open to attempts by outside users to gain unauthorized access. This usually takes the following forms:

+   - Trying to break into the system
+   - Having broken in, changing or replacing system files with hacked or corrupt versions
+   - Attempting to intercept communications from remote users
+   - Changing or replacing messages sent to or from users
+   - Pretending to be a valid user

Firewalls, intrusion protection, encryption, data integrity, and authentication are ways of protecting against such attacks.

+   - A firewall prevents any direct unauthorized attempts at access.
+   - Intrusion detection checks the state of your system files to see if they have been tampered with by someone who has broken in.
+   - Encryption protects transmissions by authorized remote users, providing privacy.
+   - Integrity checks such as modification digests guarantee that messages and data have not been intercepted and changed or substituted en route.
+   - Authentication methods such as digital signatures can verify that the user claiming to send a message or access your system is actually that person.

# Security Services

Red Hat includes several security services for protecting your system and your network transmissions (see Table 4-3). Using GNU Privacy Guard (GPG) you can encrypt your e-mail messages or files you want to send, as well as letting you sign them with an encrypted digital signature authenticating that the message was sent by you (see Chapter 16). The digital signature also includes encrypted modification digest information that provides an integrity check, allowing the recipient to verify that the message received is the original and not one that has been changed or substituted.

A good foundation for your network security is to set up a Linux system to operate as a firewall for your network, protecting it from unauthorized access (see Chapter 19). You can use a firewall to implement either packet filtering or proxies. Packet filtering is simply the process of deciding whether a packet received by the firewall host should be passed on into the local system or network. The firewall package currently in use is Netfilter (iptables). Older distributions versions releases use an earlier version called ipchains. To implement a firewall, you simply provide a series of rules to govern what kind of access you want to allow on your system. If that system is also a gateway for a private network, the system's