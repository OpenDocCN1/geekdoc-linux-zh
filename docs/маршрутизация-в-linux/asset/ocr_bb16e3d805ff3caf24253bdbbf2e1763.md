# Table 5.9 Continued

| Option | Purpose | Format | Value(s) |
|--------|---------|--------|----------|
| no broadcast | Sets gated not to broadcast RIP packets even if there are multiple active interfaces in this machine. | N/A | N/A |
| nocheckzero | Sets gated not to reject RIP-1 packets who have nonempty reserved fields. | N/A | N/A |
| preference | Sets the preference level for a route that gated learned through RIP (as compared to other routes). The preference level goes in place of value. The default is 100. In the case of gated, the lower the preference, the more likely this route will be used. | preference value; | 100 |
| query authentication | Sets whether gated should be fussy or not about RIP-2 queries that come from nonrouters. The value for this option is one of the following: none (default), simple, or md5 (which is at best not much better than just using a password). If you choose either of the last two, you also must include a password at the end before the semi-colon. | authentication value; | none, simple, or md5 |
| Sourcegateways | Sets which routers gated should send unicast data to instead of broadcasting. The machines value consists of one or more space-separated IP addresses. | sourcegateways machines; |  |
| Traceoptions | Sets what gated tracing logs. The settings value can consist of general protocol gated tracing options and RIP-specific gated tracing options. These two option sets are covered in Tables 5.11 and 5.12. | traceoptions settings; |  |