The policy gives the action to be taken if no rules in the chain were matched. A policy can only be specified for built-in chains and can only be one of the first four special targets: ACCEPT, REJECT, DENY, or MASQ.

For example, if you only want to allow a few certain types of packets to be forwarded through the firewall, it would probably be easiest to make the default policy be DENY or REJECT and then to specify rules for the packets to forward. You would set the policy using the following command:

```
# ipchains forward DENY

or

# ipchains forward REJECT
```

# Working on Individual Rules

Now that you know how to work with entire chains of rules, we can talk about actually working with the rules that make the chains useful. There are five basic actions that can be taken on rules. You can append a rule to the end of a chain, insert a rule at a given position within a chain, replace a given rule, delete a rule at a given position within a chain, and delete the first rule that matches a given specification.

# Note

The next four sections only describe the command used to perform the specific action. For the most part, they don’t give enough information to actually use the command until you learn how to specify a rule. This will be discussed in the section entitled “Specifying a Rule.”

# Appending a Rule to the End of a Chain

The easiest way to add a rule to a chain is simply to append it to the end. You do this using the -A option:

```
ipchains -A chain rule-specification [options]
```

Recall, however, that the order of the rules is important. Appending a rule to the end of a chain will make it the last rule examined. If you want to place a rule at a different point in the chain, you must insert it using the insert command.