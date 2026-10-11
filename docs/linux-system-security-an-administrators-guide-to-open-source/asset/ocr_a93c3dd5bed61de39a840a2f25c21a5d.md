and some simple examples. We'll move from there to examine some of the more complex features such as custom chains and IP masquerading. In *Building Your Firewall* on page 469, we'll look at some real-world examples.

# The iptchains Command

There's really no way to simplify the introduction of the flags, options, and actions associated with *iptables*. So, Table 16.1 lists the flags or commands, Table 16.2 describes the options or parameters, and Table 16.3 notes the actions. We will use examples throughout the remainder of this chapter to clarify the use of many of them.

Each of the flags in Table 16.1 can utilize one or more options, described in Table 16.2. These options are the parameters that comprise a rule.

**Table 16.1** Flags of iptchains

| Flag | Description |
| :--- | :--- |
| -A or<br>--append | Appends one or more rules to the specified chain. |
| -C or<br>--check | Checks a given packet against the selected chain. The -s, -d, -p, and -i flags are required (see Table 16.2 on page 442). |
| -D or<br>--delete | Deletes one or more rules from the specified chain. |
| -F, or<br>--flush | Flushes all the rules in the specified chain. |
| -I or<br>--insert | Inserts one or more rules in the specified chain at the specified rule number. |
| -L or<br>--list | Lists all the rules in the selected chain. If no chain is specified, then all rules in all chains are listed. |
| -M or<br>--masquerading | If used with -L, this flag will display all masquerading rules. If used with -N, this flag will set one or more masquerading parameters. Masquerading rules are discussed in *IP Masquerading* on page 458. |
| -N or<br>--new-chain | Creates a new custom chain. The name of the new chain cannot exceed 8 characters. Custom chains are defined in *Custom Chains* on page 440. |
| -P or<br>--policy | Specifies the policy, or default rule, for a permanent chain. Policies cannot be specified for custom chains. This is the last rule in the chain, even though it appears first when listed with -L. |
| -R or<br>--replace | Replaces a rule in the specified chain. |