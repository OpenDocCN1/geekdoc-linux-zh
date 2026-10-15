# Table 7.2 LCP Protocol Codes

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

# Authentication Phase

Prior to accepting any option parameters, the nodes can authenticate one another. Although not required, there is no good reason to not use authentication. This is unless another form of authentication is deemed adequate, such as caller ID. Once both peers are satisfied with any required authentication, the network layer protocol phase is entered. (Most sites only have the central remote access server authenticate the remote site; however, authentication can be supported in both directions regardless of which node initiated the session.)

PPP supports two authentication methods: Password Authentication Protocol (PAP) and the Challenge Handshake Authentication Protocol (CHAP).

PAP is a simple username and password mechanism whereby the node sends the username and password in plain text. The user name and password are accepted or rejected by the remote node.

CHAP uses a more complicated 3-way handshake without sending clear text usernames or responses: challenge, response, and acknowledgement.

The node wishing to authenticate the remote host will send a challenge based on a secret phase that is known to itself and that also should be known by the remote node. The remote node uses the challenge and the secret phase with a hash function to compute the response. The response is then sent, and the node checks the response to ensure it is the same calculated response it computes itself and, should it match, acknowledges the authentication and allows the connection to continue.

Unlike PAP, CHAP never sends the secret phase, not even in encrypted form.