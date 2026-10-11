```
```
ipchains [-flags] {input|output|forward|custom_chain} [options] [action]
 ipchains -M [-L|-S] [options]
```
```

We will examine many of the ways in which this command can be used.

# ### Some Simple Examples

The first thing that we can do with `ipchains` is take a look at what rules are established by default. This can be accomplished with the `ipchains -L` as shown in Example 16-1. The output of this command shows us that there are three chains (the permanent ones)\input, forward, and output. Each of these chains has the same policy, or default action, which is `ACCEPT`. Thus, at this point, no packets will be rejected by the kernel.

```
**Example 16-1 Listing the Default Rules**
```
# /sbin/ipchains -L
Chain input (policy ACCEPT):
Chain forward (policy ACCEPT):
Chain output (policy ACCEPT):
#
```
```

In following sections, we’ll take a look at adding and removing rules from the permanent chains.

**Adding a Rule** Let’s suppose that we want to completely disable FTP traffic to the host `topcat`. We could accomplish this by commenting out or removing the `ftp` entry in `/etc/inetd.conf` (or `/etc/xinetd.conf, if we’re using xinetd—see Replacing inetd with xinetd on page 226 for a discussion of xinetd). We could also accomplish this using `ipchains`, as in

```
```
topcat# ipchains -I input 1 -p tcp --dport ftp -j REJECT
```
```

This command specifies that rule number 1 is inserted (-i) in the input chain. That rule applies to the protocol (-p) TCP and all packets with the destination port (--dport) of ftp. Any packet matching this rule will be rejected. Now we have a rule that prohibits inbound ftp connection requests. To see that this rule has been added, let’s look at a listing in Example 16-2. Notice that, even though we added the rule as rule number 1, there is no rule number associated with the rule. This becomes tedious as your rule sets get large. If you get `ipchains` Version 1.3.9 or later, you may use the command

```
```
# ipchains -L --line-numbers
```
```

to view rule numbers, but the rule numbers will not appear as you add rules. You could also have added this rule with the command

```
```
# ipchains -A input -p tcp --dport ftp -j REJECT
```
```

Here we are using append (-a), which means add the rule to the end of the chain, but before the policy (which represents the last rule). In this case, the