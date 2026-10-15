
![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_170_0.png)

## Link Establishment Phase

LCP provides the link establishment phase. The connection is established with the bare minimum configuration options to bring the link up. Neither peer in the process is aware of particular options supported by the other—with the exception of authentication protocol selection. Should authentication be determined (negotiated) during the link establishment phase, the type of authentication will be determined (negotiated) during the link establishment phase.

LCP is defined in RFC 1661 with some added capabilities in RFC 1570, “PPP LCP Extensions.” The LCP packet is made up of the LCP header and data and is encapsulated within the PPP packet as shown in Figure 7.2.

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_170_1.png)

The LCP header includes an LCP code that identifies the messaging type, which could be a rejection to a particular option request. The LCP codes are listed in Table 7.2.

### Table 7.2 LCP Protocol Codes

| Value | Message |
| --- | --- |
| 1 | Configure-Request |
| 2 | Configure-Ack |
| 3 | Configure-Nak |
| 4 | Configure-Reject |
| 5 | Terminate-Request |
| 6 | Terminate-Ack |
| 7 | Code-Reject |
| 8 | Protocol-Reject |
| 9 | Echo-Request |
| 10 | Echo-Reply |
| 11 | Discard-Request |

The data field is determined by the LCP code. This means that each message has a particular data or payload portion that matches the message.

After the link establishment phase has been accepted by both parties, the authentication phase is entered.

## Authentication Phase

Prior to accepting any option parameters, the nodes can authenticate one another. Although not required, there is no good reason to not use authentication. This is unless another form of authentication is deemed adequate, such as caller ID. Once both peers are satisfied with any required authentication, the network layer protocol phase is entered. (Most sites only have the central remote access server authenticate the remote site; however, authentication can be supported in both directions regardless of which node initiated the session.)

PPP supports two authentication methods: Password Authentication Protocol (PAP) and the Challenge Handshake Authentication Protocol (CHAP).

PAP is a simple username and password mechanism whereby the node sends the username and password in plain text. The user name and password are accepted or rejected by the remote node.

CHAP uses a more complicated 3-way handshake without sending clear text usernames or responses: challenge, response, and acknowledgement.

The node wishing to authenticate the remote host will send a challenge based on a secret phase that is known to itself and that also should be known by the remote node. The remote node uses the challenge and the secret phase with a hash function to compute the response. The response is then sent, and the node checks the response to ensure it is the same calculated response it computes itself and, should it match, acknowledges the authentication and allows the connection to continue.

Unlike PAP, CHAP never sends the secret phase, not even in encrypted form.

## Network Layer Protocol Phase

The Network Control Protocol (NCP) determines the appropriate options for the protocols being supported. Each protocol supported by a node will have an NCP for the particular protocol. In addition, these NCPs can run in parallel. For example, IP and IPX options can be negotiated at the same time. Layer 3 traffic can be passed at this point within the phase, assuming the particular protocol was negotiated.

For IP over PPP, RFC 1172, "The PPP Internet Protocol Control Protocol (IPCP)" defines the standard for IP NCP.

IPCP uses the LCP packet format. However, only codes 1 through 7, shown in Table 7.3, are valid.

### Table 7.3 IPCP Protocol Codes

| Value | Message |
| --- | --- |
| 1 | Configure-Request |
| 2 | Configure-Ack |
| 3 | Configure-Nak |
| 4 | Configure-Reject |
| 5 | Terminate-Request |
| 6 | Terminate-Ack |
| 7 | Code-Reject |

To distinguish IPCP packets from LCP, the protocol field in the PPP header is set to 0x8021.

In addition to determining that IP is supported on the link, the network layer protocol phase uses specifics of IPCP to determine the IP address of the local IP address of the link and whether compression should be used.

Although the IP address must not be determined with IPCP, most implementations of PPP allow the administrator to determine which IP address is required. Most sites require that the central remote access server provide the IP address to ensure proper routing within the network.

## Link Termination Phase

Under ideal conditions, the link termination phase is signaled end-to-end using PPP terminate packets; however, the link termination phase also can be caused by a loss of carrier or an immediate shutdown by the system administrator.

It is interesting to note that although the states seem very sequential, a state can be entered in the "middle" of a session, which would be during the network layer protocol state. For example, authentication could be requested again after having already authenticated once. This is represented by the arrows pointing the various states in Figure 7.1.
