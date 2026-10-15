describes what the variable does and shows its minimum, maximum, and default values. For example:

```
```text
$ ndd -h | grep source
ip_forward_src_routed - Controls forwarding of source routed packets
```
```

```
```text
$ ndd -h ip_forward_src_routed
ip_forward_src_routed:
  Set to 1 to forward source-routed packets; set to 0 to
  disable forwarding. If disabled, an ICMP Destination
  Unreachable message is sent to the sender of source-
  routed packets needing to be forwarded. [0,1] Default: 1
```
```

**ndd**’s output claims that this version of HP-UX allows forwarding of source-routed packets by default. That may be the kernel’s preference, but in fact the default **/etc/rc.config.d/nddconf** file on our lab system disables this behavior:

```
```text
TRANSPORT_NAME[2]=ip
NDD_NAME[2]=ip_forward_src_routed
NDD_VALUE[2]=0
```
```

The 2s here indicate the third of ten possible variables to be set in **nddconf**. For the next variable that you wanted to change, you would add another copy of the same three lines with appropriate values and with subscript 3 instead of 2. Unfortunately, only 10 parameters can be set through **nddconf**.

To view and change the value of the ip_forward_src_routed variable by hand, use **ndd -get** and **ndd -set** (the syntax is slightly different from that on Solaris systems):

```
```text
$ ndd -get /dev/ip ip_forward_src_routed
0
$ sudo ndd -set /dev/ip ip_forward_src_routed 1
$ ndd -get /dev/ip ip_forward_src_routed
1
```
```

# HP-UX security, firewalls, filtering, and NAT

Table 14.12 shows HP-UX’s default behavior with regard to various touchy network issues. For a brief description of the implications of these behaviors, see *Security issues* on page 472. You can modify most of them with **ndd**.

# Table 14.12  Security-related network behaviors in HP-UX

| Feature | Default | Control through ndd |
|---|---|---|
| IP forwarding | dynamicᵃ | Set ip_forwarding: 0 = off, 1 = on, 2 = dynamic |
| ICMP redirects | obeysᵇ | Set ip_ire_redirect_interval to 0 to disable |
| Source routing | ignores | Set ip_forward_src_routed to 1 to enable |
| Broadcast ping (forward) | blocked | Set ip_forward_directed_broadcasts |
| Broadcast ping (respond) | ignores | Set ip_respond_to_echo_broadcast |

ᵃ On with >1 network interface; off otherwise.
ᵇ The redirect entries are by default preserved for five minutes.