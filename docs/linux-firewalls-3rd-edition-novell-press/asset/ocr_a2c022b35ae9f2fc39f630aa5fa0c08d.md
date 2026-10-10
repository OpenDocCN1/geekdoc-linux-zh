# What Did Optimization Buy?

Note that some of the variations in the tables are artifacts of how the sample scripts in Chapter 4 and this chapter are organized, as well as some differences in the TCP state flag and source address checks between the two examples.

The optimized versions have more rules than their straight-through counterparts! Even more surprising, the connection-tracking versions have more rules than the classic, stateless versions! Didn't we already conclude that use of the state match module reduces the number of rules by eliminating individual **ACCEPT** rules for server responses to client requests? Yes and no... The absolute number of rules increases, because the static rules must remain present to account for any cases in which a state table entry has timed out or been replaced due to a resource shortage. The number of input rules *traversed* can drop dramatically.

Using user-defined chains results in a few more rules as well. The additional rules perform the intermediate packet selection and branching. There's a small amount of overhead? Yes and the top-level branching decisions. The overhead isn't significant and even the small amount of apparent overhead is deceiving. The number of rules traversed isn't as critical of a performance metric as the number of individual header field match tests performed.

Optimization with user-defined chains can significantly reduce the number of rules that a response packet must be tested against before reaching its final matching rule. What isn't obvious here is that the straight-through ruleset includes a set amount of overhead because of the antispoofing rules. Because the example firewalls were client-centered, the straight-through server traversal lengths are much longer than the client lengths as a result of the address checking done on the incoming packets.

Using the state module and thereby bypassing the firewall for established traffic dramatically reduces list traversal length for established connections. The increase in number of rules traversed for new connections is the result of the duplicate rules, the connection-tracking rules, and their static counterparts.

Even with the state module, the initial packet always takes the static path. So the gain that the classic optimized version shows over the straight-through version still applies to the first packet.

Finally, the benefits of both optimization and connection state tracking are obvious! The categorization being performed by the user-defined chains dramatically reduces the actual number of tests that a packet is tested against in a classic packet-filtering firewall. Use of the state modules reduces the number of tests even further by skipping the rules altogether. Furthermore, the data channel connection is matched immediately as a **RELATED** connection.

What is perhaps least obvious, unless you've read the kernel firewall code, is that the real performance issue isn't the number of rules traversed, per se, but the number of comparison tests performed. Each unmatched, traversed rule represents at least one comparison (for example,