+   Don't execute new rules from the command line. Especially don't execute the default policy rules from the command line. You'll be cut off immediately if you're logged in using X Windows or remotely from another system, including a system on the LAN.

+   Execute the test script from the console if you can. Working in X Windows at the console might be more convenient, but the danger remains of losing access to X Windows locally. Be prepared for the possibility of needing to switch over to a virtual console to regain control. If you must use a remote machine to test the firewall script, use cron to automatically stop the firewall in case you get locked out. Be sure to remove the cron job before going live with the firewall, though.

+   Remember that flushing the rule chains does not affect the default policy currently in effect.

+   With a deny-by-default policy, always enable the loopback interface immediately.

+   When feasible, work on one service at a time. Add rules one at a time, or as input and output rule pairs if you aren't using the state module. Test as you go. This makes it much easier to isolate problem areas in the rules right away. Liberal use of the *echo* command within the firewall script can help to narrow down the location or rules that are being problematic within the script.

+   The first matching rule wins. Order is important. Use the *iptables list* commands as you go to get a feel for how the rules are ordered. Trace an imaginary packet through the list.

+   Remember that there are at least two independent chains: *INPUT* and *OUTPUT*. If the input rules look right, the problem might be in the *OUTPUT* chain, or vice versa.

+   If the script appears to hang, chances are good that a rule is referencing a symbolic host-name rather than an IP address before the DNS rules have been enabled. Any rule using a hostname instead of an address must come after the DNS rules, unless the host has an entry in the */etc/hosts* file.

+   Double-check the *iptables* syntax. It's easy to mistype the rule's direction, to reverse the source and destination addresses or ports, to switch upper- and lowercase-sensitive options, to use *-i* rather than *-o* when referring to an outgoing interface, or to precede an option with the wrong number of hyphens.

+   The three tables, *filter*, *nat*, and *mangle*, have different built-in chains. *filter* has *INPUT*, *OUTPUT*, and *FORWARD*. *nat* has *POSTROUTING* for SNAT, and *PREROUTING* and *OUTPUT* for DNAT. *mangle* has *PREROUTING*, *INPUT*, *FORWARD*, *POSTROUTING*, and *OUTPUT*.

+   The various built-in chains have differing input and output interface specifications. That is, an *INPUT* rule takes only an incoming interface. An *OUTPUT* rule takes only an outgoing interface. A *FORWARD* rule can take either, both, or no interface specifications. Source