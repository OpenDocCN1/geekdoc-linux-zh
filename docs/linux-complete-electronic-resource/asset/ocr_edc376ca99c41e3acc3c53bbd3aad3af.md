# **CATEGORIES** The following flags are used to select the category of rules to which the given command applies:

+   - `-A [direction]` IP accounting rules. Optionally, a *direction* can be specified (*in*, *out*, or *both*), indicating whether only incoming or outgoing packets should be counted. The default direction is *both*.

+   - `-I` IP input firewall rules.

+   - `-O` IP output firewall rules.

+   - `-F` IP forwarding firewall rules.

+   - `-M` IP masquarading administration. This category can only be used in combination with the `-l` (list) or `-s` (set timeout values) command.

Exactly one of these options has to be specified.

# **COMMANDS** The next options specify the specific action to perform. Only one of them can be specified on the command line, unless something else is listed in the description.

+   - `-a [policy]` Append one or more rules to the end of the selected list. For the accounting chain, no policy should be specified. For firewall chains, it is required to specify one of the following policies: *accept*, *deny*, or *reject*. When the source and/or destination names resolve to more than one address, a rule will be added for each possible address combination.

+   - `-i [policy]` Insert one or more rules at the beginning of the selected list. See the description of the `-a` command for more details.

+   - `-d [policy]` Delete one or more entries from the selected list of rules. The semantics are equal to those of the append/insert commands. The specified parameters should exactly match the parameters given with an append or insert command, otherwise no match will be found and the rule will not be removed from the list. Only the first matching rule in the list will be deleted.