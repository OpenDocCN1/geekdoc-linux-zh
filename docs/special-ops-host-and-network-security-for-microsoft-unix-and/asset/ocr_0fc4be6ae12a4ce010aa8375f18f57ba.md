mitigate denial of service attacks as well. Although this may be a more expensive route than using the solution that came with your AP, if your wireless data is critical you may want to check out AirFortress or similar solutions.

# Additional Security Protocols

Going back to the "treat it like an Internet connection" theme, you can employ the same technologies used to secure data over the Internet on your wireless LAN.You're probably already familiar with VPNs for remote user access; they can also be used to grant 802.11 clients access and encrypt their data.Place the VPN server behind the AP like you would with a border router and the Internet. If you do not want to go through the trouble of a VPN system, see what your users actually need to access. See if these applications can be used over encrypted protocols such as SSL or SSH.

# Detecting 802.11 Attacks

Although 802.11 intrusion detection is still relatively new, there are a couple of entities offering offering IDS capabilities now.AirDefense Inc. (www.airdefense.net) offers an 802.11 IDS product that consists of remote wireless sensors and a central management server.The AirDefense system can look for common wireless attacks, rogue access points, or wireless clients, and it can also be used for monitoring wireless network performance.

AirDefense is the only common 802.11 IDS vendor still in business as of this writing. Many people are not putting much effort into detecting attacks on a medium that's accepted as being insecure.Rather they are deploying their familiar wired-network-based IDS systems in the demilitarized zone (DMZ) network that the access point itself is connected to.

# Security Checklist

+   - Firewall the wireless network It's not an Internet connection, but you should treat it like one. Remember that a RF network is more public than the Internet in some ways, just more local. Place the AP itself in a DMZ so you can easily monitor and filter traffic from the wireless network. Do not directly connect the AP to the internal network and hope to rely on the built-in filtering capabilities used by any access point.