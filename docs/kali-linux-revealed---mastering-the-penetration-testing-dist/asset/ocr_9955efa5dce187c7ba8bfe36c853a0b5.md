![](bbox=[0.257, 0.049, 0.742, 0.296])

**Figure 7.1** How Netfilter Chains are Called

Each chain is a list of rules; each rule is a set of conditions and an action to perform when the conditions are met. When processing a packet, the firewalls scans the appropriate chain, one rule after another, and when the conditions for one rule are met, it jumps (hence the -j option in the commands) to the specified action to continue processing. The most common behaviors are standardized and dedicated actions exist for them. Common one of these actions (barring an exception mentioned below) interrupts the processing of the chain, since the packet fates is already sealed (barring an exception mentioned below). Listed below are the Netfilter actions.

+   - ACCEPT: allow the packet to get on its way.
- REJECT: reject the packet with an Internet control message protocol (ICMP) error packet (the --reject-with type option of iptables determines the type of error to send).
- DROP: delete (ignore) the packet.
- LOG: log (via syslog) a message with a description of the packet. Note that this action does not interrupt processing, and the execution of the chain continues to the next rule, which is logging refused packets requires both a LOG and a REJECT/DROP command. Common parameters associated with logging include:

+   --log-level, with default value warning, indicates the syslog level.
-- --log-prefix allows specifying a text prefix to differentiate between logged messages.
-- --log-tcp-sequence, --log-tcp-options, and --log-ip-options extract data to be integrated into the message: respectively, the TCP sequence number, TCP options, and IP options.

+   - ULOG: log a message via slog, which can be better adapted and more efficient than syslog for handling large numbers of messages; note that this action, like LOG, also returns processing to the next rule in the calling chain.
- chain_name: jump to the given chain and evaluate its rules.