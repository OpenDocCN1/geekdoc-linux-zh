# IP ADDRESSES EXPRESSED AS SYMBOLIC NAMES

Remote hosts and networks may be specified as fully qualified hostnames or network names. Using a hostname is especially convenient for firewall rules that apply to an individual remote host. This is particularly true for hosts whose IP addresses can change or that invisibly represent multiple IP addresses, such as ISP mail server sometimes do. In general, however, remote addresses are better expressed in dotted quad notation because of the possibility of DNS host hostname spoofing.

Symbolic hostnames can't be resolved until DNS traffic is enabled in the firewall rules. If host-names are used in the firewall rules, those rules must follow the rules enabling DNS traffic, unless `/etc/hosts` contains entries for the hostnames.

Furthermore, some distributions such as Red Hat use a boot environment that installs the fire-wall rules before starting the network or any other services, including BIND. If symbolic host and network names are used in the firewall script, those names must have entries in `/etc/hosts` to be resolved.

iptables allows the address to be suffixed with a bit mask specifier. The mask's value can range from 0 through 32, indicating the number of bits to mask. As discussed in Chapter 1, “Preliminary Concepts Underlying Packet-Filtering Firewalls,” bits are counted from the left, or most significant, bit. This mask specifier indicates how many of the leading bits in the address must exactly match the IP address specified.

A mask of 32, `/32`, means that all the bits must match. The address must exactly match what you've defined in the rule. Specifying an address as `192.168.10.30` is the same as specifying the address as `192.168.10.30/32`. The `/32` mask is implied by default; you don't need to specify it.

An example using masking is to allow connections to a particular service to be made only between your machine and your ISP's server machines. Let's say that your ISP uses addresses in the range of `192.168.24.0` through `192.168.27.255` for its server address space. In this case, the address/mask pair would be `192.168.24/22`. As shown in Figure 4.1, the first 22 bits of all addresses in this range are identical, so any address matching on the first 22 bits will match. Effectively, you are saying that you will allow connections to the service only when offered from machines in the address range `192.168.24.0` through `192.168.27.255`.

A mask of `0`, `/0`, means that no bits in the address are required to match. In other words, because no bits need to match, using `/0` is the same as not specifying an address. Any unicast address matches. `iptables` has a built-in alias for `0.0.0.0/0`, `any/0`. Note that `any/0`, whether implied or stated, does not include broadcast addresses.