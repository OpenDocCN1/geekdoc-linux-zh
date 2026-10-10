Before a chain can be deleted, it must be empty (use the -F option to flush it), and there must be no rules in other chains that refer to it. Any rules that refer to it must either be deleted or replaced by rules with different targets. If no chain is specified, `iptables` will try to delete all user-defined chains.

> Note  
> The three built-in chains (`input`, `forward`, and `output`) cannot be deleted.

For example, if you wanted to clear the entire firewall setup so that you could start over, you could issue the following two commands, which will flush all chains and then delete all user-defined chains:

```
# iptables -F
# iptables -X
```

# ### Creating a New Chain

You can create a new chain of rules (a user-defined chain) using the -N option:

```
iptables -N new_chain
```

`new_chain` is the name you want for your new chain. You cannot use a name that is already in use. So, right from the outset, you cannot use the names `input`, `forward`, and `output`.

There is no easy way to rename a chain. You will simply have to create a new chain with the new name and set it up like the old chain. Any rules that referred to the old chain must be redefined to refer to the new chain. You can then delete the old chain and forget that it ever existed.

For example, if you wanted to set up a chain for packets coming in off the `ppp0` interface, you could create a new chain called `ppp0` with the following command:

```
# iptables -N ppp0
```

You can then place rules that apply only to packets coming from the `ppp0` interface in this chain.

Creating the chain and adding rules to it is not sufficient, however, to put the chain in use. The name of the chain is only there for your convenience and is meaningless to the kernel. The kernel does not look at the name and think, “Okay. Packets coming from `ppp0` go to the `ppp0` chain.” You need to set up a rule in one of the built-in chains (or a user-defined chain that can be reached from one of the built-in chains) that has the chain `ppp0` as its target. This is easy to do and will be discussed later.