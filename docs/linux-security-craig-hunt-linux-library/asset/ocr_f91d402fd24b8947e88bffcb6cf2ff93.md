tunneling, so all PPTP implementations rely on an existing (or bundled) PPP installation. While PPTP is primarily a packet encapsulation standard, it includes provisions to add connection security in two areas:

**Authentication** PPTP uses the authentication methods typically supported by PPP devices, both Microsoft and third-party devices such as PAP (Password Authentication Protocol), which is actually not secure at all, and CHAP (Challenge Handshake Authentication Protocol), including its Microsoft and Shiva variants.

**Privacy** Microsoft defined an optional encryption protocol to be used to protect the privacy of PPTP packet payload as it traverses an untrusted network. The Microsoft Point-to-Point Encryption (MPPE) protocol uses the RC4 encryption algorithm with the password as the seed to generate session keys for encryption.

A PPTP client (typically a Windows laptop or home user) works directly with the PPTP server at the edge of the corporate LAN, as illustrated in Figure 12.9.

![](bbox=[0.16, 0.51, 0.84, 0.81])

Once the PPTP client has established IP connectivity, typically over PPP to the ISP's nearest remote access server (RAS), it uses PPTP messages (which run on top of TCP) to establish a connection to the PPTP server and negotiate a set of tunnel addresses. The PPP process at the PPTP server assigns both a local and a remote address for the resulting PPP tunnel. After the user has authenticated successfully, a Generic Routing Encapsulation (GRE) session is built from end to end that sustains the PPP connection just negotiated. Only after