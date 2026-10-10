website, the machine's CPU isn't likely to break a sweat. The bottleneck is the Internet connection itself.

# ## Begin with Rules That Block Traffic on High Ports

As the example in Chapter 4 demonstrated, the bulk of the rules are antispoofing rules, or rules blocking traffic on specific high ports (such as NFS or X Windows). These types of rules must come before the rules allowing traffic to specific services. Obviously, the FTP data channel rules must come near the end of the rule list, even though you'd want the rules to be near the top of the list because FTP transfers tend to be large.

# ## Use the State Module for ESTABLISHED and RELATED Matches

Using the state module's ESTABLISHED and RELATED matches essentially allows for moving all rules for ongoing exchanges to the head of the chains, as well as eliminating the need for specific rules for the server half of a connection. In fact, bypassing filter matching for ongoing, recognized, previously accepted exchanges is one of the two primary purposes of the state module.

The state module's second primary purpose is to serve a firewall-filtering function. Connection-state tracking allows the firewall to associate packets with ongoing exchanges. This is particularly useful for connectionless, stateless UDP exchanges.

# ## Consider the Transport Protocol

The transport protocol that the service runs over is another factor. In a static firewall, the overhead of testing every single incoming packet against all the spoofing rules is a big loss.

# ### TCP SERVICES: BYPASS THE SPOOFING RULES

Even without the state module, for TCP-based services, the rule for the remote server half of a connection can bypass the spoofing rules. The TCP layer will drop incoming spoofed packets with the ACK bit set because the packet won't match any of the TCP layer's established connection states.

The remote client half of a rule pair must follow the spoofing rules, however, because the typical client rule covers both the initial connection request and the ongoing traffic from the client. If the SYN and ACK flags are tested for individually, the rules testing for the ACK flag in packets arriving from remote clients can bypass the spoofing tests. The spoofing tests must apply to only the initial SYN request.