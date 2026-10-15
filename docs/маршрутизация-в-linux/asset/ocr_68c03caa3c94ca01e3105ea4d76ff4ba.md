All of this is easier done than said. To illustrate, here’s a simple example that will block any telnet connection coming in from outside the local network:

```
root@host:> iptables -A INPUT -s ! 10.0.0.0 -p tcp --destination-port telnet -j REJECT
```

This example will reject (-j REJECT) any packets attempting to establish a telnet connection, unless they’re being made from inside the local network. Because using telnet is a bad idea these days anyway, you can keep your users from making outgoing telnet connections as well with the following:

```
root@host:> iptables -A OUTPUT -p tcp --destination-port telnet -j REJECT
```

# Creating a New Chain

If you’d like to specify a chain other than INPUT, OUTPUT, or FORWARD, you can create a custom chain. This one is easy—simply decide what name you’d like to use for the new chain (up to 31 characters) and use the new chain (-N) option.

```
root@host:> iptables -N NEW_CHAIN_NAME
```

Now if you run the iptables -L command, you’ll see something like this:

```
root@aesir:~ > iptables -L
Chain INPUT (policy ACCEPT)
 target     prot opt source               destination
Chain FORWARD (policy ACCEPT)
 target     prot opt source               destination
Chain OUTPUT (policy ACCEPT)
 target     prot opt source               destination
Chain NEW_CHAIN_NAME (0 references)
 target     prot opt source               destination
```

As you can see, when you create a new chain, it has no default rules, unlike the default chains.

# Flushing a Rule

As with iptables, flushing a chain requires using the -F. To flush the OUTPUT chain, for instance, you would type iptables -F OUTPUT. This will get rid of all rules that have been set in that chain.

# For More on iptables

This has been a fairly brisk overview of iptables. If you want to learn more about them, the man page contains a fairly extensive description of the use of iptables. The Netfilter home page also has several well-written HOWTOs by the primary author of Netfilter, Rusty Russell. Even if you’re not going to use Netfilter or iptables extensively, they’re worth reading. How can you pass up documentation by an author who