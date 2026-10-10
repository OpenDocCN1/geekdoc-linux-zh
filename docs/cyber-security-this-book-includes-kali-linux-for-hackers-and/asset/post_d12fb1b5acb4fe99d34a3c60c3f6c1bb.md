
## Cryptography Used to Maintain Communications Security

There are two types of protection available depending on the level of communication that you would like to use. First, link encryption repeatedly encrypts and decrypts all information sent as part of data transmission, while end-to-end encryption only encrypts the internal information sent but not the packet header information that is necessary for routing.

### Link Encryption

As mentioned earlier, all data is encrypted in this type of data transmission with the exception of the data-link control information. As it moves along its route to the destination host, each router at a certain point decrypts the information in order to obtain header information for its destination and encrypts the information again.

As a person sending data over the internet, either by email or in which banking institutions have to communicate with their customers, then link encryption is preferred. This is because all data is encrypted and provides privacy and security. On the downside, all devices the data passes through must receive the key and key changes if necessary. Apart from this, the decryption of the packet at each routing point has to take place in order for it to move further along the route.

### End-to-End Encryption

In this type of encryption, encryption of the data is restricted to everything apart from packet headers and addresses. This makes it more susceptible to hackers who can gain more information about packets by sniffing or eavesdropping. Still, end-to-end encryption allows for users to have control over what gets encrypted or not. In addition, since there is no repeated decryption or encryption at each routing point, the performance of routing devices improves greatly. IPsec is one such example of end-to-end encryption.

## Actively Secure Network Components

There's an important reason why network components must be secured along with protecting data in transit. This is for the simple reason that if compromised, the information in the network can be easily accessed by attackers. In other words, both matters.

### Hardware

So, what do we mean by network components? This can be classified into five parts: hardware, transmission media, network access control devices, apart from endpoint security and content-distribution networks, which we will look at next.

### Modem

Serving as a portmanteau for modulator/demodulator, the modem gives remote users access to a network by means of an analog phone line. When the user sends an analog signal to the modem, it is converted to a digital signal that is usually sent to a server. As a result, when the server responds to the signal, the digital signal is converted back to analog and sent back to the remote user.

While this can prove to be useful for those who find themselves traveling on work, this type of access can give attackers a way in while security personnel are busy protecting the Internet gateway.

While not allowing modems to be placed on the network is a common approach to prevent threats, telephony firewalls are also used and monitor both incoming and outgoing analog calls. As a result, certain numbers can be used to make modem calls into the organization's phone exchange.

That said, the telephony firewall mentioned earlier is much like an IP firewall where it sits between the PSTN and the organization's telephone network.

### Bridges and Switches

Local area networks have been known to grow in size, which not only reduces bandwidth but reaches a point where the LAN cannot expand anymore.

Increasing the cable length and the size of the LAN will only increase attenuation. Is there a way to connect two LANs without reconfiguring both networks?

The common solution to this is called a Layer 2 device known as a bridge, which is responsible for filtering traffic between segments by virtue of their MAC Addresses. Also, they amplify the signal while also reducing the amount of unnecessary traffic flowing through each part of the network.

Unfortunately, despite being efficient, bridges do not prevent someone from any of the segments on the network from intercepting traffic. So, security must be taken seriously in the form of link-layer encryption and even access lists. This is particularly true for wireless bridges.

As for switches, they offer the same benefits as bridges do but are expensive. Put simply, they are multiport devices that LANs can connect to and also come with the additional benefit of increasing network bandwidth. That said, both bridges and switches can forward broadcasts to all segments in the network.

### Routers

The primary function of routers is to forward packets to another network by virtue of the IP address that is added in the packet it receives. Since routers maintain a certain view of the network they’re in by means of the routing table, they then decide which device on the network should receive this packet next. This is commonly known as the next hop. Of course, if the destination IP address is not located within its network, it forwards the packet to another router that is closer to its destination. One advantage of using a router is that it connects networks of different types through which you can send packets of data without any issues.

### Wireless Access Points

By definition, a wireless access point gives wireless devices access to a network. Divided into cells, this area can expand outside the secure area if wireless access point strength is not adjusted appropriately. Some of the strategies used here include shielding, noise transmission, and placing the access point itself to prevent attackers from accessing the network.

### Transmission Media

The importance of cables used in the design of a network cannot be overstated. Picking the right type of cable for the said network can determine whether the network succeeds in performing its function. Some of the aspects that must be taken into consideration when selecting cables are throughput, distance between devices, data sensitivity, and the environment.

As for the type of cables available for selection, they include shielded and unshielded twisted pair, coaxial cable, patch panel, and three types of fiber optic cables.

### Wired

As mentioned earlier, cables that you can select involve twisted pair and coaxial cables where copper wires are twisted together so as to prevent electromagnetic interference and crosstalk. Since this type is the most inexpensive, it is easily bent during installation. So, in order to resolve this, the shielded twisted pair cable is generally used, which adds an extra shield to protect the signal along with the usual protective jacket used. Of course, since it is more expensive and harder to bend when installing, this can prove to be disadvantageous, unless shielding the signal is the maximum priority.

As for coaxial cables, they protect a sizeable conductor which is then covered by a grounding braid of wire and which is separated by a non-conducting layer. In addition, a protective sheath is used to cover the entire cable. Since the coaxial cable is larger than twisted pair cables, it usually supports a larger bandwidth apart from being installed across larger distances. Intruders cannot monitor the signal while interference is blocked out by the superior protective sheath. Still, given how expensive it is, it is only used in specialized applications.

### Wireless

There are two types of wireless transmissions: radio waves and microwaves. Some applications that we have looked at in an earlier chapter to transmit wirelessly include Bluetooth, Infrared, Wi-Fi, and wireless transmission using satellites.

### Fiber

Even if cables continue to be used in fiber optic cables, the use of light replaces changing voltages when using copper cables. An LED or laser is used to direct the data, which turns on and off to send zeroes and ones. The receiver at the other end of the cable then interprets these bits and converts them back to the original signal.

Now, the faster the laser fluctuates, the greater the possibility of the light signal dispersing. For this, light strengtheners are used much like repeaters are. Three types of fiber optic cables are used: namely single-mode, multi-mode, and plastic optical fiber (POF).

## Network Access Control Devices

By definition, network access control devices generally inspect devices that want access to an organization’s network. Whether they already have malware on them, are missing security updates, among a host of other issues; this could affect the network as a whole and must be dealt with in real-time. Of course, the acceptable security standards that grant device access to the network have to be based on the organization’s security policy. Network access control devices (NAC) tend to act as an automated detection and response system that have been placed so as to prevent severe damage to a network or a data breach.

## Firewalls

Defined as a network device that controls traffic and that serves as a barrier between the Internet and a private network, a firewall is used to filter traffic based on rules set, which distinguishes between what the organization deems as malicious or authorized traffic.
