222

Chapter 16. iptables

When looking at the structure of an iptables command, it is important to remember that, unlike other commands, the length and complexity of a iptables command can change based on its purpose. A simple command to remove a rule can be very short, while a command designed to filter packets from a particular subset using a variety of specific parameters and options can be lengthy. When creating iptables commands it is helpful to recognize that some parameters and options may need the need for other parameters and options to further specify the previous option's request. In order to construct a valid rule, this must continue until every parameter and option that requires another set of options is satisfied.

Type iptables -h to see a comprehensive list of iptables command structures.

# 16.3.3. Commands

Commands iptables to perform a specific action. Only one command is allowed per iptables command string. With the exception of the help command, all commands are written in upper-case characters.

The iptables commands are as follows:

+   - -A Appends the iptables rule to the end of the specified chain. This is the command used to simply add a rule when order in the chain does not matter.
- -C Checks a particular rule before adding it to the user-specified chain. This command can help you verify complicated iptables by prompting you for additional parameters and options.
- -D Deletes a rule in a particular chain by number (such as 5 for the fifth rule in a chain). You can also delete the entire rule, and iptables will delete the chain that matches.
- -E Renames a user-defined chain. This does not affect the structure of the table.
- -F Flushes the specified chain, which effectively deletes every rule in the chain. If no chain is specified, this command flushes every rule from chain.
- -h Provides a list of command structures, as well as a quick summary of command parameters and options.
- -I Inserts a rule in a chain at a point specified by a user-defined integer value. If no number is specified, iptables will place the command at the top of the chain.

![](bbox=[0.095, 0.633, 0.135, 0.658])

# Caution

Be aware of which option (-A or -I) is used when adding a rule. The order of the rules within a chain are important for determining which rules apply to what packets.

+   - -L Lists all the rules in the chain specified after the command. To list all rules in all chains the default filter, do not specify a chain or table. Otherwise, the syntax should be used to list the rules in a specific chain in a particular:
iptables -L <chain-name> -t <table-name>
- -N Creates a new chain with a user-specified name.
- -P Sets the default policy for a particular chain, so that when packets traverse an entire chain without matching a rule, they will be sent to a particular target, such as ACCEPT or DROP.
- -R Replaces a rule in a particular chain. The rule's number must be specified after the chain's name. The first rule in a chain corresponds to rule number one.
- -X Deletes a user-specified chain. Deleting a built-in chain for any table is not allowed.

Powerful options for the -L command that provide rules and allow more verbose rule descriptions, others, are described in Section 16.3.7 Listing Options.