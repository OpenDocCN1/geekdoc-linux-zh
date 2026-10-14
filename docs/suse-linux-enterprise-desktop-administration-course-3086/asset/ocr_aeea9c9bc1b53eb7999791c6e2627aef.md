+   13. Restart sshd by entering
+       `rcsshd restart`
+   14. Try ssh geeko@localhost.
+       You should see an error message and no prompt for a password.
+   15. Log out as root by entering `exit`.

# Configure VPN Connections

In the past, dedicated phone lines to connect branch offices or dial-in connections for remote workers were widely used. Because they were, however, rather expensive, especially if used over a long distance, alternatives were needed.

These costs were remarkably reduced using the Internet. But with the use of the Internet, new problems arose, namely unauthorized access to the internal networks or unauthorized access to the data exchanged over the Internet.

To solve these problems, cryptography is used, both to ensure that only authorized users access the internal network and to protect the data traveling through the Internet from being viewed by unauthorized people.

**VPN and IPSec Basics** Technologies that use one network infrastructure, for example the Internet, to carry the packets of another network are usually classified under the heading VPN (Virtual Private Network). Figure 5-18 illustrates a VPN connection. By definition, a VPN does not necessarily have to encrypt the traffic, but encryption is used on most VPNs.

![](bbox=[0.11, 0.505, 0.79, 0.711])

**Figure 5-18**

Various technologies are used to implement VPNs. These technologies include IPSec (Internet Protocol Security), OpenVPN, L2TP (Layer 2 Tunneling Protocol), HTTPS (HTTP protocol over Transport Layer Security/Secure Sockets Layer), and SSH (Secure Shell).