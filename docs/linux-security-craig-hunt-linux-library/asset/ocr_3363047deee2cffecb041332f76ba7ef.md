worked with kernel versions 1.2 through 2.1. The last version of ipfwadm was released in July 1996. Starting with kernel version 2.1.102 and later, ipfwadm has been replaced by Paul “Rusty” Russell and Michael Neuling’s iptchains, which addresses some of ipfwadm’s limitations, namely:

+   • 32-bit counters, which were previously unable to keep track of packets coming into high-speed network interfaces
+   • Inability to deal adequately with IP fragmentation
+   • No support for transport layer protocols other than UDP and TCP
+   • No support for inverse rules, where you look for the opposite of a condition (e.g., -i ! eth0).

If your Linux distribution only supports ipfwadm, you are running an old system and you should upgrade to a newer version. Most recent Linux vendors include the iptchains utility in their standard distribution. The next section explains how to use the iptchains command and includes some real-life examples of how you can use it to build a network layer firewall.

# ## Using iptchains

The name iptchains refers to the fact that the Linux kernel consults three separate chains, or sequence of rules, when it receives a network layer packet. There are three chains that come built-in with the Linux kernel:

+   • **Input Chain** The input chain handles packets that arrive at one of the server’s interfaces and are bound for the local host.
+   • **Output Chain** The output chain handles packets that are originated by the local system and are bound for a remote host.
+   • **Forward Chain** The forward chain handles packets that arrive at one of the server’s interfaces and are bound for a remote host.

Each of these three chains can contain a set of rules that define access controls based on the source/destination address, the TCP/UDP port, or the protocol ID. By specifying a set of rules that enforce the provisions of your security policy, you can build a firewall device using the Linux kernel as the underlying system and iptchains as your configuration tool. Let’s take a look at the syntax of the iptchains command.

The iptchains utility uses the following syntax:

```
```
iptchains command chain rule-specifications [options] -j action
```
```

The command field is used to maintain the list of rules for a given chain and defines, for example, whether you’re adding a rule, deleting a rule, or simply listing the rules that have already been defined for that chain. Table 9.1 contains a list of valid commands supported in iptchains.