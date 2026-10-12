| Action Parameter | Description |
| :--- | :--- |
| -I, --insert | Insert a new rule into a specific position in the list. |
| -L, --list | List all the rules in a chain. If the chain name is left off, list all rules in all chains. |
| -F, --flush | Flush all the rules out of a chain. |
| -Z, --zero | Zero out the packet counters for all chains. |
| -N, --new-chain | Create a new chain with the specified name. |
| -X, --delete-chain | Delete the chain with the specified name. |
| -P, --policy | Set the policy for the chain to the specified target. The policy of a chain describes what action to take if no rule matches the packet. The default policy for all chains is ACCEPT. |
| -M, --masquerading | Allows viewing of masqueraded connections. IP Masquerading is discussed in Chapter 16. |
| -S, --set | Set the timeouts for TCP, TCPFIN, and UDP packets. |
| -C, --check | Check a supplied packet against the given chain. This is useful mainly for debugging. |
| -h | Print a Help message describing parameters to ipchains. |

As you can see in Table 14-4, the ipchains action parameters can be expressed in two forms, either as a dash followed by a single capital letter, or two dashes followed by a descriptive word. Both will work, so use whichever you prefer. In the example in this chapter, I will use the abbreviated version.

Usually, we follow the action parameter with the rule chain to apply it to. Rules added to the input chain will be examined only when filtering network packets being received by the Linux box. Similarly, the output chain is examined only for packets being transmitted from the Linux box. The forward chain is examined only for network packets that are received by the Linux system but will be delivered to some other network system. Packet forwarding only occurs when your system is configured as a router.

After specifying a chain to act on, you may specify some optional parameters to define a rule. Table 14-5 lists the available optional parameters.