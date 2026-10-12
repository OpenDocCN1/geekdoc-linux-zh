
Multiple Phase 2 exchanges (i.e. conversations) can happen after a single Phase 1 exchange – because the channel set up in Phase 1 can be used repeatedly, reducing the overall amount of network traffic required.

In Phase 1, the two systems use the Diffie-Hellman key agreement method. This lets two parties converse over a public communications channel to negotiate a secret number, even if they don't have any shared secret information to begin with. Even though Eve the eavesdropper can listen in to the whole conversation, she won't be able to find out what the secret number is. (This sounds like magic but see the Notes for more information.) In IKE the two parties use the secret number they agreed as the encryption key for the rest of the IKE session.

IKE gets complicated because there are many different options in each phase. In Phase 1 the two parties can:

- authenticate using a shared secret (almost like a password) that both of them know, or using digital certificates and signatures, or using public-key encryption. With shared secrets, you still have to distribute them manually, which still isn't scalable to large numbers of sites. With public-key encryption or certificates, if Alice and Dave want to set up a VPN, they look up each other's public encryption keys (e.g. from a Secure DNS server or in a public LDAP directory of public keys) and can then use IKE as before. There is no longer any need to distribute keys or secrets manually.
- use either main mode or aggressive mode to set up the secure channel. (Main mode hides the identities of the two parties from snoopers but aggressive mode uses fewer packets.)
- use different encryption and authentication algorithms, and different groups (used in the secret-number generation process) for the Diffie-Hellman exchange. There are currently five of these groups (named “1” … “5”). They are also called Oakley groups as they were used in the earlier Oakley protocol. (In fact IKE is a mixture of Oakley and ISAKMP – the Internet Security Association and Key Management Protocol.)

In Phase 2, the parties can:

- use different encryption and authentication algorithms
- have perfect forward secrecy (PFS) or not
- issue many proposals to one another, indicating which type of encryption algorithms each one is prepared to accept. The other party has to choose one of the proposals, and this specifies the details of the SA IKE will create. IPsec's ESP or AH then use this SA as before
- specify the key lifetime, i.e. the duration after which new keys ought to be renegotiated.

IKE runs over UDP, and uses port 500.

In the next module, we show the VPN settings for a Windows client.

### 27.7 IKE example

![](img/a2132b646d336d5f9a21102d6320e537_733_0.png)

**Figure 27.9** Dial-up VPN, IKE setup 1

Figures 27.9 and 27.10 show IKE settings for a Windows VPN client (‘bump in the stack’ implementation) configured to VPN to several sites on the Internet. We chose a single-PC VPN system so that you can see the VPN settings clearly. (If we showed a firewall’s VPN settings, they would be dependent on the firewall’s NAT and other configuration details, which are not relevant to us here.)

![](img/a2132b646d336d5f9a21102d6320e537_734_0.png)

**Figure 27.10** Dial-up VPN, IKE setup 2

### 27.8 Protecting dial-up VPN

![](img/a2132b646d336d5f9a21102d6320e537_735_0.png)

If Alice uses VPN software on her laptop, which you've pre-configured to connect to the HQ LAN (Figure 27.11), all traffic between the laptop and HQ's firewall is secured. Sounds good so far. But if a hacker physically steals Alice's laptop (or someone borrows it for a while), they have full access to the HQ LAN, just like they were connected to your Ethernet inside the firewall. You need to provide some extra security mechanism. There are several different options:

- username/password protection. Asking for a password before a VPN connection is established is an extra barrier to the thief
    - this password protection could be built into your VPN client software (although we haven't seen any that have this feature)
    - many firewalls, routers, and VPN boxes support RADIUS authentication, described below, where the VPN system receives the connection attempt from the laptop, but refers the authentication (“login”) request to a separate server for validation (Figure 27.11)
- two-factor authentication systems, where the user has a special smart-card or other type of device. This displays a special number that changes regularly (e.g. every minute). To logon, the user has to enter the currently displayed number, plus a password. The VPN system (or associated authentication server) also generates the same sequence of numbers internally, and when the user tries to log on, the server validates the password but also compares the number entered with the internally generated one. Only if everything matches is the logon allowed. The advantage of this system is that a thief has to obtain not just the smart-card device, but also the password, and that can't be physically stolen.

#### RADIUS – Remote Authentication Dial-In-User Service

RADIUS offers user authentication (“logging on”) as a network service. As with LDAP, user-names and passwords and details of which resources each user is allowed access are stored on a central server. However, with RADIUS the authentication checking is performed on the RADIUS server, not on the client machine. (Some RADIUS servers store their user information in an LDAP directory, combining the benefits of both systems.) The client, e.g. the firewall or VPN box, encrypts the logon information that the user entered, and sends it to the server. The server checks whether the user has authenticated correctly, and replies to the client with either an Authentication Acknowledgement or an Authentication Reject message, which is also encrypted. RADIUS uses UDP; its official well-known port is 1812, although many implementations default to port 1645 for historical reasons.

RADIUS was originally developed to allow multiple remote-access servers to be controlled by a single authentication database. It’s now also used widely by firewalls, routers, and VPN systems (Figure 27.12).

![](img/a2132b646d336d5f9a21102d6320e537_736_0.png)

### Other VPN security issues

An external laptop connected to your LAN via VPN appears (more or less) to be connected directly to your LAN, with the same ability to access resources as our local PCs. This can be dangerous: if the laptop isn’t protected as above, you can’t be sure who is using it. Even if the user is genuine, they may have connected to Internet sites or received e-mail that infected them with viruses, etc. and when they VPN in to HQ, they can easily infect your “protected” LAN. To guard against such problems you can restrict what the laptop user may do by (a) configuring their VPN software so they can only connect directly to HQ, ensuring all their Web surfing and e-mail is processed by the central HQ servers for virus scanning, content filtering, etc., and (b) giving them access only to the resources they need, but no more, both by restricting the traffic they are allowed to send through the VPN tunnel, and by using host-based security mechanisms on the LAN – on the servers in particular. In addition, you might use “personal firewall” software for laptops – as a product on its own or combined with VPN – that is becoming widely available now.

If you connect machines to the local LAN using wireless networking, you should consider treating them as “external” machines requiring VPN protection, etc. Otherwise, passing hackers might be able to connect to your LAN from just outside your building, using their wireless networking cards.

### 27.9 VPN troubleshooting

![](img/a2132b646d336d5f9a21102d6320e537_737_0.png)

As we mentioned in Module 27.6, VPN implementations differ widely for many reasons. What we give here are general tips that we’ve found useful with many different systems. (The overall approach is not unlike troubleshooting a firewall; see Module 24.9.)

It would be wonderful if every vendor included superb debugging tools in their products, but alas, they don’t. Often you’ll find that your VPN link doesn’t work, but there are no error messages and no log messages. VPNs are often hard to get working for this reason and we have certainly had our share of problems.

- read all your log and error messages, at both ends of the VPN tunnel
- the best way we’ve found to set up VPN is to get it working on a test network integrated with your live LAN. We describe this in detail in the next module. To explore dial-up VPN and work through Windows Networking issues, etc. we also use a small, test network (Figure 27.13), similar to that described in Module 26.12. In this configuration our live LAN simulates the ISP’s network and the Internet; the test dial-up connects over this to the test VPN box and test LAN, which are attached to our live LAN. This configuration lets us sniff packets and see what’s happening everywhere
- use tcpdump of course! By tracing traffic just inside and just outside the VPN box (Figure 27.14) you can see traffic “in clear” reaching the VPN box and any transformed (ESP or AH, IP protocols 50 or 51) traffic heading to your Internet router. If you see transformed traffic leave your site, but none returning, you know that your own configuration is at least half correct. If you (or a colleague) can trace the traffic at the other end too, you can form a good view of what’s happening and where the problem is likely to be
- manual keying is much easier to set up, because there are far fewer different options. It has no key-negotiation stage: if your keys and IP addresses are set up correctly, you’ll see VPN traffic leave the VPN box as soon as you generate some test traffic from inside. We always start with manual keying; only when that’s working do we try IKE. This is an example of the principle that it’s best to start simple and get a basic configuration first. Then, and only then, should you start adding more complexity or sophistication: at each step verify that the system is still working, and if it isn’t, your most recent change is usually what caused the problem
