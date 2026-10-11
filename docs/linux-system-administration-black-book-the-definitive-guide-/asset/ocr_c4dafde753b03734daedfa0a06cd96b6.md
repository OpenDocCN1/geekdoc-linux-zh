> *TIP:* *This command actually has much more to it. Type “man-dig” to investigate further.*

# Debugging Your Setup

A domain administrator can get highly frustrated trying to figure out why a huge set of zone files detailing an entire class C network, including subnetworks, special services, and more, is not resolving properly. Enter the **dnswalk** tool. This program is a zone debugger, available at [www.visi.com/~barr/dnswalk/](http://www.visi.com/~barr/dnswalk/). These zones have to be loaded into the name server before this tool can go through them, so it is not helpful if you cannot get the server to load the files. See the Immediate Solutions section “Installing And Running **dnswalk**” if you want to give this tool a try.

# Getting Information About Hosts

Sometimes, you need to get information about a particular machine on another domain, or maybe you want to test and make sure that some of the special service machines on your domain are showing up properly. The tool that helps you on this front is the **host** command. You use this command in the following format:

```
host flags machine
```

> *NOTE:* *A similar command called* nslookup *does essentially the same thing.*

Available *flags* for the **host** command are given in Table 11.6. The *machine* entry can be either the hostname for a local machine or the full *host.domain.extension* value. That is, unless you use the *-l* flag, in which case you can just use *domain.extension*.

> *TIP:* *For additional information on the types available with the -t flag, see the* named *man page.*

# Table 11.6 Flags available with the host command.

| Flag | Purpose | Values |
|---|---|---|
| -a | Gives all available information about the host specified. | None |
| -d | Debugging mode. Shows all network transactions. | None |
| -l | Gives information for the entire domain. Essentially does a full zone transfer. | None |
| -r | Asks your own name server only; does not send the request out to others. | None |

(continued)