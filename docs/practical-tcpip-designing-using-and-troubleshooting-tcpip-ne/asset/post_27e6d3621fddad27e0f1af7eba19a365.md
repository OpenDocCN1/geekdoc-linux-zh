
- for manual keying, we start with very simple keys that we can easily read and check over the phone. We use “0123456789abcdef” for a 16-digit key and the same thing repeated twice for a 32-digit key. (But make sure you change them to something less easily guessed as soon as the link is working!)
- ISPs often block the IPsec AH and ESP protocols by default. (It’s more unusual to have IKE blocked, because it runs over UDP) Before you even start installing your VPN, check that the ISPs at both ends allow protocols 50 and 51 (ESP, AH) and UDP port 500 (IKE) in and out of their networks
- many ISP services for home users (e.g. cheap or free phone calls to the ISP, and some ADSL or cable modem services) deliberately block ESP and AH, since they are only used by business customers. You may have to pay extra to have these blocks removed
- if you have your laptop set up to VPN to the office (e.g. to 10.*.*) and later bring it into the office and connect up to the LAN, traffic for 10.*.* will still be VPNed. (Typical symptoms are that ARPs succeed – arp -a shows other machines – but no other TCP/IP traffic is transmitted on the wire.) You need to either manually disable the VPN when on the LAN, or enable VPNing only on the dial-up interface (cf. Module 26.10.)
- because IPsec is an evolving standard and IKE is very complex, not all implementations inter-operate with one another or support all options. This will become less of a problem in time, as implementations are tested and improved (and maybe IKE will be replaced with something better – see Notes). In the meantime, you may have to restrict yourself to option combinations that your VPN manufacturer recommends
- if you’re using Microsoft Windows Networking over VPN, remember that your network now involves routers, so you’ll have to use WINS (or an LMHOSTS file) if you want NetBIOS name resolution and network browsing to operate correctly (c.f. Module 26.11).

In the next module we explain how to integrate a test network with your live LAN, to simplify troubleshooting and to check out your configurations before you actually deploy them live.

![](img/a2132b646d336d5f9a21102d6320e537_738_0.png)

Figure 27.14 Use tcpdump outside your firewall to see encrypted VPN packets

## 27.10 Building a test network for VPN

A technique that saves us a huge amount of time is to “glue on” a test network to our live LAN. Let’s say we’re going to install a VPN firewall at our new office in New York (“NY”). Our aims are to:

- install the test firewall alongside the live network in Cambridge (“CAM”), so we can check out VPN, etc.
- configure the New York firewall/VPN fully, so it can be slotted into the real remote site without any extra configuration. We’ll just courier it over to the new office, and have someone connect it up. We want to avoid sending an engineer over if possible.

However, there are many constraints:

- we’re working on our live network, so CAM’s Internet connectivity must not be disrupted for more than a minute or two at most
- the CAM router is managed by the ISP, and we can’t alter it. Therefore we need another way to route traffic between the CAM and NY networks. We’ll insert a temporary extra router to do this
- the NY firewall must be outside the live CAM firewall, so VPN and firewall rules for NY/CAM traffic are exercised
- the NY firewall must be inside CAM’s ISP’s router. It will have public IP addresses that really belong in NY; if any packets for these appeared on the network outside the CAM live router, they would be routed to NY.

We build the network shown in Figure 27.15 here in Cambridge. We’ve used a Linux box as the extra router; if you use an NT box instead, the steps are the same but the commands to apply the settings will of course be different.

![](img/a2132b646d336d5f9a21102d6320e537_739_0.png)

1. **Configure the extra router:**
   - ensure IP forwarding is enabled:
   
   ```bash
   echo 1 > /proc/sys/net/ipv4/ip_forward
   ```
   
   - set its IP address to an unallocated one from the set of CAM public addresses. Its netmask should match the CAM firewall's external interface.
   
   ```bash
   ifconfig eth0 192.0.0.2.2 netmask 255.255.255.0
   ```
   
   - create a new interface **eth0:1** to match the real Internet router in NY:
   
   ```bash
   ifconfig eth0:1 1.1.1.57 netmask 255.255.248 up
   ```
   
   By choosing the IP address to match the real NY router, once we've configured the NY firewall, it can be installed in NY without any changes.
   
   This is the crucial step: creating the interface automatically creates a routing table entry for the 1.1.1.57/29 network, so packets from CAM to NY will be sent to the NY firewall, which is exactly what we want
   - set the default gateway to be the CAM live router (192.0.2.1) so that traffic for exterior sites can still get out
   - connect the extra router into the network as shown. (It will have no effect until other components are changed.)

2. **Configure the NY firewall:**
   - private (LAN) IP address = 10.7.7.58, netmask = 255.255.255.0 (or whatever IP address range you want to use in NY)
   - public (WAN) IP address = 1.1.1.58 and netmask = 255.255.255.248 (or whatever your NY ISP has allocated)
   - default gateway = extra router (1.1.1.57), so that packets can be routed between the NY and CAM networks.

3. **Configure a small NY test LAN**
   Set up a machine on the test LAN, so we can **ping**, etc. and check out some of the rules, and ensure we have VPN connectivity, etc: IP address = 10.7.7.39, netmask = 255.255.255.0, default gateway = 10.7.7.58.

4. **configure the live, CAM network use the extra router**
   Only when we do this is anything (apart from the test net) affected.
   - we set the default gateway on the CAM firewall = extra router (192.0.2.2) instead of the CAM router. This allows traffic from the CAM network to route to the NY network.

Important: this works only because we're using NAT on the CAM LAN – all the LAN PCs use the *inside* interface of the CAM firewall as their default gateway. If you're not using NAT, their default gateway is almost certainly the live CAM firewall (192.0.2.1) and changing just the firewall's default gateway won't do what you need. You *could* change all the LAN PCs' default gateways manually, but you can do 99% of what you need by setting up a test PC on the CAM LAN, and set its default gateway explicitly = extra router (192.0.2.2). Then you can test connectivity and VPN between it and the NY LAN.

To remove the test network when you're finished, change the default gateway on the CAM firewall back to be the CAM live router (192.0.2.1) and physically disconnect the extra router, test network, etc.

# Summary

- VPN secures traffic between:
  - two sites ("gateway implementation")
  - or (rarely) between two remote PCs ("host or client implementation")
  - or between a site and a remote PC
- most VPN systems use the IPsec IP security protocol
- IPsec uses the ESP protocol to encrypt/authenticate traffic, or the AH protocol if only authentication is needed. Encryption prevents an eavesdropper from reading the traffic, and prevents a hacker modifying the data without you knowing
- ESP and AH can each support many different algorithms for encryption and authentication
- both ends of the VPN "tunnel" must somehow obtain the encryption/authentication keys before they can exchange data over the tunnel
- IPsec supports two types of key management:
  1. manual keying. The administrators at both ends enter the keys manually (having agreed what keys to use beforehand, e.g. by phone or e-mail). Manual keying is easier to set up, but not so secure – if an encryption key is broken, all past and future traffic can be read
  2. automatic keying using IKE. Before sending any data across the tunnel, the ends automatically negotiate the keys to use. Over the lifetime of the VPN tunnel they may periodically "re-key," i.e. re-negotiate new keys to use. This can provide "perfect forward secrecy:" even if a hacker breaks one set of keys, they still can't read data encrypted with earlier or later keys. IKE is more complicated to configure than manual keying
- the VPN system on a dial-up laptop can contain all the keys, etc. necessary to connect into the HQ office LAN. To protect against theft of a laptop you can use an extra layer of authentication and require the laptop user to logon when they connect in. You can use a RADIUS server or other authentication server on the LAN to implement this.

## What's next?

Nothing, apart from the Epilog – you’ve reached the end!

## Notes and further reading

- Kaufman, Perlman and Spincer's *Network Security: Private Communication in a Public World* (2002, Prentice Hall PTR)

Recently there have been several surveys of how organizations' wireless LANs have been accessible to anyone nearby on the street outside. (Finding accessible networks is known in the hacker world as *war-driving*, by analogy with the "war-dialing" of phone-preaks in the 1960s and 1970s. To avoid such problems, some vendors suggest that you protect all wireless networking users – even those inside your building – with VPN. See:
