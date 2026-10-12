
## Is the WEP stream cipher good enough?

WEP uses the RC4 encryption algorithm, which is known as a stream cipher. Such an algorithm works by taking a short secret key and generating an infinite stream of pseudorandom bits. Before sending the data, the sending station performs an exclusive-OR operation between the pseudorandom bits and the bits representing the data packet, which results in a 1 when two bits are different and 0 if they are the same. The receiver has a copy of the same secret key, and generates an identical stream of pseudorandom bits — and performs an identical exclusive-OR operation between this pseudorandom stream and the received bits. Doing so regenerates the original, unencrypted data packet.

Such a method of stream cipher has a few problems. If a bit is flipped (from a 0 to 1 or vice versa) in the encrypted data stream, then the corresponding bit is flipped in the decrypted output — this can help an attacker derive the encryption key. Also, an eavesdropper who intercepts two encoded messages that were encoded with the same stream can generate the exclusive-OR of the original messages. That knowledge is enough to mount attacks that can eventually break the encryption.

To counter these weaknesses, WEP uses some defenses:

- **Integrity Check (IC) Field** — To make sure that data packets are not modified in transit, WEP uses an Integrity Check field in each packet.
- **Initialization Vector (IV)** — To avoid encrypting two messages with the same key stream, WEP uses a 24-bit initialization vector (IV) that augments the shared secret key to produce a different RC4 key for each packet. The IV itself is also included in the packet.

Experts say that both these defenses are poorly implemented, making WEP ineffective. IC and IV have two main problems:

- **The Integrity Check field** is implemented by using a checksum algorithm called 32-bit cyclic redundancy code (CRC-32); that checksum is then included as part of the data packet. Unfortunately, an attacker can flip arbitrary bits in an encrypted message and correctly adjust the checksum so the resulting message appears valid.
- **The 24-bit IV** is sent in the clear (unencrypted). This means that there are only 2^24 possible initialization vectors (no big challenge for a fast machine), and they have to be reused after running through all of them. In other words, after sending 2^24 or 16,777,216 packets, the IV has to be repeated. The number might sound like a lot, but consider the case of a busy access point that sends 1,500-byte packets at a rate of 11 Mbps. Each packet has 8 × 1,500 = 12,000 bits. That means each second the access point sends 11,000,000/12,000 = 916 packets. At that rate, the access point sends 16,777,216 packets in 16,777,216/916 = 18,315 seconds or 5 hours. That means the IV is reused after 5 hours, and the time may be less than that because many messages are smaller than 1,500 bytes. Thus, an attacker has ample opportunities to collect two encrypted messages that are encrypted with the same key stream — and perform statistical attacks (which amount to trying the possible “combinations” really fast) to decrypt the message.

## Understanding Wired Equivalent Privacy (WEP)

The 802.11 standard includes the Wired Equivalent Privacy (WEP) for protecting wireless communications from eavesdropping. WEP relies on a 40-bit or 104-bit secret key that is shared between a mobile station (such as a laptop with a wireless Ethernet card) and an access point (also called a base station). The secret key is used to encrypt data packets before they are transmitted, and an integrity check is performed to ensure that packets are not modified in transit. The 802.11 standard does not explain how the shared key is established. In practice, most wireless LANs use a single key that is shared between all mobile stations and access points. Such an approach, however, does not scale very well to an environment such as a college campus because the keys are shared with all users — and you know how it is if you share a "secret" with hundreds of people. That’s why WEP is typically not used on large wireless networks such as the ones at universities. In such wireless networks, you have to use other security approaches such as SSH (Secure Shell) to log in to remote systems. WEP, however, is good to use on your home wireless network.

WEP has its weaknesses, but it’s better than nothing. You can use it in smaller wireless LANs where sharing the same key among all wireless stations is not an onerous task.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_351_0.png)

There is work underway to provide better security than WEP for wireless networks. The 802.11i standard, now under development, would use public-key encryption with digital certificates — along with an authentication, authorization, and accounting done on a RADIUS (Remote Authentication Dial-In User Service) server — to provide better security for wireless Ethernet networks.

While the 802.11i standard is in progress, the Wi-Fi Alliance — a multivendor consortium that supports Wi-Fi — is publishing an interim specification called Wi-Fi Protected Access (WPA) that’s a precursor to 802.11i. WPA will replace the existing WEP standard and improve security by making some changes. For example, unlike WEP (which uses fixed keys), the WPA standard uses Temporal Key-Integrity Protocol (TKIP), which generates new keys for every 10K of data transmitted over the network. This makes WPA more difficult to break. You may want to consider WPA in the interim while work progresses on 802.11i.

## Setting Up the Wireless Hardware

To set up the wireless connection, you need a wireless access point and a wireless network card in each PC. You can also set up an ad hoc wireless network among two or more PCs with wireless network cards, but that would be a standalone wireless LAN among those PCs only. In this section, I focus on the scenario where you want to set up a wireless connection to an established LAN that has a wired Internet connection through a cable modem or DSL.

In addition to the wireless access point, you would also need a cable modem or DSL connection to the Internet, along with a NAT router/hub, as described in the previous sections. Figure 3-1 shows a typical setup for wireless Internet access through an existing cable modem or DSL connection.

As Figure 3-1 shows, the LAN has both wired and wireless PCs. In this example, a cable or DSL modem connects the LAN to the Internet through a NAT router/hub. Laptops with wireless network cards connect the LAN through a wireless access point attached to one of the RJ-45 ports on the hub. To connect desktop PCs to this wireless network, you can use a USB wireless network card (which connects to a USB port).

If you have not yet purchased a NAT router/hub for your cable or DSL connection, consider buying a router/hub that has a built-in wireless access point.

![](img/a7eec43a54473e95dc5ea333fecf1bd7_352_0.png)

![](img/a7eec43a54473e95dc5ea333fecf1bd7_352_1.png)

Figure 3-1:
Typical connection of a mixed wired-and-wireless Ethernet LAN to the Internet.

## Configuring the Wireless Access Point

Configuring the wireless access point involves the following tasks:

- Setting a name for the wireless network (the technical term is ESSID).
- Setting the frequency or channel on which the wireless access point communicates with the wireless network cards. The access point and the cards must use the same channel.
- Deciding whether to use encryption.
- If encryption is to be used, setting the number of bits in the encryption key and the value of the encryption key. Twenty-four bits of the encryption key are internal to the access point; you specify only the remaining bits. Thus, for 64-bit encryption, you have to specify a 40-bit key, which comes to 10 hexadecimal digits (a hexadecimal digit is an integer from 0 through 9 or a letter from A through F). For a 128-bit encryption key, you specify 104 bits, or 26 hexadecimal digits.
- Setting the access method that wireless network cards must use when connecting to the access point. You can opt for either open access or shared key. The open-access method is typical (even when using encryption).
- Setting the wireless access point to operate in infrastructure (managed) mode (because that's the way you should connect wireless network cards to an existing Ethernet LAN).

![](img/a7eec43a54473e95dc5ea333fecf1bd7_353_0.png)

The exact method of configuring a wireless access point depends on make and model; the vendor provides instructions to configure the wireless access point. You would typically work through a graphical client application on a Windows PC to do the configuration. If you enable encryption, make note of the encryption key; you have to specify that same key for each wireless network card.

## Configuring Wireless Networking

On your Red Hat Linux laptop, the PCMCIA or PC Card manager should recognize the wireless network card and load the appropriate driver for the card. The wireless network card is treated like another Ethernet device — assign it a device name such as eth0 or eth1. If you already have an Ethernet card in the laptop, that card gets the eth0 device name, and the wireless PC card becomes the eth1 device.

You do have to configure certain parameters to enable the wireless network card to communicate with the wireless access point. For example, you have
