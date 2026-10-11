
## JUMPSTART: BUILDING A FIREWALL USING system-config-firewall

![](img/f28adb66a7398a382f0505e0ba74a872_864_0.png)

Figure 25-3 Firewall Configuration window

To run this utility, enter `system-config-firewall` (*FEDORA*) or `system-config-securitylevel` (*RHEL*) on a command line or select **System > Administration > Firewall** (*FEDORA*) or **System > Administration > Security Level and Firewall** (*RHEL*). The `system-config-firewall` and `system-config-securitylevel` utilities build an extremely simple firewall but struggle with complex setups. The `system-config-securitylevel` utility displays a simpler window that contains a subset of the features of `system-config-firewall`. This section describes the `system-config-firewall` utility, which displays the Firewall Configuration window (Figure 25-3).

To enable the firewall, click **Enable** on the toolbar. The firewall automatically allows packets that originate locally through to the outside (generally the Internet) and allows responses to those packets back in.

Click the check boxes next to the services that the local system provides. These boxes set up a firewall that allows the local system to function as one or more types of servers, including FTP, Mail (SMTP), Samba, Secure WWW (HTTPS), SSH, and WWW (HTTP).

### Opening Trusted services

Opening Other ports: Enter other ports you want to open by clicking **Other ports** on the left side of the window and then clicking **Add** to open the Port and Protocol window. This window allows you to select from a list or, if you put a check mark in the box labeled **User Defined**, specify a port to open and the protocol that that port uses (TCP or UDP). Click **Apply** and **Yes**, and `system-config-firewall` sets up the firewall. Click **Enable** if necessary. For more information refer to “system-config-firewall: Generates a Set of Rules” on page 833.

## ANATOMY OF AN iptables COMMAND

Command line: This section lists the components of an iptables command line that follow the name of the utility, `iptables`. Except as noted, the `iptables` utility is not sensitive to the position of arguments on the command line. The examples in this chapter reflect a generally accepted syntax that allows commands to be easily read, understood, and maintained. Not all commands have all components.

Many tokens on an iptables command line have two forms: a short form, consisting of a single letter preceded by a single hyphen, and a long form, consisting of a word preceded by two hyphens. Most scripts use the short forms for brevity; lines using the long forms can get unwieldy. The following iptables command lines are equivalent and are used as examples in this section:

```bash
# iptables --append FORWARD --in-interface eth1 --out-interface eth0 --jump ACCEPT
# iptables -A FORWARD -i eth1 -o eth0 -j ACCEPT
```

Table: Specifies the name of the table the command operates on: Filter, NAT, or Mangle. You can specify a table name in any iptables command. When you do not specify a table name, the command operates on the Filter table. Most of the examples in this chapter do not specify table names and, therefore, work on the Filter table. Specify a table as `-t tablename` or `--table tablename`.

Command: Tells iptables what to do with the rest of the command line—for example, add or delete a rule, display rules, or add a chain. The example commands, `-A` and `--append`, append the rule specified by the command line to the specified table and chain. See page 827 for a list of commands.

Chain: Specifies the name of the chain that this rule belongs to or that this command works on. The chain is INPUT, OUTPUT, FORWARD, PREROUTING, POSTROUTING, or the name of a user-defined chain. Specify a chain by putting the name of the chain on the command line without any preceding hyphens. The examples at the beginning of this section work with the FORWARD chain.

There are two kinds of match criteria: *packet match* criteria, which match a network packet, and *rule match* criteria, which match an existing rule.

Packet match criteria identify network packets and implement rules that take action on packets that match the criteria. The combination of packet match criteria and an action is called a **rule specification**. Rule specifications form the basis for packet filtering. The first example at the beginning of this section uses the `--in-interface eth1 --out-interface eth0` rule match criteria. The second example uses the short form of the same criteria: `-i eth1 -o eth0`. Both of these rules forward packets that come in on device `eth1` and go out on device `eth0`.

Rule match criteria identify existing rules. An `iptables` command can modify, remove, or position a new rule adjacent to a rule specified by a rule match criterion. There are two ways to identify an existing rule: You can use the same rule specification that was used to create the rule or you can use the rule's ordinal number, called a **rule number**. Rule numbers begin with 1, signifying the first rule in a chain, and can be displayed with `iptables -L` (or `--line-numbers`). The first command below deletes the rule listed at the beginning of this section; the second replaces rule number 3 in the INPUT chain with a rule that rejects all packets from IP address 192.168.0.10:

```bash
# iptables --delete FORWARD -i eth1 -o eth0 -j ACCEPT
# iptables -R INPUT 3 --source 192.168.0.10 -j REJECT
```

A **jump or target** specifies what action the kernel takes on packets that match all match criteria for a rule. Specify a jump or target as `-j target` or `--jump target`. The examples at the beginning of this section specify the ACCEPT target using the following commands: `--jump ACCEPT` and `-j ACCEPT`.

A jump transfers control to a different chain within the same table. The following command adds (`--append`) a rule to the INPUT chain that transfers packets that use the TCP protocol (`--protocol tcp`) to a user-defined chain named `tcp_rules` (`--jump tcp_rules`):

```bash
# iptables --append INPUT --protocol tcp --jump tcp_rules
```

When the packet finishes traversing the `tcp_rules` chain, assuming it has not been dropped or rejected, it continues traversing the INPUT chain from the rule following the one it jumped from.

A target specifies an action the kernel takes on the packet; the simplest actions are ACCEPT, DROP, and REJECT. The following command adds a rule to the FORWARD chain that rejects packets coming from the FTP port (1) (/etc/services, the file iptables consults to determine which port to use, shows that FTP uses port 21):

```bash
# iptables --append FORWARD --sport ftp --jump REJECT
```

Some targets, such as LOG, are **nontargeting:** Control passes to the next rule after the target is executed. See page 831 for information on how to use targets.

## BUILDING A SET OF RULES

To specify a table, it is common practice to put the table declaration on the command line immediately following `iptables`. For example, the following command flushes (deletes all the rules from) the NAT table:

```bash
# iptables -t NAT -F
```

## COMMANDS

Following is a list of iptables commands:

- `--append -A` Adds rule(s) specified by rule-specifications to the end of chain. When a packet matches one of the rule-specifications, target processes it.

```bash
iptables -A chain rule-specifications --jump target
```

- `--delete -D` Removes one or more rules from chain, as specified by the rule-numbers or rule-specifications.

```bash
iptables -D chain rule-numbers | rule-specifications
```

- `--insert -I` Adds rule(s) specified by rule-specifications and target to the location in chain specified by rule-number. If you do not specify rule-number, it defaults to 1, the head of the chain.

```bash
iptables -I chain rule-number rule-specifications --jump target
```

- `--replace -R` Replaces rule number rule-number in chain with rule-specification and target. The command fails if rule-number or rule-specification resolves to more than one address.

```bash
iptables -R chain rule-number rule-specification --jump target
```

- `--list -L` Displays the rules in chain. Omit chain to display rules for all chains. Use `--line-numbers` to display rule numbers or select other display criteria from the list on page 828.

```bash
iptables -L [chain] display-criteria
```

- `--flush -F` Deletes all rules from chain. Omit chain to delete all rules from all chains.

```bash
iptables -F [chain]
```

- `--zero -Z` Change to zero the value of all packet and byte counters in chain or in all chains when you do not specify chain. Use with `-L` to display the counters before clearing them.

```bash
iptables -Z [-L] [chain]
```

- `--delete-chain -X` Removes the user-defined chain named chain. If you do not specify chain, removes all user-defined chains. You cannot delete a chain that a target points to.

```bash
iptables -X chain
```

- `--policy -P` Sets the default target or policy builtin-target for the builtin chain builtin-chain. This policy is applied to packets that do not match any rule in the chain. If a chain does not have a policy, unmatched packets are ACCEPTed.

```bash
iptables -P builtin-chain builtin-target
```

- `--rename-chain -E` Changes the name of the chain old to new.

```bash
iptables -E old new
```
