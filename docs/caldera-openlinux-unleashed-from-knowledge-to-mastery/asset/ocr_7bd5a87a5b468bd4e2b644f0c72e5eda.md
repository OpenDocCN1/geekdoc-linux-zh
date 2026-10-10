| Local Process | A local process can receive packets after the routing decision and send them through the routing decision step on to the output chain. |
| lo Interface | If packets from a local process are sent to another local process, they are sent through the output chain with the interface set to 'lo' (usually called the loopback interface) and come back in to the input chain with the interface still set to 'lo'. |
| forward Chain | Any packets destined for another machine pass through the forward chain. |
| output Chain | The output chain is traversed by all packets just before they are sent on. |

# Using ipchains to Configure and
Check the Firewall

The program ipchains is used to configure the firewall (firewall chains) and view information about it. ipchains allows you to work on entire chains or the rules within a chain. It also allows you to define new chains in addition to the three built-in chains. It is generally run from the command line to set things up, and then preferably from a system startup script when the firewall boots.

ipchains doesn't store the firewall configuration anywhere, so it is lost when the firewall is shut down. However, it is easy to add ipchains commands to system startup scripts that will reconfigure the firewall when it boots up. There are also a few scripts that help simplify the process.

# Working on an Entire Chain

Six operations work on entire chains. The first five all have the same syntax:

```
ipchains -[LFNXZ] [chain] [options]
```

The brackets ([ ]) are not part of the command, but signify either optional arguments, or that only one of the arguments within the brackets is used. For example, you may not have any options because they are not required. However, you must choose one of -L, -F, -X, -N, and -Z to perform the corresponding action.