# FIGURE 21.1  
The path of a  
*filter* through the*

![](bbox=[0.27, 0.11, 0.9, 0.43])

**Checksum**  
Makes sure that the packet hasn’t been corrupted in some way. If it has, then it is denied.

**Sanity Check**  
Malformed packets can confuse the rule-checking code, so they are detected and discarded. For clarity, the sanity check is only shown before the *input* chain in Figure 21.1, but it actually is performed before traversing each firewall chain.

**input Chain**  
The *input* chain is the first chain that a packet is tested against. Unless the packet is denied or rejected, it is passed on.

**Demosquare**  
If the packet is a reply to a *masquerade* packet, the packet is *demosquare*s and passed directly on to the *output* chain. (*Note:* This applies only if you are using *IP masquerading*)

**Routing Decision**  
The destination of the packet is examined to see if it is headed toward a local process or needs to be forwarded to another machine. If the destination is a local process, the packet is sent to the *output* chain; otherwise, it is sent to the *forward* chain.