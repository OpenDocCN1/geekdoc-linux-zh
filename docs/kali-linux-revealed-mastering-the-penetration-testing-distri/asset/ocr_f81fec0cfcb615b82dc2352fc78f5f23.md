```
Unaccepted Keys:
kali-scratch
Proceed? [n/Y] y
Key for minion kali-scratch accepted.
```

# 10.2.2. Executing Commands on Minions

As soon as minions are connected, you can execute commands on them from the master:

```
master# salt '*' test.ping
kali-scratch:
    True
kali-master:
    True
```

This command asks all minions (the \`\`*\`\` is a wildcard targeting all minions) to execute the ping function from the test execution module. This function returns a True value on success and is a simple way to ensure that the connection is working between the master and the various minions. You can also target a specific minion by giving its identifier in the first parameter, or possibly a subset of minions by using a less-generic wildcard (such as \`\`*\`\`\`scratch\`\` or \`\`kali-*\`\`). Here is an example of how to execute an arbitrary shell command on the kali-scratch minion:

```
master# salt kali-scratch cmd.shell 'uptime; uname -a'
kali-scratch:
    05:25:48 up 44 min,  2 users,  load average: 0.00, 0.01, 0.05
    Linux kali-kali-scratch 4.5.0-kali-amd64 #1 SMP Debian 4.5.3-2kali1 (2016-05-09) x86_64 GNU/Linux
```

> | Salt Module Reference | There are many execution modules available for all sorts of use cases. We won’t cover them all here, but the full list is available at https://docs.saltstack.com/en/latest/ref/modules/all/index.html. You can also obtain a description of all the execution modules and their available functions on a given minion with the salt minion sys.doc command. Running this command returns a very long list of functions, but you can filter the list by passing the name of a function or module prefixed by its parent module as a parameter:
> 
> ```salt
> master# salt kali-scratch sys.doc disk.usage
> disk.usage:
>     Return usage information for volumes mounted on this minion
> ``` |

One of the most useful modules is pkg, which is a package manager abstraction relying on the appropriate package manager for the system (apt-get for Debian and its derivatives like Kali).