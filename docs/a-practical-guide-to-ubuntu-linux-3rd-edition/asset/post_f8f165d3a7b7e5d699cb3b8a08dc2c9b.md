
## IMPLICIT MATCH EXTENSIONS

Implicit extensions are loaded (somewhat) automatically when you use a `-protocol` command (described below). Each protocol has its own extensions. Follow the protocol with `-h` to display extensions you can use with that protocol. For example, the following command displays TCP extensions at the end of the Help output:

```
$ iptables -p tcp -h
... 
tcp match options:
  --tcp-flags [!] mask comp        match when TCP flags & mask == comp
                                   (Flags: SYN ACK FIN RST URG PSH ALL NONE)
  [!] --syn                         match when only SYN flag set
                                   (equivalent to --tcp-flags SYN,RST,ACK SYN)
  --source-port [!] port[:port]
  --sport ...
                                   match source port(s)
  --destination-port [!] port[:port]
  --dport ...
                                   match destination port(s)
  --tcp-option [!] number          match if TCP option set
```

This section does not describe all extensions. Use `-h`, as in the preceding example, to display a complete list.

`-P` Loads the proto module and matches if the packet uses the proto protocol. The proto can be a name or number from `/etc/protocols`, including `tcp`, `udp`, and `icmp` (page 1153). Specifying `all` or `0` (zero) matches all protocols and is the same as not including this match in a rule.

The following criteria load the TCP module and match TCP protocol packets coming from port 22 (ssh packets):

```
--protocol tcp --source-port 22
```

The following command expands the preceding match to cause the kernel to drop all incoming ssh packets. This command uses `ssh`, which iptables looks up in `/etc/services`, in place of 22:

```
$ sudo iptables --protocol tcp --source-port ssh --jump DROP
```

The extensions in this section are loaded when you specify `--protocol tcp`.

`-dport` Matches a destination port number or service name (see `/etc/services`). You can also specify a range of port numbers. Specifically, `:port` specifies ports 0 through `port`, and `port:` specifies ports `port` through 65535.

`--source-port [!] port[:port]` Matches a source port number or service name (see `/etc/services`). You can also specify a range of port numbers. Specifically, `:port` specifies ports 0 through `port`, and `port:` specifies ports `port` through 65535.

`[!] --syn` Matches packets with the SYN bit set and the ACK and FIN bits cleared. This match extension is shorthand for `--tcp-flags SYN,RST,ACK SYN`.

`--tcp-flags [!] mask comp` Defines which TCP flag settings constitute a match. Valid flags are SYN, ACK, FIN, RST, URG, PSH, ALL, and NONE. The `mask` is a comma-separated list of flags to be examined; `comp` is a comma-separated subset of `mask` that specifies the flags that must be set for a match to occur. Flags not specified in `mask` must be unset.

`--tcp-option [!] n` Matches a TCP option with a decimal value of `n`.

### UDP

When you specify `--protocol udp`, you can specify a source and/or destination port in the same manner as described under “TCP” on the preceding page.

### ICMP

The extension in this section is loaded when you specify `--protocol icmp`. ICMP (page 1153) packets carry messages only.

`--icmp-type [!] name` Matches when the packet is an ICMP packet of type `name`. The `name` can be a numeric ICMP type or one of the names returned by

```
$ iptables -p icmp -h
```

## EXPLICIT MATCH EXTENSIONS

Explicit match extensions differ from implicit match extensions in that you must use a `-m` or `--match` option to specify a module before you can use the extension. Many explicit match extension modules are available; this section covers `state`, one of the most important.

### STATE

The `state` extension matches criteria based on the state of the connection the packet is part of (page 882).

`--state state` Matches a packet whose state is defined by `state`, a comma-separated list of states from the following list:

- ESTABLISHED — Any packet, within a specific connection, following the exchange of packets in both directions for that connection.
- INVALID — A stateless or unidentifiable packet.
- NEW — The first packet within a specific connection, typically a SYN packet.
- RELATED — Any packets exchanged in a connection spawned from an ESTABLISHED connection. For example, an FTP data connection might be related to the FTP control connection. (You need the `ip_conntrack_ftp` module for FTP connection tracking.)

The following command loads the state extension and establishes a rule that matches and drops both invalid packets and packets from new connections:

```shell
$ sudo iptables --match state --state INVALID,NEW --jump DROP
```

## TARGETS

All targets are built in; there are no user-defined targets. This section lists some of the targets available with iptables. Applicable target options are listed following each target.

- **ACCEPT**
  Continues processing the packet.

- **DNAT**
  Destination Network Address Translation
  Rewrites the destination address of the packet (page 881).
  - `--to-destination ip[:ip] [:port:port]`
    Same as SNAT with `to-source`, except that it changes the destination addresses of packets to the specified addresses and ports and is valid only in the PREROUTING or OUTPUT chains of the NAT table and any user-defined chains called from those chains. The following command adds to the PREROUTING chain of the NAT table a rule that changes the destination in the headers of TCP packets with a destination of 66.187.232.50 to 192.168.0.10:
    ```shell
    $ sudo iptables -t NAT -A PREROUTING -p tcp -d 66.187.232.50 -j DNAT --to-destination 192.168.0.10
    ```

- **DROP**
  Ends the packet’s life without notice.

- **LOG**
  Turns on logging for the packet being processed. The kernel uses syslogd (page 625) to process output generated by this target. LOG is a nonterminating target, so processing continues with the next rule. Use two rules to LOG packets that you REJECT or DROP, one each with the targets LOG and REJECT or DROP, with the same matching criteria.
  - `--log-level n`
    Specifies logging level `n` as per `syslog.conf` (page 626).
  - `--log-prefix string`
    Prefixes log entries with `string`, which can be a maximum of 14 characters long.
  - `--log-tcp-options`
    Logs options from the TCP packet header.
  - `--log-ip-options`
    Logs options from the IP packet header.

- **MASQUERADE**
  Similar to SNAT with `to-source`, except that it grabs the IP information from the interface on the specified port. For use on systems with dynamically assigned IP addresses, such as those using DHCP, including most dial-up lines. Valid only in rules in the POSTROUTING chain of the NAT table.
  - `--to-ports port[-port]`
    Specifies the port for the interface you want to masquerade. Forgets connections when the interface goes down, as is appropriate for dial-up lines. You must specify the TCP or UDP protocol (`--protocol tcp` or `udp`) with this target.

- **REJECT**
  Similar to DROP, except that it notifies the sending system that the packet was blocked.
  - `--reject-with type`
    Returns the error `type` to the originating system. The `type` can be any of the following, all of which return the appropriate ICMP (page 1153) error: `icmp-net-unreachable`, `icmp-host-unreachable`, `icmp-port-unreachable`, `icmp-proto-unreachable`, `icmp-net-prohibited`, or `icmp-host-prohibited`. You can specify `type` as `echo-reply` from rules that require an ICMP ping (page 393) packet to return a ping reply. You can specify `tcp-reset` from rules in or called from the INPUT chain to return a TCP RST packet. This parameter is valid in the INPUT, FORWARD, and OUTPUT chains and user-defined chains called from these chains.

- **RETURN**
  Stops traversing this chain and returns the packet to the calling chain.

- **SNAT**
  Source Network Address Translation
  Rewrites the source address of the packet. Appropriate for hosts on a LAN that share an Internet connection.
  - `--to-source ip[-ip][[:port[-port]]]`
    Alters the source IP address of an outbound packet, and the source IP addresses of all future packets in this connection, to `ip`. Skips additional rules, if any exist. Returning packets are automatically de-SNATed so they return to the originating host. Valid only in the POSTROUTING chain of the NAT table.

When you specify a range of IP addresses (`ip-ip`) or use multiple `to-source` targets, iptables assigns the addresses in a round-robin fashion, cycling through the addresses, one for each new connection.

When the rule specifies the TCP or UDP protocol (`-p tcp` or `-p udp`), you can specify a range of ports. When you do not specify a range of ports, the rule matches all ports. Every connection on a NATed subnet must have a unique IP address and port combination. If two systems on a NATed subnet try to use the same port, the kernel maps one of the ports to another (unused) port. Ports less than 512 are mapped to other ports less than 512, ports from 512 to 1024 are mapped to other ports from 512 to 1024, and ports above 1024 are mapped to other ports above 1024.

## COPYING RULES TO AND FROM THE KERNEL

The `iptables-save` utility copies packet filtering rules from the kernel to standard output so you can save them in a file. The `iptables-restore` utility copies rules from standard input, as written by `iptables-save`, to the kernel. Sample output from `iptables-save` appears on the next page.
