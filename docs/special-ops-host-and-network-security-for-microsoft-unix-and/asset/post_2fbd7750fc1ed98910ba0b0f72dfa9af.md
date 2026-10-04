
mitigate denial of service attacks as well. Although this may be a more expensive route than using the solution that came with your AP, if your wireless data is critical you may want to check out AirFortress or similar solutions.

## Additional Security Protocols

Going back to the "treat it like an Internet connection" theme, you can employ the same technologies used to secure data over the Internet on your wireless LAN. You're probably already familiar with VPNs for remote user access; they can also be used to grant 802.11 clients access and encrypt their data. Place the VPN server behind the AP like you would with a border router and the Internet. If you do not want to go through the trouble of a VPN system, see what your users actually need to access. See if these applications can be used over encrypted protocols such as SSL or SSH.

## Detecting 802.11 Attacks

Although 802.11 intrusion detection is still relatively new, there are a couple of entities offering IDS capabilities now. AirDefense Inc. (www.airdefense.net) offers an 802.11 IDS product that consists of remote wireless sensors and a central management server. The AirDefense system can look for common wireless attacks, rogue access points, or wireless clients, and it can also be used for monitoring wireless network performance.

AirDefense is the only common 802.11 IDS vendor still in business as of this writing. Many people are not putting much effort into detecting attacks on a medium that's accepted as being insecure. Rather they are deploying their familiar wired-network-based IDS systems in the demilitarized zone (DMZ) network that the access point itself is connected to.

## Security Checklist

- ** Firewall the wireless network: It's not an Internet connection, but you should treat it like one. Remember that a RF network is more public than the Internet in some ways, just more local. Place the AP itself in a DMZ so you can easily monitor and filter traffic from the wireless network. Do not directly connect the AP to the internal network and hope to rely on the built-in filtering capabilities used by any access point.
- ** Disable broadcast SSID: NetStumber is the most popular war-driving tool going now, probably because it requires no insight to get up and running. NetStumber also relies on one type of network discovery, luckily one that is easily disabled. Changing the default SSID gives the appearance of at least being able to configure the access point in terms of admin competency.
- ** Harden access points: Most access points come with an assortment of management services out of the box, and you probably won't need these on a day-to-day basis. Leaving these open and unsecured just gives attacker an easier route into your network. Having WEP and MAC ACLs are great, but not too useful if anyone can view and reconfigure them!
- ** Enable MAC address filtering: This is as far as a lot of networks in terms of security, it's not too effective since you can see the “pass-word” (MAC address) with any wireless sniffer, but it still makes an attacker spend time reconfiguring his MAC address. Usually the path of least resistance is the one followed by casual attackers, if you have a choice of trying to get into a network with MAC filtering and one without, they are probably going to the one lacking ACLs. 
- ** Enable WEP but don't rely on it: Yes, it can be cracked, but it's not something that's going to be done in five minutes every single time. An attacker will have to spend hours capturing traffic to execute a WEP cracking attack, and once again following the path of least resistance WEP’d networks are the last choice to attempt access to.
- ** Disable DHCP: If you disable DHCP, you at least make the attacker to obtain IP information and give a valid address before communicating with the internal network.
- ** Setup logging on the access point, if possible: Although you should be watching the DMZ behind like any other external connection, logging on the access point itself can give you some better 802.11-specific information that may be crucial in decoding attacks.
- ** Harden the wireless clients: Don't make the mistake of implementing layers upon layers of transport security but ignoring the end points. If you have enabled every security option available but gave your users wide-open Windows 2000 laptops, it's easier to break into a client system then spend time trying to bypass all of the other measures.
- ** Install a VPN**: You're probably already using a VPN for remote Internet access. It's trivial to put the AP's Ethernet side in a similar configuration as your users will already be familiar with the software and operation; Plus, since there's no need to retrain them on proprietary 802.11 solutions.
- ** Setup 802.1x**: 802.1x is the “official” solution for the meantime, but IEEE has a working group (802.11) dedicated to providing the next standard for 802.11 security. 802.1x is a temporary fix that vendors are latching on to for something to provide a modicum of security until 802.11i is standardized. 802.11i will incorporate most of the 802.1x concepts being used today.

## Chapter 15 • Wireless LANs: Discovery and Defense

## Summary

After reading this chapter, you can address the two major points of woe regarding 802.11 devices. Your first priority is going to be identification of the devices connected to your network, and then dealing with them. In most cases the easiest way to deal with the problem is to turn them off, but frequently business needs won't allow it. If the company demands 802.11 access, you can make sure they get that access securely. Although the current state of 802.11 does have more than its share of management duties to securely operate it, the IEEE is aware of the issues and is working to correct them. 802.11 should be a major improvement for WLAN security and ease of use. And many vendors are offering solutions that address these problems today. Be sure to do enough research when building your 802.11 discovery toolkit, and with the right tools you may find some other accounting systems in place on your network before you are able to use them to track down the MAC and IP addresses of rogue wireless devices. If you're running a multisite network that is geographically dispersed, it will be easier to search for 802.11 devices over the wired network. Although you won't find all of them, you should be able to find the bulk of the devices and less clutter to deal with when you actually do the detection via wireless. RF discovery of wireless networks is the only way to find all of the devices, but you will have to cover all of the devices.

## Links to Sites

- http://standards.ieee.org/getieee802/802.11: The 802.11 standards are available here.
- http://standards.ieee.org/getieee802/802.1x: The 802.1x standards are available here.
- www.hyperlinktech.com: Hyperlink carries equipment from major manufacturers as well.
- www.wirelesscentral.net: Wireless Central is a vendor with good reputation.
- www.talley.com: If you feel like getting some industrial grade 802.11 equipment or custom cables, Talley is your best choice.
- www.netstumbler.com: NetStummer.com is the unofficial NetStummer homepage as well as home to the NetStbler forums.
- www.80211-planet.com: 802.11 Planet is a site that covers 802.11 news and usually has good articles on new products.
- Kismet (www.kismetwireless.net/#mailing): Kismet offers two mailing lists, one for usage of the Kismet tool and one for general discussion of wireless security and vulnerabilities.
- DFW Wireless Users Group (www.dfwwireless.org/list.htm): The DFW Wireless Users Group promotes the acceptance and use of the IEEE 802.11b and 802.11a protocols. They have a main mailing list (at dfwwug@dfwwireless.org) and three Special Interest lists:
  - Wired and Wireless Security Issues: security@dfwwireless.org
  - Antenna Design and Construction: antenna@dfwwireless.org
  - Wireless Application Development: wapdev@dfwwireless.org
- Bugtraq (http://online.securityfocus.com): The Bugtraq list, which covers discussions of overall security, vulnerabilities, and patches, also includes information on wireless issues. Other SecurityFocus lists such as vuln-dev may also be helpful.
