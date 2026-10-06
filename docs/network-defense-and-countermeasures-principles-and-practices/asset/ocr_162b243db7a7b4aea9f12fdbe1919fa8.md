IPSec can also work in two modes. Those modes are transport mode and tunnel mode. Transport mode is the mode wherein IPSec encrypts the data, not the packet header. Tunneling mode does encrypt the header as the packet data.

There are other protocols involved in making IPSec work. IKE, or Internet Key Exchange, is used in setting up security associations in IPSec. A security association is formed by the two endpoints of the VPN tunnel, once decide how they are to encrypt and authenticate. For example, if they use AES for encrypting packets, what protocol will be used for key exchange, and what protocol will be used for authentication? All of these are negotiated between the endpoints, and decisions are stored in a security association (SA). This is accomplished via the IKE protocol. Internet Key Exchange (IKE and IKE2) is used to set up an SA by handling negotiation of protocols and algorithms and to generate the encryption and authentication keys to be used.

The Internet Security Association and Key Management Protocol (ISAKMP) provides a framework for authentication and key exchange. Once the IKE protocol sets the SA, then it is time to perform the authentication and key exchange.

That general overview of IPSec is sufficient for many security professionals. If you would like to know more details of the IPSec authentication and key exchange process, the following paragraphs provide that.

The first exchange between VPN endpoints establishes the basic security policy: the initiator proposes the encryption and authentication algorithms it is willing to use. The responder chooses the appropriate proposal and sends it to the initiator. The next exchange passes Diffie-Hellman public keys and other data. The Diffie-Hellman public keys will be used to encrypt the data sent between the two endpoints. The third exchange authenticates the ISAKMP session. This process is called main mode.

Once the IKE SA is established, IPSec negotiation (Quick Mode) begins.

Quick Mode IPSec negotiation, or Quick Mode, is similar to an Aggressive Mode IKE negotiation, except negotiation must be protected within an IKE SA. Quick Mode generates the SA for the data encryption and manages the key exchange for IPSec SA. In other words, Quick Mode uses the Diffie-Hellman keys exchanged in main mode, to continue symmetric keys that will be used for actual encryption in the VPN.

Aggressive Mode squeezes the IKE SA into three packets, with all data required for the SA passed by the initiator. The responder sends the proposal, key material, and ID, and authenticates the session in the next packet. The initiator replies by authenticating the session. Negotiation is quicker, and the initiator and responder ID pass in the class.

# SSL/TLS

A new type of uses SSL (Secure Socket Layer) or TLS (Transport Layer Security) to provide VPN access through a web portal. Essentially, TLS and SSL are the protocols used to secure websites. If you see a website beginning with HTTPS, then traffic to and from that website is encrypted using SSL or TLS.