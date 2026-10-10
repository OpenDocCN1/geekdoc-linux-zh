security and user convenience is acceptable, and so on. The next section, “Designing Appropriate Rules,” presents some examples, but you must evaluate these, and probably modify them for your own needs.

# # Designing Appropriate Rules

With information on whether you’re configuring a router as a firewall or firewall rules on a client or server, knowledge of what protocols you need to pass, and so on, you should now have a general idea of how you want to configure your firewall rules. When you create a set of firewall rules, they’re expressed as an ordered list. If a packet matches the criteria specified by a rule, then the rule applies, and the packet is allowed through or rejected, as specified by the rule. Thus, the order of rules is extremely important; if an early rule allows, say, traffic destined to TCP port 80 from any IP address, then a subsequent rule that denies all traffic from a particular IP address won’t apply if that address sends data to a system’s TCP port 80. Also, early rules entail less processing overhead, so if a rule matches a great deal of traffic (such as return data from external servers), you may want to place it early in the firewall rule set.

# ## ipfw Syntax

Having a general idea of what sorts of rules you want to create is a necessary first step, but it’s not enough. The main key that’s missing is an understanding of the ipfw utility that creates packet filtering rules. This command’s syntax is extremely complex; consult its man page for details. A simplified ipfw syntax is as follows:

```
```
ipfw [-N] command [index] [action] [log] protocol addresses [options]
```
```

The meanings of the ipfw parameters are

+   - **-N** Normally, *ipfw* reports hosts and ports by number. Using this parameter causes it to use DNS and NIS services to convert these numbers into names.

+   - **command** This parameter is the command that’s to be followed. A summary of important commands follows this list, in the section “ipfw Commands.”

+   - **index** The *index* is a number from 0 to 65535 that indicates the rule’s place in the rule set. If you omit this parameter, the system automatically generates an *index* that’s 100 higher than the highest rule in the system, excluding the default policy rule (which has an *index* of 65535).

+   - **action** The *action* describes what to do with a packet. An *action* of **allow** indicates that the packet is to be accepted. Synonyms for **allow** are **accept** and **pass**. The **deny** and **reject** actions both block delivery of the packet, but in different ways. **deny** causes FreeBSD to ignore the packet, so to the sender, it appears that the packet was lost or the target computer is offline. **reject** causes