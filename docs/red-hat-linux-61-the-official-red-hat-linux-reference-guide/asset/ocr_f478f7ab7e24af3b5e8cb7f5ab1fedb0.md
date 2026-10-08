# Chapter 16. iptables

+   - NEW — The matching packet is either creating a new connection or is part of a two-way connection not previously seen.
- RELATED — The matching packet is starting a new connection related in some way to an existing connection.

These connections can be used in combination with one another by separating them with commas, such as `-m state --state INVALID, NEW`

+   - mac module — Enables hardware MAC matching.
- --mac-source — Matches a MAC address of the network interface card that sent the packet. To exclude a MAC address from a rule, place an exclamation point (!) after the `--mac-source match option.

The `mac` module enables the following option:

View other match options available through modules, refer to the `iptables` man page.

# 16.3.6. Target Options

Once a packet has matched a particular rule, the rule can direct the packet to a number of different targets that decide its fate finally. Each chain has a default target, which is used if none of the rules on that chain match a packet or none of the rules which the packet specify a target.

The following are standard targets:

+   - `<user-defined-chain>` — Replace `<user-defined-chain>` with the name of a user-defined chain within the target.
- ACCEPT — Allows the packet to successfully move to its destination or another chain.
- DROP — Drops the packet without responding to the requester. The system that sent the packet is not notified of failure.
- QUEUE — The packet is queued for handling by a user-space application.
-RETURN — Stops the packet against rules in the current chain. If the packet with a `RETURN` matches a rule in a chain called from another, the packet is returned to the first chain where it left off. If the `RETURN` is used on a built-in chain and the packet cannot move to its previous chain, the default target for the current chain decides what to take.

In addition to these standard targets, other targets may be used with extensions `target modules`. For more information about match options, see Section 16.3.5.4 *Modules with Additional Match Options*.

There are many extended modules, which of most only apply to specific targets or situations. A couple of the most popular target modules included by default in Red Hat Linux:

+   - LOG — Logs all packets that match this rule. Since the packets are logged by the kernel, the `/etc/syslog.conf` file defines where these log entries are written. By default, they are placed in `/var/log/messages` file.
- --log-level — Sets the priority level of a logging event. A list of priority levels can be found in the `syslog.conf` man page.

Various options can be used after the `LOG` target to specify the level of a logging event: