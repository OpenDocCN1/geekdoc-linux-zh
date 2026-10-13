> **Note**  
> You even need to declare the table to use when you create or delete a user-defined chain. Only the built-in chains OUTPUT and PREROUTING can belong to more than one table.

# IPTABLES COMMANDS

Six variations are possible on the iptables command line shown earlier, and they are covered in the following command descriptions.

These commands are as follows (all commands are preceded by a hyphen):

+   - **-A (append)**—This takes a chain name and a rule specification as mandatory arguments.
+   - **-D (delete)**—This takes a chain name and a rule specification or rule number as mandatory arguments.
+   - **-C (test/check)**—-s, -d, -p, and -i are required. This takes a chain name and a rule specification as mandatory arguments. As of this writing, this command had not been implemented, but is on the author’s ToDo list.
+   - **-I (insert)**—An extension of append, but the rule specification is placed ahead of the rule number that is referenced. This command takes a chain name, rule number for insertion ahead of, and a rule specification as mandatory arguments.
+   - **-R (replace)**—An Insert and Delete. This takes as mandatory arguments a chain name, a rule number, and a rule specification. The rule specification will replace the rule number in the specified chain.
+   - **-F (flush)**—Delete all rules in a chain, or all rules in all chains if no chain name is specified.
+   - **-L (list)**—List all rules in a chain or all rules in all chains if no chain name is specified.
+   - **-Z (zero)**—Zero counters. Zeroes counters in specified chain or all chains if no chain name is provided.
+   - **-N (new)**—Create a user-defined chain. This requires only a chain name as a mandatory argument.
+   - **-X (delete a user-defined chain)**—This requires a chain name, and the chain must be empty (flushed). Default chains cannot be deleted.
+   - **-P (policy)**—This takes as mandatory arguments a chain name and a target.
+   - **-E (rename chain)**—This takes as mandatory arguments the old chain name and the new chain name.
+   - **-h (help)**—This special option takes no commands, only accepts one option (-h), and optionally accepts one argument.

# IPTABLES OPTIONS

A number of options are available for iptables. Where address masks are specified, the mask can be either of the following types: /N or /N.N.N.N. Addresses can also be hostnames. Ports can be either numbers or service names.