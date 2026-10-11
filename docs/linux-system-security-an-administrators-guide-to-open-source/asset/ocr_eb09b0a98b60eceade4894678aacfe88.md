Internet due to our default REJECT rules. If a system on the Internet attempted to ping topcat, it would get no response for the same reason. This latter behavior satisfies the first part of item 2 above. So we need to address item 1 and the logging part of item 2. Let's do it.

# Example 16-8 Failed ping Attempt Due to Default REJECT Rules

```
[root@topcat]# ping podunk.edu
PING podunk.edu (1.1.1.1): 56 data bytes
ping: sendto: Operation not permitted
ping: wrote podunk.edu 64 chars, ret=-1
^C
[root@topcat]#
```

# Table 16.8 ICMP Codes Supported by ipchains

| ICMP Code Number | ICMP Code Name | Associated ICMP Type Name |
|:---:|:---|:---|
| 0 | network-unreachable | destination-unreachable |
| 1 | host-unreachable | destination-unreachable |
| 2 | protocol-unreachable | destination-unreachable |
| 3 | port-unreachable | destination-unreachable |
| 4 | fragmentation-needed | destination-unreachable |
| 5 | source-route-failed | destination-unreachable |
| 6 | network-unknown | destination-unreachable |
| 7 | host-unknown | destination-unreachable |
| 9 | network-prohibited | destination-unreachable |
| 10 | host-prohibited | destination-unreachable |
| 11 | TOS-network-unreachable | destination-unreachable |
| 12 | TOS-host-unreachable | destination-unreachable |
| 13 | communication-prohibited | destination-unreachable |
| 14 | host-precedence-violation | destination-unreachable |
| 15 | precedence-cutoff | destination-unreachable |
| 0 | network-redirect | redirect |
| 1 | host-redirect | redirect |
| 2 | TOS-network-redirect | redirect |
| 3 | TOS-host-redirect | redirect |
| 0 | ttl-zero-during-transit | time-exceeded (ttl-exceeded) |
| 1 | ttl-zero-during-reassembly | time-exceeded (ttl-exceeded) |
| 0 | ip-header-bad | parameter-problem |
| 1 | required-option-missing | parameter-problem |