
## Chapter 16. iptables

### 16.3.5.2. UDP Protocol

These match options are available for the UDP protocol (-p udp):

- --dport — Specifies the destination port of the UDP packet, using the service name, port number, or range of port numbers. The --destination-port match option is synonymous with --dport. Refer to the --dport match option in 16.3.5.1 TCP Protocol for ways to use this option.
- --sport Specifies the source port of the UDP packet, using the service name, port number, or range of port numbers. The --source-port match option is synonymous with --sport. Refer to the --sport match option in 16.3.5.1 TCP Protocol for ways to use this option.

### 16.3.5.3. ICMP Protocol

These match options are available for the Internet Control Message Protocol (ICMP) (-p icmp):

- --icmp-type — Sets the name or number of the ICMP type to match with the rule. A list of valid ICMP names can be seen by typing the iptables -p icmp -h command.

### 16.3.5.4. Modules with Additional Options

Additional match options are available through modules loaded by the iptables command. To use a match option, load the module by name using the -m option, such as -m <module-name> (replacing <module-name> with the name of the module).

A large number of modules are available by default. It is possible to create your own modules to provide additional match functionality.

Many modules exist, but only the most popular are discussed here.

- limit Allows limit to be placed on how many packets are matched to a particular rule. This is especially beneficial when loading rule matches so that a flood of matching packets will not fill up the system log with repetitive messages or use system resources.
The limit module enables the following options:
- --limit — Sets the number of matches for a particular range of time, specified with a number and time modifier in a <number>/<time> format. For example, using --limit 5/hour only lets a rule match five times in a single hour
If a number and time modifier are not used, the default value of 3/hour is assumed. Sets a limit on the number of packets to match a rule at one time. This option should be used in conjunction with the --limit option, and it accepts a number to set the burst threshold.
If no number is specified, only five packets are initially to match the rule.

- state module — Enables state matching.
The state module enables the following options:
- --state — match a packet with the following connection states:
- ESTABLISHED — The matching packet is associated with other packets in an established connection.
- INVALID — The matching packet cannot be tied to a known connection.
- NEW — The matching packet is either creating a new connection or is part of a two-way connection not previously seen.
- RELATED — The matching packet is starting a new connection related in some way to an existing connection.

These connections can be used in combination with one another by separating them with commas, such as `-m state --state INVALID, NEW`

- mac module — Enables hardware MAC matching.
- --mac-source — Matches a MAC address of the network interface card that sent the packet. To exclude a MAC address from a rule, place an exclamation point (!) after the `--mac-source match option.

The `mac` module enables the following option:

View other match options available through modules, refer to the `iptables` man page.

### 16.3.6. Target Options

Once a packet has matched a particular rule, the rule can direct the packet to a number of different targets that decide its fate finally. Each chain has a default target, which is used if none of the rules on that chain match a packet or none of the rules which the packet specify a target.

The following are standard targets:

- `<user-defined-chain>` — Replace `<user-defined-chain>` with the name of a user-defined chain within the target.
- ACCEPT — Allows the packet to successfully move to its destination or another chain.
- DROP — Drops the packet without responding to the requester. The system that sent the packet is not notified of failure.
- QUEUE — The packet is queued for handling by a user-space application.
- RETURN — Stops the packet against rules in the current chain. If the packet with a `RETURN` matches a rule in a chain called from another, the packet is returned to the first chain where it left off. If the `RETURN` is used on a built-in chain and the packet cannot move to its previous chain, the default target for the current chain decides what to take.

In addition to these standard targets, other targets may be used with extensions `target modules`. For more information about match options, see Section 16.3.5.4 *Modules with Additional Match Options*.

There are many extended modules, which of most only apply to specific targets or situations. A couple of the most popular target modules included by default in Red Hat Linux:

- LOG — Logs all packets that match this rule. Since the packets are logged by the kernel, the `/etc/syslog.conf` file defines where these log entries are written. By default, they are placed in `/var/log/messages` file.
- --log-level — Sets the priority level of a logging event. A list of priority levels can be found in the `syslog.conf` man page.

Various options can be used after the `LOG` target to specify the level of a logging event:

- --log-options — Any options set in the header of a IP packet is logged.
- --log-prefix — Places a string of up to 29 characters before the log line when it is written. This is useful for syslog filters for use in conjunction with packet logging.
- --tcp-options — Any options set in the header of a TCP packet are logged.
- --tcp-sequence — Writes the TCP sequence number for the packet in the log.

REJECT — Sends an error packet back to the remote system and drops the packet.
The REJECT target accepts --reject-with <type> (where <type> is the rejection type) which allows more detailed information to be sent back with the error packet. The message port unreachable is the default <type> error if no option is used. For a full list of <type> options that can be used, see the iptables page.
Other target extensions, including several that are useful for IP masquerading using the nat table or with packet allocation using the mangle table, can be found in the iptables page.

### 16.3. Listing Options

The default list command, iptables -L, provides a basic overview of the filter table's current chains. Additional options provide more information:

- -v — Display verbose output, as the number of packets and bytes each chain has, the number of packets and bytes each chain matches, and interfaces to a packet rule.
- -x — Expands numbers into their exact values. By basis, the number of packets and bytes seen by a chain or rule may be abbreviated with K (thousands), M (millions), and G (billions) at the end of the number. This option forces the full number to be displayed.
- -n — Displays IP addresses and port numbers in numeric format, rather than the default hostname and network service format.
- --line-numbers — Lists rules in each chain next to their numeric order in the chain. This option is useful when attempting to delete a specific rule in a chain, or to locate where to insert a rule within a chain.
- -t — Specifies a table.

### 16.4. Storing iptables Information

Rules created with the iptables command are stored in memory. If the system is restarted after setting up iptables rules, they will be lost. For netfilter rules to persist through system reboot, they need to be saved. To do this, in root as you:

```
/sbin/service iptables save
```

This executes the iptables init script, which runs the /sbin/iptables-save program and writes the current iptables configuration to the /etc/sysconfig/iptables. This file should only be readable by root.

The next time the system boots, the iptables init script will recall the rules saved in /etc/sysconfig/iptables by using the /sbin/iptables-restore command.

While is always a good idea to test a new iptables rule before committing it to the /etc/sysconfig/iptables file, it is possible to copy iptables rules into this file from another
