
## Table 16.10 Simple Internal Network Example Server Addresses

| Hostname | IP Address | Purpose of Host |
| :--- | :--- | :--- |
| dnssvr1 | 202.7.1.225 | The primary DNS server. |
| dnssvr2 | 202.7.1.226 | The secondary DNS server. |
| mail | 202.7.1.227 | The POP3 server. POP3 for retrieving mail, SMTP for sending mail. |
| rtr-isp | 202.7.1.17 | The router to the ISP. Our default gateway. |

Let’s implement the rules to meet these requirements. We take the approach of manually executing each command for the purposes of clarifying the example. The steps are outlined beginning with *Initial Steps and the Default Policy* below, continuing through *Finally!* on page 480. Example 16-41 on page 481 captures the manual commands into a script.

### Initial Steps and the Default Policy

In accordance with our discussion in *Changing Rules* on page 467, we take down the interfaces and then flush the chains and start with a REJECT rule. We will remove the first REJECT rule when we are finished (see *Finally!* on page 480). We also set the default policy to REJECT. These steps are shown in Example 16-26. Note that we also added the two rules:

```
[root@topcat]# ipchains -A input -i lo -s 0 -d 0/0 -j ACCEPT
[root@topcat]# ipchains -A output -i lo -s 0 -d 0/0 -j ACCEPT
```

to allow all communications through the loopback interface.

#### Example 16-26 Initial REJECT Rules

```
[root@topcat]# ifconfig eth1 down
[root@topcat]# ifconfig eth0 down
[root@topcat]# ipchains -F
[root@topcat]# ipchains -I input 1 -j REJECT
[root@topcat]# ipchains -I input 1 -j REJECT
[root@topcat]# ipchains -I forward 1 -j REJECT
[root@topcat]# ipchains -A input -i lo -s 0 -d 0/0 -j ACCEPT
[root@topcat]# ipchains -A output -i lo -s 0 -d 0/0 -j ACCEPT
[root@topcat]# ipchains -P input REJECT
[root@topcat]# ipchains -P output REJECT
[root@topcat]# ipchains -P forward REJECT
[root@topcat]# ifconfig eth1 up
[root@topcat]# ifconfig eth0 up
```

Now let’s set up antispoofing (see *Antispoofing Rules* on page 463). We need to put a 1 in every rp_filter file, so we’ll just use a short script as shown in Example 16-27.

For those of you using kernel versions 2.0.x or earlier, be sure to add the last command shown in Example 16-27 to prevent loopback spoofing. This rule won’t hurt if you are using kernel version 2.1.x or 2.2.x.

#### Example 16-27 Antispoofing Script

```
[root@topcat]# for file in /proc/sys/net/ipv4/conf/*/rp_filter
> do
> echo "1" > $file
> done
[root@topcat]# ipchains -A input -i ! lo -s 127.0.0.0/8 -j REJECT
[root@topcat]#
```

We must next establish IP forwarding (to allow masquerading) and load the ftp masquerading module. Thus we execute the commands shown in Example 16-28. The first command, `/sbin/depmod -a`, performs a dependency check on all kernel modules.

#### Example 16-28 Initial Steps for Masquerading Support

```
[root@topcat]# depmod -a
[root@topcat]# modprobe ip_masq_ftp
[root@topcat]# echo "1" > /proc/sys/net/ipv4/ip_forward
```

### Setting IP Masquerading Time-Outs

By default, the kernel sets time-outs to 15 minutes for masqueraded sessions of all types. There are three time-out parameters that apply to masquerading: TCP time-outs, TCP FIN packet (TCP packets with the finish bit set) time-outs, and UDP time-outs (see Table 16.1 on page 441). TCP FIN time-outs should be short, so we'll use 10 seconds. UDP time-outs are related to the time between the arrival or dispatch of individual UDP packets that belong to the same communication. A good time-out range for this is somewhere between 40 and 60 seconds, so we will use 50 seconds. General TCP time-outs are based on inactivity of a session. So, if you have an established telnet connection, for example, and you don't use it for 15 minutes, by default, the connection will be broken. You may find it useful to increase this time-out period; we use 1 hour (3600 seconds). The command is provided in Example 16-29.

#### Example 16-29 Setting the Masquerading Time-Outs

```
[root@topcat]# ipchains -M -s 3600 10 50
```

### Generally Restricting Inbound Requests

We don't allow any inbound connections from the Internet, so we REJECT and log all requests to our internal network (10.0.0.0) and we REJECT all TCP SYN packets (described in *Rule Ordering Is Important!* on page 464) as our first two rules in the input chain as shown in Example 16-30.

#### Example 16-30 Reject All Inbound Attempts

```
[root@topcat]# ipchains -A input -i eth0 -p tcp -d 10.0.0.0/8 -j REJECT
[root@topcat]# ipchains -A input -i eth0 -y -p tcp +d topcat -j REJECT
```

### ICMP Rules

At this point, we can deal with our ICMP requirements. We need to allow outbound ping and disallow incoming ping. We already established these rules in *Sample ICMP Rules* on page 454. But we’ll be a little more careful, in accordance with *Rule Writing and Logging Tips* on page 466.

We need four rules to allow `ping` to go from our internal network to the Internet. Here’s why: A user on a client in the 10.0.0.0 network executes a `ping` to a system in the Internet. The `ping` generates an ICMP echo-request, which goes to `totcat-in` (`eth1`) and is initially processed by the input chain. So we need a rule for that. The ICMP echo-request is then passed on to the forward chain for routing. We’ll use the masquerading rule for that. Next the packet is passed on to the output chain to head off to the Internet via `eth0`. We’ll need another rule there.

Then the packet leaves `totcat` and reaches the server. The server responds with an ICMP echo-reply, which arrives at `totcat` (`eth0`) to be processed by the input chain. We’ll put a rule in there. Because the address is masqueraded, it skips the forward chain and goes straight to the output chain for processing before it heads out `eth1` and back to the internal client.

We also do not want to respond to `ping` requests from the Internet, so we’ll add a rule for that—Example 16-31 provides the rules. (The numbering to the left is for illustrative purposes and will not actually appear.)

#### Example 16-31 Rules to Manage ping

```
[root@topcat]# ipchains -A input -p icmp --icmp-type echo-request -i eth0 -s 0/0 -d totcat -j REJECT
[root@topcat]# ipchains -A input -p icmp --icmp-type echo-request -i eth1 -s 10.0.0.0/8 -d 0/0 -j ACCEPT
[root@topcat]# ipchains -A forward -i eth0 -s 10.0.0.0/8 -d 0/0 -j MASQ
[root@topcat]# ipchains -A output -p icmp --icmp-type echo-request -i eth0 -s totcat -d 0/0 -j ACCEPT
[root@topcat]# ipchains -A input -p icmp --icmp-type echo-reply -i eth0 -s 0/0 -d totcat -j ACCEPT
[root@topcat]# ipchains -A output -p icmp --icmp-type echo-reply -i eth1 -s 0/0 -d 10.0.0.0/8 -j ACCEPT
```

- **Rule 1** disallows any `ping` request from the Internet. Note that we use **REJECT**. Recall from Table 16.3 on page 445 that DENY and REJECT are identical when the rule matches ICMP.
- **Rule 2** allows client `pings` from the internal network to pass through the input chain when they arrive at `eth1`.
- **Rule 3** is the general masquerading rule. It masquerades all internal 10.0.0.0 addresses as 202.7.1.19. This rule will masquerade all traffic and is required by all subsequent rules that permit external access.
- **Rule 4** permits the echo-request to traverse the output chain with respect to `eth0` and head off to the destination system.
- **Rule 5** allows the return echo-reply to traverse the input chain after it enters `eth0`.
- **Rule 6** permits the echo-reply to pass through the output chain with respect to `eth1` and go off to the internal client.

To better understand the flow of the packet as well as the chains it passes through, it may be useful to take a look at Figure 16.4 on page 475. That diagram is specific to `tcp` and is discussed in *Rules for Allowing ftp from the Internal Network to the Internet* below, but the flow of packets through the chains is conceptually the same for all traffic through the firewall.

Now that we have taken care of `ping`, we need to set up the rules for ICMP error messages. We'll use the custom chain in Example 16-15 on page 462. Be sure to create the chain before you execute the commands given in Example 16-15. Once accomplished, we can add rules to jump to the `icmperr` chain as shown in Example 16-32.

#### Example 16-32 Rules that Invoke the ICMP Custom Chain

```
[root@topcat]# ipchains -A input -p icmp -s 0/0 -d topcat -j icmperr
[root@topcat]# ipchains -A output -p icmp -s 10.0.0.0/8 -d 0/0 -j icmperr
```

Note that we are specifying both source and destination in these rules. In particular, we will not allow our internal network to generate ICMP messages out to the Internet.

Except for the rules in *Finally!* on page 480, the rules we add after this point are not order dependent as long as they are added *after* the ones we've added up through this section.

### Rules for Allowing ftp from the Internal Network to the Internet

Based on the requirements provided in *Simple Internal Network* on page 469, we must allow `ftp`. The setup for `ftp` is fairly complex because it utilizes two distinct ports for communication. In active ftp mode (executing `ftp` from the command line), the initial packet generated by the client sets the destination port to `tcp` (port number 21). For responses from the server, 21 becomes the source port number. When the client requests data from the server—for example, by executing `ls` at the `ftp` prompt—the client sends the request using the `ftp-data` port (port number 20) as the destination port. Passive ftp (usually implemented through web browsers) allows the `ftp` server to choose the data port. Fortunately we don't need to worry about passive ftp because `ip_masq_ftp` (see the references cited in the section, *Masquerading Documentation* on page 487) automatically takes care of it for us. But we do need to write the rules. It will help our understanding to refer to the diagram in Figure 16.4.

In order to configure this capability, we will need eight rules for `tcp` and one masquerading rule. The masquerading rule will be general and will apply to all connections originating from the internal network. As we step through this process, the numbers in Figure 16.4 correspond to the FTP rules noted in the following sections. The reference to masquerade in Figure 16.4 corresponds to *Masquerade Rule* on page 476.

#### FTP Rule 1

A client in the internal network wants to connect to the Internet via `tcp`. The client will execute a command like `ftp ftp.reallycool.com`.
