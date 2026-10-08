# Chapter 16. iptables

+   - --log-options — Any options set in the header of a IP packet is logged.
- --log-prefix — Places a string of up to 29 characters before the log line when it is written. This is useful for syslog filters for use in conjunction with packet logging.
- --tcp-options — Any options set in the header of a TCP packet are logged.
- --tcp-sequence — Writes the TCP sequence number for the packet in the log.

REJECT — Sends an error packet back to the remote system and drops the packet.
The REJECT target accepts --reject-with <type> (where <type> is the rejection type) which allows more detailed information to be sent back with the error packet. The message portunreachable is the default <type> error if no option is used. For a full list of <type> options that can be used, see the iptables page.
Other target extensions, including several that are useful for IP masquerading using the nat table or with packet allocation using the mangle table, can be found in the iptables page.

# 16.3. Listing Options

The default list command, iptables -L, provides a basic overview of the filter table's current chains. Additional options provide more information:

+   -v — Display verbose output, as the number of packets and bytes each chain has, the number of packets and bytes each chain matches, and interfaces to a packet rule.
-x — Expands numbers into their exact values. By basis, the number of packets and bytes seen by a chain or rule may be abbreviated with K (thousands), M (millions), and G (billions) at the end of the number. This option forces the full number to be displayed.
-n — Displays IP addresses and port numbers in numeric format, rather than the default hostname and network service format.
- --line-numbers — Lists rules in each chain next to their numeric order in the chain. This option is useful when attempting to delete a specific rule in a chain, or to locate where to insert a rule within a chain.
- -t — Specifies a table.

# 16.4. Storing iptables Information

Rules created with the iptables command are stored in memory. If the system is restarted after setting up iptables rules, they will be lost. For netfilter rules to persist through system reboot, they need to be saved. To do this, in root as you:

```
/sbin/service iptables save
```

This executes the iptables init script, which runs the /sbin/iptables-save program and writes the current iptables configuration to the /etc/sysconfig/iptables. This file should only be readable by root.

The next time the system boots, the iptables init script will recall the rules saved in /etc/sysconfig/iptables by using the /sbin/iptables-restore command.

While is always a good idea to test a new iptables rule before committing it to the /etc/sysconfig/iptables file, it is possible to copy iptables rules into this file from another