
## Is the WEP stream cipher good enough?

WEP uses the RC4 encryption algorithm, which is known as a *stream cipher*. Such an algorithm works by taking a short secret key and generating an infinite stream of pseudorandom bits. Before sending the data, the sending station performs an exclusive-OR operation between the pseudorandom bits and the bits representing the data packet, which results in a 1 when two bits are different and 0 if they are the same. The receiver has a copy of the same secret key and generates an identical stream of pseudorandom bits—and performs an identical exclusive-OR operation between this pseudorandom stream and the received bits. Doing so regenerates the original, unencrypted data packet.

Such a method of stream cipher has a few problems. If a bit is flipped (from a 0 to 1 or vice versa) in the encrypted data stream, the corresponding bit is flipped in the decrypted output, which can help an attacker derive the encryption key. Also, an eavesdropper who intercepts two encoded messages that were encoded with the same stream can generate the exclusive-OR of the original messages. That knowledge is enough to mount attacks that can eventually break the encryption.

To counter these weaknesses, WEP uses some defenses:

-   **Integrity Check (IC) field:** To make sure that data packets are not modified in transit, WEP uses an Integrity Check field in each packet.
-   **Initialization vector (IV):** To avoid encrypting two messages with the same key stream, WEP uses a 24-bit IV that augments the shared secret key to produce a different RC4 key for each packet. The IV itself is also included in the packet.

Experts say that both these defenses are poorly implemented, making WEP ineffective. IC and IV have two main problems:

1.  The Integrity Check field is implemented by using a checksum algorithm called 32-bit cyclic redundancy code (CRC-32); that checksum is then included as part of the data packet. Unfortunately, an attacker can flip arbitrary bits in an encrypted message and correctly adjust the checksum so that the resulting message appears valid.
2.  The 24-bit IV is sent in the clear (unencrypted). There are only $2^{24}$ possible initialization vectors (no big challenge for a fast machine), and they have to be reused after running through all of them. In other words, after sending $2^{24}$, or 16,777,216 packets, the IV is repeated. The number may sound like a lot, but consider the case of a busy access point that sends 1,500-byte packets at a rate of 11 Mbps. Each packet has $8 \times 1,500 = 12,000$ bits. That means each second the access point sends $11,000,000 / 12,000 = 916$ packets. At that rate, the access point sends 16,777,216 packets in $16,777,216 / 916 = 18,315$ seconds or 5 hours. That means the IV is reused after 5 hours, and the time may be less than that because many messages are smaller than 1,500 bytes. Thus an attacker has ample opportunities to collect two encrypted messages encrypted with the same key stream—and perform *statistical attacks* (which amount to trying the possible *combinations* really fast) to decrypt the message.

WEP has its weaknesses, but it's better than nothing. You can use it in smaller wireless LANs where sharing the same key among all wireless stations is not an onerous task.

![](img/792720823146d68f19fd50c99ebfce4b_316_0.png)

Work is underway to provide better security than WEP for wireless networks. In 2003, the Wi-Fi Alliance published a specification called **Wi-Fi Protected Access (WPA)** that replaced the existing WEP standard and improved security by making some changes. For example, unlike WEP, which uses fixed keys, the WPA standard uses **Temporal Key Integrity Protocol (TKIP)**, which generates new keys for every 10K of data transmitted over the network. This makes WPA more difficult to break. In 2004, the Wi-Fi Alliance introduced a follow-on to WPA called the **Wi-Fi Protected Access 2 (WPA2)** — the second generation of WPA security). WPA2 is based on the final **IEEE 802.11i** standard, which uses public key encryption with digital certificates and an authentication, authorization, and accounting **RADIUS** (**Remote Authentication Dial-In User Service**) server to provide better security for wireless Ethernet networks. WPA2 uses the **Advanced Encryption Standard (AES)** for data encryption.

## Setting Up the Wireless Hardware

To set up the wireless connection, you need a wireless access point and a wireless network card in each PC. You can also set up an ad hoc wireless network among two or more PCs with wireless network cards, but that is a standalone wireless LAN among those PCs only. In this section, I focus on the scenario in which you want to set up a wireless connection to an established LAN that has a wired Internet connection through a cable modem or DSL.

In addition to the wireless access point, you also need a cable modem or DSL connection to the Internet, along with a **NAT** router and hub, as described in the previous chapters of this minibook. Figure 3-1 shows a typical setup for wireless Internet access through an existing cable modem or DSL connection.

As Figure 3-1 shows, the LAN has both wired and wireless PCs. In this example, either a cable or DSL modem connects the LAN to the Internet through a NAT router and hub. Laptops with wireless network cards connect to the LAN through a wireless access point attached to one of the RJ-45 ports on the hub. To connect desktop PCs to this wireless network, you can use a USB wireless network card (which connects to a USB port).

![](img/792720823146d68f19fd50c99ebfce4b_316_1.png)

If you have not yet purchased a NAT router and hub for your cable or DSL connection, consider buying a router and hub that has a built-in wireless access point.

![](img/792720823146d68f19fd50c99ebfce4b_317_0.png)

> Figure 3-1: Typical connection of a mixed wired and wireless Ethernet LAN to the Internet.
>
> PCs in a local area network (LAN). Each PC must have a 10BaseT Ethernet card.

## Configuring the Wireless Access Point

Configuring the wireless access point involves the following tasks:

-   Setting a name for the wireless network. (The technical term is ESSID.)
-   Setting the frequency or channel on which the wireless access point communicates with the wireless network cards. The access point and the cards must use the same channel.
-   Deciding whether to use encryption.
-   If encryption is to be used, setting the number of bits in the encryption key and the value of the encryption key. For the encryption key, 24 bits are internal to the access point; you specify only the remaining bits. Thus, for 64-bit encryption, you have to specify a 40-bit key, which comes to 10 hexadecimal digits. (A hexadecimal digit is an integer from 0-9 or a letter from A-F.) For a 128-bit encryption key, you specify 104 bits, or 26 hexadecimal digits.
-   Setting the access method that wireless network cards must use when connecting to the access point. You can opt for either open access or shared key. The open-access method is typical (even when using encryption).
-   Setting the wireless access point to operate in infrastructure (managed) mode (because that's the way you connect wireless network cards to an existing Ethernet LAN).

The exact method of configuring a wireless access point depends on make and model; the vendor provides instructions to configure the wireless access point. You typically work through a graphical client application on a Windows PC to do the configuration. If you enable encryption, make note of the encryption key; you have to specify that same key for each wireless network card on your laptops or desktops.

### Configuring Wireless Networking

On your Linux laptop, the PCMCIA or PC Card manager recognizes the wireless network card and loads the appropriate driver for the card. Linux treats the wireless network card like another Ethernet device and assigns it a device name such as eth0 or eth1. If you already have an Ethernet card in the laptop, that card gets the eth0 device name, and the wireless PC Card becomes the eth1 device.

You do have to configure certain parameters to enable the wireless network card to communicate with the wireless access point. For example, you have to specify the wireless network name assigned to the access point, and the encryption settings must match those on the access point. You can usually configure everything using a graphical network configuration tool that's available for your Linux distribution — just select the Wireless Network option and fill in the requested information.

For example, in Fedora Core, choose System→Administration→Network from the GNOME desktop. Then click New on the toolbar to add a network device. You can then select the wireless device and get to a window where you can configure the wireless connection. (See Figure 3-2.) In particular, set the Mode to Managed, specify the name of the wireless network (the one
