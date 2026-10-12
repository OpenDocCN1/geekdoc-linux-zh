
### 5.12.2. Configuring a Custom Service for an IP Set

You can add the IP set as a source to a zone to control all traffic coming in from any of the addresses listed in the IP set with a zone. For example, to add the `test` IP set as a source to the `drop` zone to drop all packets coming from all entries listed in the `test` IP set, use the following command as `root`:

```bash
[~]# firewall-cmd --permanent --zone=drop --add-source=ipset:test
success
```

The `ipset:` prefix in the source shows `firewalld` that the source is an IP set and not an IP address or an address range.

Only the creation and removal of IP sets is limited to the permanent environment, all other IP set options can be used also in the runtime environment without the `--permanent` option.

To configure a custom service to create and load the IP set structure before `firewalld` starts:

1. Using an editor running as `root`, create a file as follows:

```bash
[~]# vi /etc/systemd/system/ipset_name.service
[Unit]
Description=ipset_name
Before=firewalld.service

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/local/bin/ipset_name.sh start
ExecStop=/usr/local/bin/ipset_name.sh stop

[Install]
WantedBy=basic.target
```

2. Use the IP set permanently in `firewalld`:

```bash
[~]# vi /etc/firewalld/direct.xml
<?xml version="1.0" encoding="utf-8"?>
<direct>
  <rule ipv="ipv4" table="filter" chain="INPUT" priority="0">-m set \
-match-set ipset_name src -j DROP</rule>
</direct>
```

3. A `firewalld` reload is required to activate the changes:

```bash
[~]# firewall-cmd --reload
```

This reloads the firewall without losing state information (TCP sessions will not be terminated), but service disruption is possible during the reload.

> **WARNING**
> Red Hat does not recommend using IP sets that are not managed through firewalld. To use such IP sets, a permanent direct rule is required to reference the set, and a custom service must be added to create these IP sets. This service needs to be started before firewalld starts, otherwise firewalld is not able to add the direct rules using these sets. You can add permanent direct rules with the `/etc/firewalld/direct.xml` file.

## 5.13. SETTING AND CONTROLLING IP SETS USING IPTABLES

The essential differences between firewalld and the iptables (and ip6tables) services are:

- The iptables service stores configuration in `/etc/sysconfig/iptables` and `/etc/sysconfig/ip6tables`, while firewalld stores it in various XML files in `/usr/lib/firewalld/` and `/etc/firewalld/`. Note that the `/etc/sysconfig/iptables` file does not exist as firewalld is installed by default on Red Hat Enterprise Linux.
- With the iptables service, every single change means flushing all the old rules and reading all the new rules from `/etc/sysconfig/iptables`, while with firewalld there is no recreating of all the rules. Only the differences are applied. Consequently, firewalld can change the settings during runtime without existing connections being lost.

Both use the iptables tool to talk to the kernel packet filter.

To use the iptables and ip6tables services instead of firewalld, first disable firewalld by running the following command as root:

```bash
~]# systemctl disable firewalld
~]# systemctl stop firewalld
```

Then install the iptables-services package by entering the following command as root:

```bash
~]# yum install iptables-services
```

The iptables-services package contains the iptables service and the ip6tables service.

Then, to start the iptables and ip6tables services, enter the following commands as root:

```bash
~]# systemctl start iptables
~]# systemctl start ip6tables
```

To enable the services to start on every system start, enter the following commands:

```bash
~]# systemctl enable iptables
~]# systemctl enable ip6tables
```

The ipset utility is used to administer IP sets in the Linux kernel. An IP set is a framework for storing IP addresses, port numbers, IP and MAC address pairs, or IP address and port number pairs. The sets are indexed in such a way that very fast matching can be made against a set even when the sets are very large. IP sets enable simpler and more manageable configurations as well as providing performance advantages when using iptables. The iptables matches and targets referring to sets create references which protect the given sets in the kernel. A set cannot be destroyed while there is a single reference pointing to it.

The use of **ipset** enables **iptables** commands, such as those below, to be replaced by a set:

```bash
~]# iptables -A INPUT -s 10.0.0.0/8 -j DROP
~]# iptables -A INPUT -s 172.16.0.0/12 -j DROP
~]# iptables -A INPUT -s 192.168.0.0/16 -j DROP
```

The set is created as follows:

```bash
~]# ipset create my-block-set hash:net
~]# ipset add my-block-set 10.0.0.0/8
~]# ipset add my-block-set 172.16.0.0/12
~]# ipset add my-block-set 192.168.0.0/16
```

The set is then referenced in an **iptables** command as follows:

```bash
~]# iptables -A INPUT -m set --match-set my-block-set src -j DROP
```

If the set is used more than once a saving in configuration time is made. If the set contains many entries a saving in processing time is made.

## 5.14. USING THE DIRECT INTERFACE

It is possible to add and remove chains during runtime by using the `--direct` option with the `firewall-cmd` tool. A few examples are presented here. See the `firewall-cmd(1)` man page for more information.

It is dangerous to use the direct interface if you are not very familiar with **iptables** as you could inadvertently cause a breach in the firewall.

The direct interface mode is intended for services or applications to add specific firewall rules during runtime. The rules can be made permanent by adding the `--permanent` option using the `firewall-cmd --permanent --direct` command or by modifying `/etc/firewalld/direct.xml`. See man `firewalld.direct(5)` for information on the `/etc/firewalld/direct.xml` file.

### 5.14.1. Adding a Rule using the Direct Interface

To add a rule to the “IN_public_allow” chain, enter the following command as **root**:

```bash
~]# firewall-cmd --direct --add-rule ipv4 filter IN_public_allow \
     0 -m tcp -p tcp --dport 666 -j ACCEPT
```

Add the `--permanent` option to make the setting persistent.

### 5.14.2. Removing a Rule using the Direct Interface

To remove a rule from the “IN_public_allow” chain, enter the following command as **root**:

```bash
~]# firewall-cmd --direct --remove-rule ipv4 filter IN_public_allow \
    0 -m tcp -p tcp --dport 666 -j ACCEPT
```

Add the `--permanent` option to make the setting persistent.

### 5.14.3. Listing Rules using the Direct Interface

To list the rules in the “IN_public_allow” chain, enter the following command as **root**:

```bash
~]# firewall-cmd --direct --get-rules ipv4 filter IN_public_allow
```

Note that this command (the `--get-rules` option) only lists rules previously added using the `--add-rule` option. It does not list existing `iptables` rules added by other means.

## 5.15. CONFIGURING COMPLEX FIREWALL RULES WITH THE "RICH LANGUAGE" SYNTAX

With the “rich language” syntax, complex firewall rules can be created in a way that is easier to understand than the direct-interface method. In addition, the settings can be made permanent. The language uses keywords with values and is an abstract representation of `iptables` rules. Zones can be configured using this language; the current configuration method will still be supported.

### 5.15.1. Formatting of the Rich Language Commands

All the commands in this section need to be run as **root**. The format of the command to add a rule is as follows:

```bash
firewall-cmd [--zone=zone] --add-rich-rule='rule' [--timeout=timeval]
```

This will add a rich language rule *rule* for zone *zone*. This option can be specified multiple times. If the zone is omitted, the default zone is used. If a timeout is supplied, the rule or rules only stay active for the amount of time specified and will be removed automatically afterwards. The time value can be followed by s (seconds), m (minutes), or h (hours) to specify the unit of time. The default is seconds.

To remove a rule:

```bash
firewall-cmd [--zone=zone] --remove-rich-rule='rule'
```

This will remove a rich language rule *rule* for zone *zone*. This option can be specified multiple times. If the zone is omitted, the default zone is used.

To check if a rule is present:

```bash
firewall-cmd [--zone=zone] --query-rich-rule='rule'
```

This will return whether a rich language rule *rule* has been added for the zone *zone*. The command prints **yes** with exit status **0** if enabled. It prints **no** with exit status **1** otherwise. If the zone is omitted, the default zone is used.

For information about the rich language representation used in the zone configuration files, see the `firewalld.zone(5)` man page.
