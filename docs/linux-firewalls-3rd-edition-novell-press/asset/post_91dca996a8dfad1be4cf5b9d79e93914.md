
As each externally originating packet arrives at the network interface, its header fields are compared against each rule in the interface's INPUT chain until a match is found. Conversely, as each locally generated packet is sent out, its header fields are compared against each rule in the interface's OUTPUT chain until a match is found. In either direction, once a match is found, the comparison stops and the rule's packet disposition is applied: ACCEPT, DROP, or, optionally, REJECT. If the packet doesn't match any rule on the chain, the default policy for that chain is applied. The bottom line is that the *first matching rule wins*.

The numeric service port numbers, rather than their symbolic names, as listed in `etc/services`, are used in all the filter examples in this chapter. iptables supports the symbolic service port names. The examples in this chapter use the numeric values because the symbolic names are not consistent across Linux distributions—or even from one release to the next. You could use the symbolic names for clarity in your own rules, but remember that your firewall could break with the next system upgrade. I've found it much more reliable to use the port numbers themselves. The last thing you want in a firewall is ambiguity, which is just what is introduced by using names instead of numbers for ports.

Most Linux distributions implement iptables as a set of loadable program modules. Most or all of the modules are dynamically and automatically loaded on first use. If you choose to build your own kernel, which I nearly always do, you'll need to compile in support for Netfilter, either as modules or directly into the kernel. The `iptables` command must be invoked once for each individual firewall rule you define. This is initially done from a shell script. This chapter will use a script called `rc.firewall1`. The location of the script is dependent on the flavor of Linux where the script will be used. For example, on Red Hat and SUSE systems, the script should likely be within the `/etc/rc.d/` directory whereas on Debian, `/etc/init.d/` is the correct location. In cases in which shell semantics differ, the examples are written in Bourne (`sh`) or Bourne Again (`bash`) shell semantics.

The shell script sets a number of variables. Chief among these is the location of the `iptables` command itself. It's important to set this in a variable so that it is explicitly located. There's no excuse for ambiguity with a firewall script. The variable used to represent the `iptables` command in this chapter is `SIPT`. If you see `SIPT`, it is a substitute for the `iptables` command. You could just as easily execute the commands from the shell by typing `iptables` instead of `SIPT`. However, for use in a script (which is the intention in this chapter), setting this variable is a good idea.

The script should begin with the "shebang" line invoking the shell as the interpreter for the script. In other words, put this as the first line of the script:

```
#!/bin/sh
```

The examples are not optimized. They are spelled out for clarity. Firewall optimization and user-defined chains are discussed separately in Chapter 5, “Firewall Optimization.”

# Build Versus Buy: The Linux Kernel

There is great debate over whether it is advisable to compile a custom kernel or stick with the “stock” kernel that comes with a given Linux distribution. The debate also includes whether it is inherently better to compile a monolithic kernel (in which everything is compiled into the kernel) or use a modular kernel. As with any debate, there are pros and cons to each method. On the one hand there are those who always (or almost always) build their own kernel, sometimes called “rolling their own.” On the other hand, there are those who rarely or never roll their own kernel. There are those who always build monolithic kernels and others who use modular kernels.

Building a custom kernel has a few advantages. First is the capability to compile in only the exact drivers and options necessary for the computer to run. This is great for a server such as a firewall because the hardware rarely, if ever, changes. Another advantage to compiling a custom kernel, if you choose a monolithic kernel, is the capability to completely prevent some types of attacks against the computer. Although attacks against monolithic kernels are possible, they are less common than attacks against modular kernels. Further, when you roll your own kernel you’re not confined to the kernel version used by the distribution. This enables you to use the latest and greatest kernel, which may include bug fixes for your hardware. Finally, with a custom kernel you can apply additional security enhancements to the kernel itself. One such enhancement is covered in Chapter 13, “Kernel Enhancements.”

Building a custom kernel is not without its own set of pitfalls. If you roll your own kernel, you can no longer use the distribution’s kernel updates. Actually, you can revert to the distribution’s kernel and use the updates, but it’s likely that the distribution uses an earlier version of the kernel that may reintroduce bugs that were fixed in your custom version. Using a stock kernel also makes it easier to obtain support from the vendor for kernel issues.

As alluded to earlier, I nearly always roll my own kernel for production server machines. The situations in which direct support is an absolute requirement are the only exceptions. These are few and far between. I believe the capability to customize the kernel to the computer and add greater security through additional patches far outweighs the need to use official kernel updates from the distribution.

# Source and Destination Addressing Options

A packet’s source address and destination address can both be specified in a firewall rule. Only packets with that specific source or destination address match the rule. Addresses may be a specific IP address, a fully qualified hostname, a network (domain) name or address, a limited range of addresses, or all-inclusive.

# IP ADDRESSES EXPRESSED AS SYMBOLIC NAMES

Remote hosts and networks may be specified as fully qualified hostnames or network names. Using a hostname is especially convenient for firewall rules that apply to an individual remote host. This is particularly true for hosts whose IP addresses can change or that invisibly represent multiple IP addresses, such as ISP mail servers sometimes do. In general, however, remote addresses are better expressed in dotted quad notation because of the possibility of DNS host hostname spoofing.

Symbolic hostnames can't be resolved until DNS traffic is enabled in the firewall rules. If hostnames are used in the firewall rules, those rules must follow the rules enabling DNS traffic, unless `/etc/hosts` contains entries for the hostnames.

Furthermore, some distributions such as Red Hat use a boot environment that installs the firewall rules before starting the network or any other services, including BIND. If symbolic host and network names are used in the firewall script, those names must have entries in `/etc/hosts` to be resolved.

iptables allows the address to be suffixed with a bit mask specifier. The mask's value can range from 0 through 32, indicating the number of bits to mask. As discussed in Chapter 1, “Preliminary Concepts Underlying Packet-Filtering Firewalls,” bits are counted from the left, or most significant, bit. This mask specifier indicates how many of the leading bits in the address must exactly match the IP address specified.

A mask of 32, `/32`, means that all the bits must match. The address must exactly match what you've defined in the rule. Specifying an address as `192.168.10.30` is the same as specifying the address as `192.168.10.30/32`. The `/32` mask is implied by default; you don't need to specify it.

An example using masking is to allow connections to a particular service to be made only between your machine and your ISP's server machines. Let's say that your ISP uses addresses in the range of `192.168.24.0` through `192.168.27.255` for its server address space. In this case, the address/mask pair would be `192.168.24/22`. As shown in Figure 4.1, the first 22 bits of all addresses in this range are identical, so any address matching on the first 22 bits will match. Effectively, you are saying that you will allow connections to the service only when offered from machines in the address range `192.168.24.0` through `192.168.27.255`.

A mask of `0`, `/0`, means that no bits in the address are required to match. In other words, because no bits need to match, using `/0` is the same as not specifying an address. Any unicast address matches. `iptables` has a built-in alias for `0.0.0.0/0`, `any/0`. Note that `any/0`, whether implied or stated, does not include broadcast addresses.
