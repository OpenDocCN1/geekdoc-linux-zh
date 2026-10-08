# ICMP REDIRECT BOMBS

ICMP redirect message Type 5 tells the target system to change its in-memory routing tables in favor of a shorter route. Redirects are sent by routers to their adjacent hosts. Their intention is to inform the host that a shorter path is available (that is, the host new router is on the same network, and the new router is the original that would route the packet to its next hop).

Redirect arrive on an almost-daily basis. They rarely originate from the adjacent router. For residential or business sites connected to an ISP, it's very unlikely that your adjacent router will generate a redirect message.

If your host uses static routing and honors redirect messages, it's possible for some-one to fool your system into thinking that a remote machine is one of your local machines or one of your ISP's machines, or even to fool your system into forwarding all traffic to some other remote host.

# DENIAL-OF-SERVICE ATTACKS AND OTHER SYSTEM RESOURCES

Network connectivity isn't the only concern in DoS attacks. Here are some examples of other areas to keep in mind while configuring your system:

+   - Your filesystem can overflow if your system is forced to write enormous numbers of messages to the error logs, or if your system is flooded with many copies of large email messages. You might want to configure resource limits and set up a separate partition for rapidly growing or changing filesystems.

# EMAIL DENIAL-OF-SERVICE EXPLOITS

For a description of a DoS exploit using email, see "Email Bombing and Spamming," at http://www.cert.org.

+   - System memory, process table slots, CPU cycles, and other resources can be exhausted by repeated, rapid invocations of network services. You can do little about this other than set any configurable limits for each individual service, enabling SYN cookies, and denying rather rejecting packets to unsupported service ports.