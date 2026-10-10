Chain test (refcnt = 0):

| | |
| --- | --- |
| # |  |
| 0 | O DENY icmp ----- 0xFF 0x00 pppO |
| | | |
| | | |
| localNet/24 | | anywhere | any |

**Setting Policy** In the “Specifying a Target” section earlier in this chapter, we glossed over what happens when a packet hits the end of a built-in chain when we discussed how a packet walks through chains. In this case, the policy of the chain determines the fate of the packet. Only built-in chains (input, output, and forward) have policies, because if a packet falls off the end of a user-defined chain traversal resumes at the previous chain.

The policy can be any of the first four special targets: ACCEPT, DENY, REJECT, or MASQ. MASQ is only valid for the forward chain.

It is also important to note that a RETURN target in a rule in one of the built-in chains is useful to explicitly target the chain policy when a packet matches a rule.

# Operations on Masquerading

There are several parameters you can tweak for IP Masquerading. They are bundled with ipchains because it’s not worth writing a separate tool for them (although this will change).

The IP Masquerading command is -M, and it can be combined with -L to list currently masqueraded connections or with -S to set the masquerading parameters.

The -L command can be accompanied by -n (show numbers instead of hostnames and port names) or -v (show deltas in sequence numbers for masqueraded connection, just in case you care).

The -S command should be followed by three timeout values, each in seconds: for TCP sessions, for TCP sessions after a FIN packet, and for UDP packets. If you don’t want to change any of these values, simply give a value of 0.

The default values are listed in /usr/include/net/ipmasq.h, currently 15 minutes, 2 minutes, and 5 minutes respectively.

The most common value to change is the first one, for FTP. (See the “FTP Nightmares” section later in this chapter.)

Note the problems with setting masquerading timeouts listed in the “Common Problems” section later in this chapter.